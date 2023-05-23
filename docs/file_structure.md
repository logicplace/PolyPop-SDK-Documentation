# File structure

The most minimal plugin consists of at least 4 files. 

+ [Lua file](#Lua-File)
+ [Text File](#Text-File)
+ [UIX File](#UIX-File) 

PolyPop will recognize plugins in either:
`C:\Users\%USERNAME%\PolyPop\`
Or by default (where it automatically installs plugins)
`%APPDATA%\PolyPop\`

    ├── PolyPop
    │   ├── Plugins
    |   │   ├── Example
    |   │   │   ├── Example.lua
    │   │   │   ├── Example.text
    │   │   │   ├── Example.uix
    │   │   │   ├── Plugin.json

# Lua File
Contains the code ran inside the plugin

When PolyPop attaches this module, it automattically passes it's `self` object as `Instance`. Below outlines the methods Instance has:

## `Instance.properties(props)`
Used to create properties within the module.
- `props` - A table of properties to be used. For example: `{ {name="Example", type="Text"} }`
  - `name` - The name of the property must be one word and uses PascalCase to separate words
  - `type` - The type of the property. Possible types are:
    - `Text` - A text type

## `Instance:onInit(obj)`
Called when a new instance of this module is created in PolyPop
