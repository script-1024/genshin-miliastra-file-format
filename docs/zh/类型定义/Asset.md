# Asset
> 此段落仍在编辑和测试中

## 类型定义
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

## 字段说明

### info
- 类型：[`AssetInfo`](/docs/zh/类型定义/AssetInfo.md)
- 表示此资产的元信息

### related
- 类型：列表\<[`AssetInfo`](/docs/zh/类型定义/AssetInfo.md)>
- 表示关联资产的元信息

### name
- 类型：字符串
- 资产名称

### type
- 类型：枚举\<[`AssetType`](/docs/zh/类型定义/AssetType.md)>
- 表示资产具体的类型

### content
- 类型：互斥结构
- 表示资产内容
