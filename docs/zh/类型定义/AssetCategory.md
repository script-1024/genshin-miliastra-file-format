# AssetCategory
> 此段落仍在编辑和测试中

表示资产的主要类别。

## 类型定义
```proto
enum AssetCategory {
    SPECIAL                 = 0;  // 特殊类型
    PREFAB                  = 1;  // 预制体（元件）、玩家模板或角色模板
    ENTITY                  = 2;  // 实体或造物
    CONFIGURATION           = 3;  // 配置信息
    reserved 4;
    TERRAIN                 = 5;  // 地形
    reserved 6, 7;
    UI                      = 8;  // 界面布局或交互控件
    PRESET_POINT            = 9;  // 预设点
    reserved 10 to 13;
    DECORATION              = 14; // 装饰物
    STRUCTURE               = 15; // 结构体
    reserved 16, 17;
    ENTITY_DEPLOYMENT_GROUP = 18; // 实体布设组
    PATH                    = 19; // 路径
    reserved 20 to 22;
    UNIT_TAG                = 23; // 单位标签
}
```

## 字段说明

### SPECIAL
- 特殊类型，请见 [`AssetSpecialType`](/docs/zh/类型定义/AssetSpecialType.md)
- 此字段的值为 0，通常会被省略，但也有发现样本存在此值为 0 的情况
- 因为 Protobuf 的标准规定当字段缺省时应视为该类型的默认值

### CONFIGURATION
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
  - *... 可能存在未列出的项目，但目前样本不足*
