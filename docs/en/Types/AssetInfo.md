# AssetInfo
Metadata for an asset.

## Definition
```proto
message AssetInfo {
    AssetSpecialType special_type = 2;
    AssetCategory category = 3;
    uint32 guid = 4;
}
```

## Fields

### special_type
- Type: Enum\<[`AssetSpecialType`](/docs/en/Types/AssetSpecialType.md)>
- Used for special types of assets
- Usually set to `DEFAULT`

### category
- Type: Enum\<[`AssetCategory`](/docs/en/Types/AssetCategory.md)>
- Primary category of the asset
- Most assets are categorized with this field
- The `special_type` field is only relevant when this field is `SPECIAL`
- This field may be omitted when it is 0 (`SPECIAL`), as is detailed in the [Protobuf introduction](/docs/en/Introduction%20to%20Protobuf.md)

### guid
- Type: unsigned int
- Globally unique identifier of the asset
- Testing shows that you can use anything for the GUID, as long as it is consistently used.
- When importing assets, the game will reallocate GUIDs based on related assets.
- The game seems to always allocate GUIDs starting from `0x40000000` (1073741824).
