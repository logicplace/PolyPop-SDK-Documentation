# File structure

The most minimal plugin consists of at least 4 files. 

+ [Lua file](#lua_file)
+ [Text File](#text_file)
+ [UIX File](#uix_file) 
+ [plugin.json File](#plugin_json_file) 

PolyPop will recognize plugins in either:

`C:\Users\%USERNAME%\PolyPop\`

Or by default (where plugins are automatically installed)

`%APPDATA%\PolyPop\`

    ├── PolyPop
    │   ├── Plugins
    |   │   ├── Example
    |   │   │   ├── Example.lua
    │   │   │   ├── Example.text
    │   │   │   ├── Example.uix
    │   │   │   ├── Plugin.json

# Lua File <a name="lua_file"></a>
Contains the code ran inside the plugin

When PolyPop attaches this module, it automattically passes it's `self` object as `Instance`. Below outlines the methods Instance has:

## `Instance.properties(props)`
Used to create properties within the module.
- `props` - A table of properties to be used. For example: `{ {name="Example", type="Text"} }`
  - `name` - The name of the property must be one word and uses PascalCase to separate words
  - `type` - The type of the property. Possible types are:
    - `Text` - A text type
      - `onUpdate` - Name of the function to call when the field is changed
    - `Int` - Integer type
      - `onUpdate` - Name of the function to call when the field is changed
      - `range` - A table containing the the `min` and `max` values *(ie: `{min=0, max=100}`)*
      - `ui` - A table containing ui variables
        - `easing` - Where the slider should ease to *(ie: `ui={easing=5}`)*
        - `step` - How much one tick of the slider should increase/decrease the value by
    - `Real` - Floating point type
      - `onUpdate` - Name of the function to call when the field is changed
      - `range` - A table containing the the `min` and `max` values *(ie: `{min=0, max=100}`)
      - `ui` - A table containing ui variables (these are specific to `Real` types
        - `easing` - Where the slider should ease to *(ie: `ui={easing=5}`)*
        - `step` - How much one tick of the slider should increase/decrease the value by
    - `Bool` - Boolean type
      - `onUpdate` - Name of the function to call when the field is changed
    - `Action` - Button type (there is no on-press or on-update for this type, the name must match the function
    - `ObjectSet` - An object set is explained more in [Object Sets](object-sets.md)
      - `set_types` - A table containing:
        - `type` - The type of the object(s)
        - `index` - The index of the object(s)
    - `PropertyGroup` - This can be used to group properties
      - `items` - A table of properties.
    - `Enum` - A drop down of elements to choose from
      - `elements` A table containing the elements to choose from
- `ui` - A table containing ui variables (these apply to all types
  - `

### `Instance:onInit(obj)`
Called when a new instance of this module is created in PolyPop

### `Instance:onDelete()`

# Text File <a name="text_file"></a>
Contains all descriptions of the file and all it's properties. The file follows `xml formatting.

When captioning properties they need to be delimited by (`_`) underscores

`Example.text`

    <stringtable>
      <ID name="Self_ToolTip">Brief description of what the plugin does.</ID>
      <ID name="PropGroup_PropName_ToolTip">Brief description of what a property named `PropName` that is in a PropertyGroup named `PropGroup` does.</ID>
      <ID name="PropName_ToolTip">Brief description of what a property named `PropName` does.</ID>
    </stringtable>      
    
## UIX file <a name="uix_file"></a>
Used to define charactaristics of a module

`Example.uix`

    <uix type="Source">
      <name>Example</name>
    </uix>
    
## plugin.json file <a name="plugin_json_file"></a>
This is used to describe the plugin itself. It must be in the root folder of the plugin

`plugin.json`

    {
        "name": "Example",
        "author": "John Smith",
        "description": "Brief description of the plugin",
        "category": "Utilities",
        "url": "https://github.dev/JustinBacher/PolyPop-SDK-Documentation",
        "version": "1.0",
        "min_app_version": "1.0"
    }
