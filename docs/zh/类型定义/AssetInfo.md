# AssetInfo
> 此段落仍在编辑和测试中

表示资产的元信息。

## 类型定义
```c#
public struct AssetInfo {
    // id = 2, type = VARINT
    public AssetSpecialType SpecialType { get; set; }

    // id = 3, type = VARINT
    public AssetCategory Category { get; set; }

    // id = 4, type = VARINT
    public Guid Guid { get; set; }
}
```

## 字段说明

### SpecialType
- 类型：枚举\<[`AssetSpecialType`](/docs/zh/类型定义/AssetSpecialType.md)>
- 资产的特殊类型
- 绝大多数时候此字段都被设为 `AssetSpecialType.Default`（也就是 1）
- 目前仅发现节点图、服务器信号、结构体定义和主镜头配置具有不同的值

### Category
- 类型：枚举\<[`AssetCategory`](/docs/zh/类型定义/AssetCategory.md)>
- 资产的主要类别
- 大部分资产通过此字段区分类别
- 仅当此字段为 `AssetCategory.Special`时（也就是 0），`SpecialType` 才有意义
- 当此字段为 0 时可能被省略，具体可见[此处说明](/docs/zh/Protobuf%20简介.md#注意事项)，这是为了减小文件体积所做的优化

### Guid
- 类型：`Guid`（其实就是 uint）
- 资产的全局唯一标识符
- 经测试发现可以乱填，只要保证同个对象的 GUID 在文件中的任何地方都相同就好
- 游戏在导入资产时会根据引用关系重新分配 GUID
- 游戏似乎总是从 `0x40000000`（1073741824）之后开始分配 GUID
