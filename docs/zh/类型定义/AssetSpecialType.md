# AssetSpecialType
表示资产的特殊类型。

## 类型定义
```proto
enum AssetSpecialType {
    UNKNOWN      = 0;
    DEFAULT      = 1;
    reserved 2 to 4;
    NODE_GRAPH   = 5;
    reserved 6 to 22;
    COMPOSITE    = 23;
    GLOBAL_TIMER = 24;
    CAMERA       = 25;
}
```

## 字段说明

### UNKNOWN
- 未知类型
- 非法值，不会出现在正常的文件中

### DEFAULT
- 默认类型（无特殊类型）
- 绝大多数时候你都会得到这个值

### NODE_GRAPH
- 节点图

### COMPOSITE
- 复合节点、服务器信号或结构体定义
- 其实每个信号和结构体只是定义了专门用来操作它们的特殊节点而已

### GLOBAL_TIMER
- 全局计时器

### CAMERA
- 主镜头配置
