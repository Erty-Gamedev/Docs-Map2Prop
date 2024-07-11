---
title: map2prop.fgd
layout: default
nav_order: 7
---

# map2prop.fgd

Add the `map2prop.fgd` to your map editor's game configuration to make use of the func_map2prop entity.

### Attributes:

* **Name (*targetname*)** - Sets a name that can be referenced by child objects using the *Template prop* key.
* **Exported model's name (*outname*)** - The name that will be used for the model file.
* **Exported model subfolder (*subdir*)** - The subfolder of the output directory the model and its assets will be placed in.
* **Gamma (default 1.8) (*gamma*)** - The value that will be used for the model's `$gamma` QC command. Increasing the value will make the model darker, and decreasing the value will make the model brighter.
* **Smoothing (*smoothing*)** - The angle threshold in degrees for which edges will be smooth-shaded. More fine-grained control can be achieved using `BEVEL` and `CLIPBEVEL` brushes.
* **Scale (*scale*)** - Sets the `$scale` QC command for the model.
* **Flags (*qc_flags*)** - Sets the value of the `$flags` QC command for the model.
* **Template prop (*parent_model*)** - Set a parent func_map2prop's *Name* here to use its model for this entity.
* **Export as its own model (*own_model*)** - Whether to export the prop as its own model or merge it with the worldspawn model. (NOTE: When using `--mapcompile` this keyvalue is ignored and all func_map2prop entities will always be exported as their own models).
* **Chrome (*chrome*)** - Whether to rename any textures with CHROME in the name to disable these receiving the chrome render mode by studiomdl.exe.
* **Classname after conversion (*convert_to*)** - The classname to convert this entity to when using `--mapcompile`. NOTE: One can use a classname not listed in the choices by simply turning off SmartEdit and typing in the classname as the value.
  * *cycler (0)*
  * *cycler_sprite (1)*
  * *env_sprite (2)*
  * *item_generic (3)*
  * *monster_furniture (4)*
  * *monster_generic (5)*

### Flags
* Disable (1) - If set, this prop will be removed from the converted map

---

## func_map2prop

```c
@SolidClass = func_map2prop : "Entity for Map2Prop to turn into a model" 
[
    spawnflags(flags) =
    [
        1 : "Disable" : 0
    ]

    targetname(string) : "Name"
    outname(string) : "Exported model's name"
    subdir(string) : "Exported model subfolder"
    gamma(string) : "Gamma (default 1.8)" : "1.8"
    smoothing(string) : "Smoothing threshold (0 disables)" : "60.0"
    scale(string) : "Scale" : "1.0"
    qc_flags(integer) : "Flags" : 0
    parent_model(string) : "Template prop"
    own_model(choices) : "Export as its own model" : 1 =
    [
        0: "No"
        1: "Yes"
    ]
    chrome(choices) : "Chrome setting override" : 0 =
    [
        0: "Default"
        1: "Rename chrome textures (disable chrome)"
    ]
    convert_to(choices) : "Classname after conversion" : 0 =
    [
        0: "cycler"
        1: "cycler_sprite"
        2: "env_sprite"
        3: "item_generic"
        4: "monster_furniture"
        5: "monster_generic"
    ]
]
```
