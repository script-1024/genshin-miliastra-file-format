# Asset
> 此段落仍在编辑和测试中

## 类型定义
```c#
public sealed class Asset {
    // id = 1, type = LENGTH
    public AssetInfo Info { get; set; }

    // id = 2, type= LENGTH
    public List<AssetInfo>? RelatedInfo { get; set; }

    // id = 3, type = LENGTH
    public string Name { get; set; }

    // id = 5, type = VARINT
    public AssetType Type { get; set; }

    // id = 13, type = LENGTH
    // 节点图定义，待研究

    // id = 19, type = LENGTH
    // 界面控件组定义，待研究
}
```

## 字段说明

### Info
- 类型：[`AssetInfo`](/docs/zh/类型定义/AssetInfo.md)
- 表示此资产的元信息

### RelatedInfo
- 类型：列表\<[`AssetInfo`](/docs/zh/类型定义/AssetInfo.md)>
- 表示关联资产的元信息

### Name
- 类型：字符串
- 资产名称

### Type
- 类型：枚举\<[`AssetType`](/docs/zh/类型定义/AssetType.md)>
- 表示资产具体的类型
