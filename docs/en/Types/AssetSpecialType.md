# AssetSpecialType
Enum for special types of assets

## Definition
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

## Types

### UNKNOWN
- Should never appear in real files

### DEFAULT
- Most common value

### NODE_GRAPH

### COMPOSITE
- Composite node; signal or structure definition
- Each signal/structure defines a special node used to operate on them

### GLOBAL_TIMER

### CAMERA
