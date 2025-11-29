# AssetSpecialType
> 此段落仍在编辑和测试中

表示资产的特殊类型。

## 类型定义
```c#
public enum AssetSpecialType : byte {
    Unknown   = 0,
    Default   = 1,
    NodeGraph = 5,
    Composite = 23,
    Camera    = 25,
}
```

## 字段说明

### Unknown
- 未知类型
- 非法值，不会出现在正常的文件中

### Default
- 默认类型（无特殊类型）
- 绝大多数时候你都会得到这个值

### NodeGraph
- 节点图

### Composite
- 复合节点、服务器信号或结构体定义
- 其实每个信号和结构体只是定义了专门用来操作它们的特殊节点而已

### Camera
- 主镜头配置
