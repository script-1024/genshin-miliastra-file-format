# AssetInfo
表示资产的元信息。

## 类型定义
```proto
message AssetInfo {
    AssetSpecialType special_type = 2;
    AssetCategory category = 3;
    uint32 guid = 4;
}
```

## 字段说明

### special_type
- 类型：枚举\<[`AssetSpecialType`](/docs/zh/类型定义/AssetSpecialType.md)>
- 资产的特殊类型
- 此字段通常被设为 `DEFAULT`
- 目前仅发现节点图、服务器信号、结构体定义、全局计时器和主镜头配置具有不同的值

### category
- 类型：枚举\<[`AssetCategory`](/docs/zh/类型定义/AssetCategory.md)>
- 资产的主要类别
- 大部分资产通过此字段区分类别
- 仅当此字段为 `SPECIAL` 时，`special_type` 才有意义
- 当此字段为 0 时可能被省略，具体可见[此处说明](/docs/zh/Protobuf%20简介.md#注意事项)，这么做是为了减小文件体积

### guid
- 类型：无符号整型
- 资产的全局唯一标识符
- 经测试发现可以乱填，只要保证同个对象的 GUID 在文件中的任何地方都相同就好
- 游戏在导入资产时会根据引用关系重新分配 GUID
- 游戏似乎总是从 `0x40000000`（1073741824）开始分配 GUID
