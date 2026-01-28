# AssetCategory
> This section is still being edited and tested.

Enum to describe the primary category of an asset

## Definition
```proto
enum AssetCategory {
    SPECIAL                 = 0;
    PREFAB                  = 1;  // Prefabs; Player/character templates
    ENTITY                  = 2;
    CONFIGURATION           = 3;
    reserved 4;
    TERRAIN                 = 5;
    reserved 6, 7;
    UI                      = 8;
    PRESET_POINT            = 9;
    reserved 10 to 13;
    DECORATION              = 14;
    STRUCTURE               = 15;
    reserved 16, 17;
    ENTITY_DEPLOYMENT_GROUP = 18;
    PATH                    = 19;
    reserved 20 to 22;
    UNIT_TAG                = 23;
}
```

## Fields

### SPECIAL
- Documented at [`AssetSpecialType`](/docs/en/Types/AssetSpecialType.md)
- This field is usually omitted, but in some samples, an explicit value of 0 has been observed.
- In Protobuf, an omitted field is interpreted as the default value—in this case, 0.

### CONFIGURATION
- Configuration information
- Includes:
  - Shop
  - Props
  - Lighting
  - Profession
  - Shield
  - Skills
  - Skill resources
  - Units
  - Environment
  - Label
  - *... There may be more that are missing, but more samples are needed.*
