# File structure

The most minimal plugin consists of at least 4 files.

+ [Lua file](#lua-file)
+ [Text File](#text-file)
+ [UIX File](#uix_file)
+ [plugin.json File](#plugin-json-file)

PolyPop will recognize plugins in either:

`C:\Users\%USERNAME%\PolyPop\`

Or by default (where plugins are automatically installed)

`%APPDATA%\PolyPop\`

```txt
├── PolyPop
│   ├── Plugins
|   │   ├── Example
|   │   │   ├── Example.lua
│   │   │   ├── Example.text
│   │   │   ├── Example.uix
│   │   │   ├── plugin.json
```

## Lua File

Contains the code ran inside the plugin

When PolyPop attaches this module, it automattically passes it's `self` object as `Instance`. Below outlines the methods Instance has:

### `Instance.properties(props)`

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
      - `ui`
        - `expand` - Whether this property is expanded or not
    - `Enum` - A drop down of elements to choose from
      - `elements` A table containing the elements to choose from
- `ui` - A table containing ui variables (these apply to all types
  - `visible` - Whether this propery is visible or not

### `Instance:onInit(obj)`

Called when a new instance of this module is created in PolyPop

### `Instance:onDelete()`

## Text File

Contains all descriptions of the file and all its properties. The file follows `xml` formatting.

When captioning properties they need to be delimited by (`_`) underscores

`Example.text`

```xml
<stringtable>
  <ID name="Self_ToolTip">Brief description of what the plugin does.</ID>
  <ID name="PropGroup_PropName_ToolTip">Brief description of what a property named `PropName` that is in a PropertyGroup named `PropGroup` does.</ID>
  <ID name="PropName_ToolTip">Brief description of what a property named `PropName` does.</ID>
  <ID name="EnumPropName_ToolTip">Brief description of the whole enum.</ID>
  <ID name="EnumPropName_EnumElementName_ToolTip">Brief description of a specific option in the enum.</ID>
</stringtable>
```

## UIX file

Used to define charactaristics of a module. The only required elements are `uix` with the `type` attribute and its child `name`.

```xml
<uix type="Source" index="[Subsources.Texture]">
  <add_menu_group>Example</add_menu_group>
  <category>Example</category>
  <cast_types>MeshModel</cast_types>
  <name>Example</name>
  <source_type></source_type>
  <target_type></target_type>
  <ui_name></ui_name>
  <developer_mode_only>true</developer_mode_only>
  <unique></unique>
  <user_creatable></user_creatable>
</uix>
```

### uix

The root node of the file, required.

#### type

`type` is a required attribute which specifies the type of instance that this creates. It can be one of the following types.

- `ActionStep`
  - Children used officially: `name`, `ui_name`, `user_creatable`
- `importer` - Special type for the 3D model importer.
  - Children used officially: `ext`, `import_type`, `name`, `source_type`
- `Layer`
  - Children used officially: `category`, `name`, `tooltip`
- `LayerGroup`
  - Children used officially: `category`, `name`, `scene_type`
- `Mod` - A modifier for some other instance, usually paired with `uix.index` in order to limit what it can modify.
  - Children used officially: `add_menu_group`, `affect`, `affects`, `dependencies`, `dependency`, `instanced`, `mod_type`, `name`, `parent_type`, `ui_name`
- `Output` - Output video feeds.
  - Children used officially: `group_name`, `name`, `unique`, `user_creatable`
- `PolyPopHost` - Used for connecting to a streaming service.
  - Children used officially: `name`, `server`
- `PolyPopObject`
  - Children used officially: `add_menu_group`, `cid`, `name`, `script`, `vst3_path`
- `Scene` - A scene, as expected.
  - Children used officially: `category`, `name`, `object_categories`, `tooltip`
- `Source` - Some data source like a 3D model, audio feed, webcam feed, hotkey, image, or video.
  - Children used officially: `add_menu_group`, `cast_types`, `category`, `developer_mode_only`, `name`, `source_type`, `unique`, `user_creatable`
- `Toy`
  - Children used officially: `category`, `developer_mode_only`, `instanced`, `name`, `tooltip`
- `Utility`
  - Children used officially: `group_name`, `name`
- `Wire` - For creating new wires from alerts to other things.
  - Children used officially: `action_label`, `name`, `source_type`, `target_cast_types`, `target_type`, `tooltip`, `ui_name`

#### index

`index` is an optional attribute which specifies what parent instances this can live under. This will add a `+` menu on the right-hand side of matched entries in the Library. For mods, it will add them to the `Mods`'s `+` menu in the properties view. The format is not super clear to me but here's the existing ones.

- Found on `Mod` types:
  - `[Mods.Toy.AreaEmitter]`, `[Mods.Toy.Entity]`, `[Mods.Toy.MeshEntity]`, `[Mods.Toy.NodeEmitter]`, `[Mods.Toy.Node]`, `[Mods.Toy.ParticleEmitter]`
  - `[Mods].Name` where `Name` is the instance's `name` field from the uix.
    - Examples: `[Mods].2D Text`, `[Mods].3D Object Set`, `[Mods].3D Screen Layer`
- Found on `PolyPopObject` types:
  - `[AudioFilters]`
  - `AppChannelPoints`, `ChannelPoints`, `ChatAlerts`, `CheerAlerts`, `SuperChatAlerts`, `Transition.Styles`, `VST3.Properties`
- Found on `Source` type (Crop and Filter):
  - `[Subsources.Texture]`

### action_label

### add_menu_group

This specifies the group (section between two horizontal rules) by name that this instance appears under the relevant Add (`+`) menu. You may specify any string but below are some official ones.

- `[VST3] mda`
- `Actions`
- `Alert Objects`
- `Animations`
- `Capture`
- `Dev`
- `File`
- `Physics`
- `Utilities`
- `Variance`
- `Web Alerts`

### affect

#### exclusive

Boolean type attribute.

### affects

### cast_types

### category

### cid

### dependencies

### dependency

### developer_mode_only

### ext

### group_name

### import_type

### instanced

### mod_type

### name

### object_categories

### parent_type

### scene_type

### script

### server

### source_type

### target_cast_types

### target_type

### tooltip

### ui_name

### unique

### user_creatable

### vst3_path

## plugin.json file

This is used to describe the plugin itself. It must be in the root folder of the plugin and must be present in order for PolyPop to identify this folder as containing a plugin.

`plugin.json`

```json
{
    "name": "Example",
    "author": "John Smith",
    "description": "Brief description of the plugin",
    "category": "Utilities",
    "url": "https://github.dev/JustinBacher/PolyPop-SDK-Documentation",
    "version": "1.0",
    "min_app_version": "1.0"
}
```
