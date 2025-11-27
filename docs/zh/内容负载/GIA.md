# GIA - 资产文件
> 此段落仍在编辑和测试中

透过「资产导入导出」功能生成的文件，通常包含一个或多个由玩家勾选导出的资产定义。

## 类型定义
```c#
public partial class GiaFile : GiFile {
    public override GiFileType Type => GiFileType.Gia;

    // id = 1, type = LENGTH
    public IList<Asset>? Assets;
    
    // id = 2, type = LENGTH
    public IList<Asset>? DependentAssets;
    
    // id = 3, type = LENGTH
    public string? ExportInfo;
}
```

## 字段说明

### Assets
- 类型：列表
- 一个或多个资产定义对象
- 通常是玩家在「资产导入导出界面」中显式导出的元件

### DependentAssets
- 类型：列表
- 依赖的资产对象，此项可能不存在
- 通常是那些在导出时没被玩家选中，但其他组件必须依赖它才能运作的元件

### ExportInfo
- 类型：字符串
- 导出信息
- 游戏似乎不会校验此字段的内容，即使乱填或不存在也不影响加载
- 默认格式是 `{玩家UID}-{导出时间戳}-{文件GUID}-\{导出文件名称}.gia`
