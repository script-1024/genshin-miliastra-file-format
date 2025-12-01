# AssetType
> 此段落仍在编辑和测试中

表示资产的具体类型。

## 类型定义
```c#
public enum AssetType : byte {
    Unknown               = 0,  // 未知类型
    Prefab                = 1,  // 预制体（元件）
    Creation              = 2,  // 造物
    Entity                = 3,  // 实体
    // ???                = 4,
    Terrain               = 5,  // 地形
    PresetPoint           = 6,  // 预设点
    UnitStatus            = 7,  // 单位状态
    Skill                 = 8,  // 技能
    EntityNodeGraph       = 9,  // 实体节点图
    BooleanFilter         = 10, // 布尔过滤器
    SkillNodeGraph        = 11, // 技能节点图
    CompositeNode         = 12, // 复合节点 (含监听信号、修改/拆分/拼装结构体)
    Camera                = 13, // 镜头
    Signal                = 14, // 信号 (发送信号、向服务器节点图发送信号)
    UIControl             = 15, // 交互控件
    SkillResource         = 16, // 技能资源
    // ???                = 17,
    Player                = 18, // 玩家模板
    Character             = 19, // 角色模板
    InterfaceLayout       = 20, // 界面布局
    UIControlGroup        = 21, // 界面控件组
    StatusNodeGraph       = 22, // 状态节点图
    ClassNodeGraph        = 23, // 职业节点图
    GlobalTimer           = 24, // 全局计时器
    // ???                = 25,
    Item                  = 26, // 道具
    // ???                = 27,
    Decoration            = 28, // 装饰物
    Structure             = 29, // 结构体
    Shop                  = 30, // 商店
    // ???
    Path                  = 38, // 路径
    Shield                = 39, // 护盾
    // ???
    EntityDeploymentGroup = 43, // 实体布设组
    UnitTag               = 44, // 单位标签
    ScanTag               = 45, // 扫描标签
    ItemNodeGraph         = 46, // 道具节点图
    IntegerFilter         = 47, // 整数过滤器
    LightSource           = 48, // 光源
    Environment           = 49, // 环境配置
}
```

> 别问我为什么看起来毫无规律，我也想问🫤
