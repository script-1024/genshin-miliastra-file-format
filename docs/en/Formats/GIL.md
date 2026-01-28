# GIL - Level information
> This section is still being edited and tested.

Stores the levels generated in "My Miliastra", containing a wide variety of data. This is seriously holding back the 
reversal process 💀

## Definition
```c#
public partial class GilFile : GiFile {
    public override GiFileType Type => GiFileType.Gil;

    // id = 2, type = LENGTH
    public string LevelName;

    // id = 3
    // Unknown

    // id = 4, type = LENGTH
    public List<Component> Components;

    // id = 5, type = LENGTH
    public List<Entity> Entities;

    // id = 6, type = LENGTH
    public List<Category> Categories;

    // id = 7, type = LENGTH
    public List<Terrain> Terrains;

    // id = 8
    // Appears to also be component data? More investigation needed

    // id = 9, type = LENGTH
    public UIControlGroup UIControlGroup;

    // id = 10, type = LENGTH
    public NodeGraph NodeGraph;
    
    // id = 11, type = LENGTH
    public LevelSettings LevelSettings;

    // id = 12
    // Unknown

    // id = 14
    // Unknown

    // id = 15
    // Appears to be data related to environment settings, professions, and skills?
    
    // id = 16
    // Appears to be skill animations and event information

    // id = 17
    // Unknown

    // id = 18, type = LENGTH
    public List<Camera> CameraTemplates;

    // id = 21
    // Unknown

    // id = 22, type = LENGTH
    public LevelFlags LevelFlags;

    // id = 23
    // Unknown

    // id = 25, type = LENGTH
    public PeripheralSystem PeripheralSystem;

    // id = 27, type = LENGTH
    public List<Component> Decorations;

    // id= 29， type = LENGTH
    public EditorInfo EditorInfo;

    // id = 30
    // Unknown

    // id = 31
    // Unknown

    // id = 32
    // Unknown

    // id = 33
    // Unknown

    // id = 36
    // Appears to be localization data

    // id = 37
    // Unknown

    // id = 38
    // Unknown
}
```

## Fields

### LevelName
- Type: string
- The name of the level

### Components
- Type: List
- A list of player and component templates

### Entities
- Type: List
- A list of entities within the level

### Categories
- Type: List
- A list of categories the level belongs to

### Terrains
- Type: List
- Terrain data

### UIControlGroup
- Type: message
- Includes all UIControlGroup elements

### NodeGraph
- Type: message
- Includes all server, client, and custom node graphs, signals, etc.

### LevelSettings
- Type: message
- Includes all level settings, such as teams, spawn points, etc.

### CameraTemplates
- Type: List

### LevelFlags
- Type: message
- Contains various flags for the level

### PeripheralSystem
- Type: message
- Contains information on external systems, such as achievements and leaderboards.

### Decorations
- Type: List
- List of components and decorations

### EditorInfo
- Type: message
- Contains some information about the Miliastra editor. Probably not very important.
