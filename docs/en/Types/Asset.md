# Asset
> This section is still being edited and tested.

## Definition
```proto
message Asset {
    AssetInfo info = 1;
    repeated AssetInfo related = 2;
    string name = 3;
    AssetType type = 5;

    oneof content {
        EntityDefinition entity = 11;
        // ??? = 12;
        NodeGraph node_graph = 13;
        CompositeDefinition composite = 14;
        Configuration config = 15;
        Terrain terrain = 16;
        Camera camera = 17;
        PresetPoint point = 18;
        UiControlGroup ui = 19;
        GlobalTimer timer = 20;
        // ??? = 21;
        StructureDefinition struct = 22;
        Path path = 23;
        // ???
        UnitTag unit_tag = 26;
        EntityDeploymentGroup deployment = 27;
    }
}
```

## Fields

### info
- Type: [`AssetInfo`](/docs/en/Types/AssetInfo.md)
- Metadata for this asset

### related
- Type: List\<[`AssetInfo`](/docs/en/Types/AssetInfo.md)>
- Metadata for related assets

### name
- Type: string
- Name of the asset

### type
- Type: Enum\<[`AssetType`](/docs/en/Types/AssetType.md)>
- The type of the asset

### content
- Type: oneof
- The content of the asset itself
