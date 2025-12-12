# Introduction to Protobuf
The asset files in Miliastra Wonderland are primarily stored in one or more Protobuf structures. If you are unfamiliar with this, we recommend referring to the [official documentation](https://protobuf.dev/programming-guides/encoding/). Or, you can look at this document first; we'll guide you through it quickly in a simple and straightforward way! 👌

If you find any discrepancies between this document and the official version, please refer to the official documentation.

## Varint: Variable-length Integers
When storing files or transferring data over the Internet, we might want to save as much space as possible and avoid storing too much duplicate/useless data. Besides data compression, here's another way to save space: ***varints***!

Varint does not use a fixed 32-bit or 64-bit integer. Instead, it stores data in the lower 7 bits of each byte as needed. When there are more bits remaining, it sets the most significant bit (MSB) to 1 to indicate that there are more bytes to come.

### Conversion rules
Let's take the unsigned decimal integer `360` as an example to understand how to convert an integer to varint form:

1. Write `360` ​​in binary form: `1 0110 1000`

2. Starting from the least significant bit, group 7 bits into a group: `[Group 1: 1101000, Group 2: 10]`

3. Treat each group as a byte and fill it with zeros to make 8 bits (this step is done automatically by the computer): `[0110 1000, 0000 0010]`

4. Starting from the first byte, fill the most significant bit with 1 until the last byte: `[1110 1000, 0000 0010]`

5. We can write it in hexadecimal form for easier human reading: `E8 02`

Here, we have completed the entire process of converting an unsigned integer to varint: `360 -> E802`

### Code Implementation
Calculate the required buffer size:

- C#
  ```c#
  static int SizeOfVarintBuffer(ulong value) {
      // Even if the value is zero,
      // it still needs to be allocated one byte of space.
      if (value == 0) return 1; 
      int bits = 64 - System.Numerics.BitOperations.LeadingZeroCount(value);
      return (bits + 6) / 7; // Equivalent to ceil(bits / 7)
  }
  ```

- C/C++
  ```cpp
  // Using GCC extended methods
  int size_of_varint_buffer_gcc(uint64_t value) {
      if (!value) return 1;
      int bits = 64 - __builtin_clzll(value);
      return (bits + 6) / 7;
  }
  // Independent implementation
  int size_of_varint_buffer(uint64_t value) {
      int size = 1;
      while (value >= 0x80) { // If data still remains
        value >>= 7; // Each byte encodes 7 valid bits
        size++;
      }
      return size;
  }
  ```

Convert unsigned integers to varint:

- C#
  ```c#
  static byte[] ToVarint(ulong value) {
      // See the code above for details
      int size = SizeOfVarintBuffer(value);
      var result = new byte[size];
      for (int i = 0; i < size; i++) {
          // Get the lowest 7 bits
          byte data = (byte)(value & 0x7F);
          value >>= 7;
          // If there is still data remaining, mark the MSB.
          if (value != 0) data |= 0x80;
          result[i] = data;
      }
      return result;
  }
  ```

- C/C++
  ```cpp
  uint8_t* to_varint(uint64_t value) {
      // See the code above for details
      int size = size_of_varint_buffer(value);
      uint8_t* result = (uint8_t*) malloc(size);
      for (int i = 0; i < size; i++) {
          // Get the lowest 7 bits
          uint8_t data = (uint8_t)(value & 0x7F);
          value >>= 7;
          // If there is still data remaining, mark the MSB.
          if (value != 0) data |= 0x80;
          result[i] = data;
      }
      return result;
  }
  ```

Decode Varint into an unsigned integer:

- C#
  ```c#
  static ulong DecodeVarint(byte[] raw) {
      ulong result = 0;
      // If we can guarantee that `raw` is a valid varint,
      // only one of the exit conditions needs to be written here.
      // However, if it might be insufficient in length
      // or contain other irrelevant data, two checks must be performed.
      for (int i = 0; i < raw.Length; i++) {
          byte data = (byte)(raw[i] & 0x7F);
          result |= (ulong)(data) << (i * 7);
          if (raw[i] >> 7 == 0) break; // If no more data remaining, exit.
      }
      return result;
  }
  ```

- C/C++
  ```cpp
  uint64_t decode_varint(uint8_t* raw, int size) {
      uint64_t result = 0;
      // If we can guarantee that `raw` is a valid varint,
      // only one of the exit conditions needs to be written here.
      // However, if it might be insufficient in length
      // or contain other irrelevant data, two checks must be performed.
      for (int i = 0; i < size; i++) {
          uint8_t data = (byte)(raw[i] & 0x7F);
          reuslt |= (uint64_t)(data) << (i * 7);
          if (raw[i] >> 7 == 0) break; // If no more data remaining, exit.
      }
  }
  ```

### Encoding Signed Integers
You may have noticed that when discussing how to encode a varint, we've consistently emphasized using ***unsigned integers*** — this is because most modern computers use a form called ***two's complement*** to store negative numbers. This simplifies circuit design (natural overflow during arithmetic operations allows positive and negative numbers to be added together to zero, without needing to consider whether an integer is negative).

When representing negative numbers using two's complement, we simply need to invert each bit and add 1. Let's take 75 as an example:

- Write it in binary: `75 --> 0100 1011`
- Bitwise inversion: `1011 0100`
- Add 1: `1011 0101`

We get `-75 = 1011 0101`!

Now let's verify this. We know that `75 + (-75) = 0`, and see if this rule holds true when written in binary:

```
  0100 1011
+ 1011 0101
-----------
1 0000 0000
```

Because computers use a fixed number of bits to store integers, the highest 1 that exceeds the storage range after addition will be discard. Therefore, we determine that `75 + (-75) = 0` ✅

However, in this representation, no matter how the negative number is shifted, its highest bit will always be 1, and the conversion algorithm will never terminate — this is clearly problematic! Fortunately, we can use a technique called `ZigZag` to first represent signed integers as unsigned, and then encode them to varint:

| Before | After |
|:-----:|:-----:|
|0|0|
|-1|1|
|1|2|
|-2|3|
|2|4|
|...|...|
|0x7FFFFFFF|0xFFFFFFFE|
|-0x80000000|0xFFFFFFFF|

- Encoding Method:
  - `(n << 1) ^ (n >> 31)` (32-bit)
  - `(n << 1) ^ (n >> 63)` (64-bit)
- Decoding Method
  - `(n >> 1) ^ -(n & 1)`

## Protobuf: An Extensible Protocol for Serializing Data Structures
Protobuf is a small, fast, and language-independent storage protocol that operates on a message-by-message basis. Each message defines a series of fields and their corresponding id to store data. It looks like this:

```proto
message Person {
  int32  age  = 1; // Field 1
  string name = 2; // Field 2
}
```

1. In file, each message begins with a tag.

2. Some tags may be missing, appear out of order, or appear repeatedly (e.g., in a list storing objects). Therefore, the parser must be able to flexibly read tags and cannot rely on the byte sequence read from the file.
    > Note: Although observation suggests that Genshin write tags to the file in tag number order, you still cannot assume their order, as 3rd-party programs may not adhere to this rule!

3. When a field is missing, it should be assumed to be the default value of the type.
    > Note: Sometimes Genshin may not write certain values ​to the file if they are zero; this requires special attention!

4. Tags use the varint form, where the lowest 3 bits represent the type, and the remaining significant bits represent the tag number, that is: `(id << 3) | type`.

5. Tag numbers must be positive integers.

6. The following are the available tag types, which Genshin uses to represent specific types:

    | ID | Name | Types |
    |:--:|:----|:-----|
    |0|VARINT|Integer, Enum, Boolean|
    |1|FIXED64|Double, Fixed64 (less common)|
    |2|LENGTH|String, Compound, List, Dictionary|
    |3|GROUP_START| (Not used)|
    |4|GROUP_END| (Not used)|
    |5|FIXED32|Float, Fixed32 (less common)|

    For the LENGTH type, there is an additional field after the tag to specify the content length, using the varint form.

### Encoding Example
Assume a field is numbered `1`, representing a compound tag containing the string `"Hello, World!"` (field 1) and a boolean value `true` (field 2):

1. The field is stored using the LENGTH type: `(1 << 3) | 2 --> 0x0A`
   
2. The first sub-tag is: `(1 << 3) | 2 --> 0x0A`
   
3. Converted the string to a UTF-8 encoded byte sequence without null-terminated: `[0x48 0x65 0x6C 0x6C 0x6F 0x2C 0x20 0x57 0x6F 0x72 0x6C 0x64 0x21]`, the length is: `0x0D`
   
4. The second sub-tag is: `(2 << 3) | 0 --> 0x10`

5. Convert `true` to varint: `0x01`

6. Calculate the total length of the compound: `0x11`

7. Write the data to the file according to the Protobuf format: `0A 11 0A 0D 48 65 6C 6C 6F 2C 20 57 6F 72 6C 64 21 10 01`

8. Done!

Suppose a field numbered `4` stores the Component GUID `1073741825`:

1. We use the VARINT type to store the integer, so the tag value is `(4 << 3) | 0 --> 0x20`.

2. Convert `1073741825` to varint form, resulting in `[0x81, 0x80, 0x80, 0x80, 0x04]`.

3. Write the bytes sequentially to the file: `20 81 80 80 80 04`.

4. Done!

In fact, if you try exporting a UI Control Group component and opening it with VSCode's built-in Hex Editor, you might see the data very similar to what we calculated here at the `0x1D` offset. This is actually where Genshin saves the Component GUID 😉<br/> (although its position may change slightly depending on the file length, you cannot hardcode this offset in your program).

```
     00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F
   + ———————————————————————————————————————————————
00 | 00 00 ?? ?? 00 00 00 01 00 00 03 26 00 00 00 03
10 | 00 00 ?? ?? 0A ?? ?? 0A 0A 10 01 18 08 20 81 80
20 | 80 80 04 (... omitted)
```

> Note 1: The question marks above is related to the file size. Please refer to the [Overview](/docs/en/Overview.md) for an introduction to the file header.
> 
> Note 2: If you find that the exported GUID is different from the one shown here, this is normal. You can try to manually calculate it and convert it back to an integer from varint form to verify whether you have mastered this chapter!
