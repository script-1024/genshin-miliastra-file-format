# GIA - 资产文件
透过「资产导入导出」功能生成的文件，通常包含一个或多个由玩家勾选导出的资产定义。

## 类型定义
```proto
message GiaFile {
    repeated Asset assets = 1;
    repeated Asset related = 2;
    string export_info = 3;
}
```

## 字段说明

### assets
- 类型：列表\<[Asset](/docs/zh/类型定义/Asset.md)>
- 一个或多个资产定义对象
- 玩家在「资产导入导出界面」选中导出的资产

### related
- 类型：列表\<[Asset](/docs/zh/类型定义/Asset.md)>
- 关联资产列表，此项可能不存在
- 被其他模块依赖、无法单独导出的资产（比如装饰物）

### export_info
- 类型：字符串
- 导出信息
- 游戏似乎不会校验此字段的内容，即使乱填或省略也不影响加载
- 默认格式是 `{玩家UID}-{导出时间戳}-{文件GUID}-\{导出文件名称}.gia`
