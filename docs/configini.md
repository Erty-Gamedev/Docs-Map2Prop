---
title: config.ini
layout: default
nav_order: 5
---

# config.ini

The `config.ini` file allows customizing various options for the application that will be used by default.

This is where you can provide a path to `studiomdl.exe` which will enable the use of `autocompile` to automatically compile the .qc into a GoldSrc .mdl file.

Game configs can be set up with paths to your game and mod installs and the application will be able to look in these directories for any .wad packages to attempt to extract textures from. The `wad list` option can be used to list specific .wad packages to prioritize in this task.

---

## Example config.ini

```ini
[default]
smoothing threshold = 60.0
rename chrome = no
output directory = 
steam directory = C:\Program Files (x86)\Steam
game config = halflife
studiomdl = %(steam directory)s\steamapps\common\Sven Co-op SDK\modelling\studiomdl.exe
autocompile = yes
timeout = 60.0
autoexit = no
wad cache = 15
wad list = 
;Example wad list:
;wad list = %(steam directory)s\steamapps\common\Half-Life\valve\halflife.wad,
;           %(steam directory)s\steamapps\common\Half-Life\valve\liquids.wad,

[halflife]
game = Half-Life
mod = valve

[svencoop]
game = Sven Co-op
mod = svencoop

[cstrike]
game = Half-Life
mod = cstrike
```
