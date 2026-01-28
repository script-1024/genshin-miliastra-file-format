# GIA - Asset information
Files generated via the "Asset Import/Export" function usually contain one or more asset definitions that the user
may select to export.

## Definition
```proto
message GiaFile {
    repeated Asset assets = 1;
    repeated Asset related = 2;
    string export_info = 3;
}
```

## Fields

### assets
- Type: List\<[Asset](/docs/en/Types/Asset.md)>
- One or more asset definition messages
- Players select which assets to export in the "Asset Import/Export" interface

### related
- Type: List\<[Asset](/docs/en/Types/Asset.md)>
- List of related assets. This field may not be present.
- Assets which are depended on and cannot be independently exported (such as decorations)

### export_info
- Type: string
- Export information
- The game doesn't seem to validate the content of this field. Filling the field randomly or omitting it entirely 
doesn't affect loading.
- The default format is `{player UID}-{export timestamp}-{GUID}-{file name}.gia`
