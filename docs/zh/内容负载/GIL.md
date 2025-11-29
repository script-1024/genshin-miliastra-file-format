# GIL - 关卡文件
> 此段落仍在编辑和测试中

在「我的奇域」中创建的关卡，其中包含各式各样的关卡数据，给本项目的工作进展带来严重阻碍 💀

## 类型定义
```c#
public partial class GilFile : GiFile {
    public override GiFileType Type => GiFileType.Gil;

    // id = 2, type = LENGTH
    public string LevelName;

    // id = 3
    // 未知字段

    // id = 4, type = LENGTH
    public List<Component> Components;

    // id = 5, type = LENGTH
    public List<Entity> Entities;

    // id = 6, type = LENGTH
    public List<Category> Categories;

    // id = 7, type = LENGTH
    public List<Terrain> Terrains;

    // id = 8
    // 似乎也是元件数据? 还需要进一步研究

    // id = 9, type = LENGTH
    public UIControlGroup UIControlGroup;

    // id = 10, type = LENGTH
    public NodeGraph NodeGraph;
    
    // id = 11, type = LENGTH
    public LevelSettings LevelSettings;

    // id = 12
    // 未知字段

    // id = 14
    // 未知字段

    // id = 15
    // 似乎是背包模板、环境配置、职业和技能相关数据？
    
    // id = 16
    // 似乎是技能动画和事件轨道

    // id = 17
    // 未知字段

    // id = 18, type = LENGTH
    public List<Camera> CameraTemplates;

    // id = 21
    // 未知字段

    // id = 22, type = LENGTH
    public LevelFlags LevelFlags;

    // id = 23
    // 未知字段

    // id = 25, type = LENGTH
    public PeripheralSystem PeripheralSystem;

    // id = 27, type = LENGTH
    public List<Component> Decorations;

    // id= 29， type = LENGTH
    public EditorInfo EditorInfo;

    // id = 30
    // 未知字段

    // id = 31
    // 未知字段

    // id = 32
    // 未知字段

    // id = 33
    // 未知字段

    // id = 36
    // 似乎用于保存多语言文本配置

    // id = 37
    // 未知字段

    // id = 38
    // 未知字段
}
```

## 字段说明

### LevelName
- 类型：字符串
- 关卡名称

### Components
- 类型：列表
- 玩家和元件模板

### Entities
- 类型：列表
- 关卡内布设的实体

### Categories
- 类型：列表
- 分类页签
- 关卡配置杂项

### Terrains
- 类型：列表
- 地形

### UIControlGroup
- 类型：复合结构
- 包含所有界面控件组元件

### NodeGraph
- 类型：复合结构
- 包含所有服务器节点图、客户端节点图、自定义节点图、信号等

### LevelSettings
- 类型：复合结构
- 包含所有关卡设置信息（阵营、预设点等）

### CameraTemplates
- 类型：列表
- 镜头模板

### LevelFlags
- 类型：复合结构
- 包含关卡的各种功能旗帜开关

### PeripheralSystem
- 类型：复合结构
- 外围系统数据（计分项、成就、排行榜）

### Decorations
- 类型：列表
- 元件装饰物列表

### EditorInfo
- 类型：复合结构
- 记录千星沙箱编辑器的一些信息（应该不太重要）
