# AssetCategory
> 此段落仍在编辑和测试中

表示资产的主要类别。

## 类型定义
```c#
public enum AssetCategory : byte {
    Special               = 0,  // 特殊类型
    Prefab                = 1,  // 预制体（元件）、玩家模板或角色模板
    Entity                = 2,  // 实体或造物
    Configuration         = 3,  // 配置信息
    // ???                = 4,
    Terrain               = 5,  // 地形
    // ???                = 6,
    // ???                = 7,
    UI                    = 8,  // 界面布局或交互控件
    PresetPoint           = 9,  // 预设点
    // ???
    Decoration            = 14, // 装饰物
    Structure             = 15, // 结构体
    // ???
    EntityDeploymentGroup = 18, // 实体布设组
    Path                  = 19, // 路径
    // ???
    UnitTag               = 23, // 单位标签
}
```

## 字段说明

### Special
- 特殊类型，请见 [`AssetSpecialType`](/docs/zh/类型定义/AssetSpecialType.md)
- 此字段的值为 0，通常会被省略，但也有发现样本存在此值为 0 的情况
- 因为 Protobuf 的标准规定当字段不存在时应视为该类型的默认值

### Configuration
- 配置信息
- 包含
  - 商店
  - 道具
  - 光源
  - 职业
  - 护盾
  - 技能
  - 技能资源
  - 单位状态
  - 环境配置
  - 扫描标签
  - *... 可能还有其他，目前样本数量不足*
