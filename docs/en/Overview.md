# Miliastra Wonderland Export File Format Documentation

### Encoding
- The Protocol Buffers (Protobuf) library is used for data serialization and deserialization. If you are unfamiliar with this, please refer to the [official documentation](https://protobuf.dev/programming-guides/encoding/).
- All strings are encoded in UTF-8 format.

## File Metadata
Whether it's a `.gip` (Project), `.gil` (Level), `.gia` (Asset), or `.gir` (Runtime) file, they all have a similar structure:

```
(Start)
[File Size:      4 bytes]
[Version Number: 4 bytes]
[Header Marker:  4 bytes]
[File Type:      4 bytes]
[Content Length: 4 bytes]

(Content Payload: Arbitrary Length)

[Tail Marker:    4 bytes]
(End)
```

These fields are stored in big-endian order. Their meanings and uses will be explained in detail below.

### File Size
- Offset: `0x00`
- Actual file size minus 4 bytes (excluding the 4 bytes of the tail marker).

### Version Number
- Offset: `0x04`
- As of Genshin Impact V6.1 (Luna II), this field is always set to `00 00 00 01`.
- It seems that even if other values ​​are set, it can still be loaded normally, but it is recommended to keep it consistent with the official values.

### Header Marker
- Offset: `0x08`
- Value: `00 00 03 26`
- ⚠️ **This field is strictly validated. Any other value will be rejected**.

### File Type
- Offset: `0x0C`
- An enumeration representing the file type, accepting the following values:
  - GIP = `00 00 00 01`
  - GIL = `00 00 00 02`
  - GIA = `00 00 00 03`
  - GIR = `00 00 00 04`

### Content Length
- Offset: `0x10`
- Actual file size minus 24 bytes (excluding the fixed 20 bytes for the header and the 4 bytes of the tail marker).

### Content Load
See the corresponding page for details.

### Tail Marker
- Offset: Value of the `File Size` field
- Value: `00 00 06 79`
- ⚠️ **This field is strictly validated. Any other value will be rejected**.

## Did you know?
This is a minimal example of a valid GIA file that can pass game verification, but leaves nothing on the Manage Asset interface! 🤪

```
00 00 00 14 00 00 00 01 00 00 03 26 00 00 00 03 00 00 00 00 00 00 06 79
```

| Field          | Value       | Description |
|:---------------|:------------|:-----------:|
|File Size       |`00 00 00 14`| 14 bytes    |
|Version Number  |`00 00 00 01`| 1           |
|Header Markup   |`00 00 03 26`| Correct ✅  |
|File Type       |`00 00 00 03`| GIA File    |
|Content Length  |`00 00 00 00`| 0 Bytes     |
|Content Payload |-------------| None        |
|Tail Marker     |`00 00 06 79`| Correct ✅  |
