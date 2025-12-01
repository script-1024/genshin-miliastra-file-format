# Asset
> 此段落仍在编辑和测试中

## 类型定义
```c#
public sealed class Asset {
    // id = 1, type = LENGTH
    public AssetInfo Info { get; set; }

    // id = 2, type= LENGTH
    public List<AssetInfo> RelatedInfo { get; set; }

    // id = 3, type = LENGTH
    public string Name { get; set; }

    // id = 5, type = VARINT
    public AssetType Type { get; set; }

    // 互斥结构
    // 以下元素同时只能存在一个
    // oneof {

        // id = 11, type = LENGTH
        // 预制体（元件）
        // 造物
        // 实体
        // 玩家模板
        // 角色模板

        // id = 13, type = LENGTH
        // 节点图

        // id = 14, type = LENGTH
        // 复合节点定义

        // id = 15, type = LENGTH
        // 商店
        // 道具
        // 光源
        // 职业
        // 护盾
        // 技能
        // 技能资源
        // 单位状态
        // 环境配置
        // 扫描标签

        // id = 16, type = LENGTH
        // 地形

        // id = 17, type = LENGTH
        // 镜头

        // id = 18, type = LENGTH
        // 预设点

        // id = 19, type = LENGTH
        // 界面布局
        // 交互控件

        // id = 20, type = LENGTH
        // 全局计时器

        // id = 22, type = LENGTH
        // 结构体定义

        // id = 23, type = LENGTH
        // 路径

        // id = 26, type = LENGTH
        // 单位标签

        // id = 27, type = LENGTH
        // 实体布设组

    // }
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
