# AssetType
> This section is still being edited and tested.

Enum to specify the type of an asset.

## Definition
```proto
enum AssetType {
    UNKNOWN                 = 0;
    PREFAB                  = 1;
    CREATION                = 2;
    ENTITY                  = 3;
    // ???                  = 4;
    TERRAIN                 = 5;
    PRESET_POINT            = 6;
    UNIT_STATUS             = 7;
    SKILL                   = 8;
    ENTITY_NODE_GRAPH       = 9;
    BOOLEAN_FILTER          = 10;
    SKILL_NODE_GRAPH        = 11;
    COMPOSITE_NODE          = 12;
    CAMERA                  = 13;
    SIGNAL                  = 14;
    UI_CONTROL              = 15;
    SKILL_RESOURCE          = 16;
    // ???                  = 17;
    PLAYER                  = 18;
    CHARACTER               = 19;
    INTERFACE_LAYOUT        = 20;
    UI_CONTROL_GROUP        = 21;
    STATUS_NODE_GRAPH       = 22;
    CLASS_NODE_GRAPH        = 23;
    GLOBAL_TIMER            = 24;
    // ???                  = 25;
    ITEM                    = 26;
    // ???                  = 27;
    DECORATION              = 28;
    STRUCTURE               = 29;
    SHOP                    = 30;
    // ???
    PATH                    = 38;
    SHIELD                  = 39;
    // ???
    ENTITY_DEPLOYMENT_GROUP = 43;
    UNIT_TAG                = 44;
    SCAN_TAG                = 45;
    ITEM_NODE_GRAPH         = 46;
    INTEGER_FILTER          = 47;
    LIGHT_SOURCE            = 48;
    ENVIRONMENT             = 49;
}
```

> Don't ask why it looks so random, I want to know too 🫤
