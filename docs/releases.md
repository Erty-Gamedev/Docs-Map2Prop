---
title: Releases
layout: default
nav_order: 2
---

# Releases
<br />
[Latest (v1.1.0)](#goldsrc-map2prop-v110){: .btn .btn-green }

---

## GoldSrc Map2Prop v1.1.0

* Added support for OL (Worldcraft/Hammer/SvenCraft prefab library)
* Support for RMF versions 1.6 and 1.8

### Windows:<br>
[Download Map2Prop1.1.0.7z](https://github.com/Erty-Gamedev/GoldSrc-Map2Prop/releases/download/v1.1.0/Map2Prop1.1.0.7z){: .btn .btn-blue}

---

## GoldSrc Map2Prop v1.0.1

Minor patch
* Try to handle WAD files with missing drive letter from MAP wad list key (try first using the steam directory's drive letter and then the MAP file's drive letter)

### Windows:<br>
[Download Map2Prop1.0.1.7z](https://github.com/Erty-Gamedev/GoldSrc-Map2Prop/releases/download/v1.0.1/Map2Prop1.0.1.7z){: .btn .btn-purple}

## GoldSrc Map2Prop v1.0.0

Map2Prop Released!

### Changelog:

* Now with map compilation integration!
  * Using the `--mapcompile` argument it can now be used in a map compilation process to automatically produce models from func_map2prop entities and modify the MAP file to convert these to model displaying entities such as `cycler` or `env_sprite`.<br />
  **NOTE:** Make sure *Use Process Window* or *Wait for Termination* (or similar) is checked to ensure it finishes before the rest of the compilation process proceeds!
  ![Example advanced compile config](assets/images/mapcompile.png)
* Template models
  * No need to create hundreds different models for the same prop.
  The *Template Prop* (`parent_model`) key can be used to point to a func_map2prop entity whose model will be re-used
* The base mod folder will now also be checked for WADs if the mod folder was a SteamPipe folder such as _addon or _downloads
* config.ini, CLI arguments and FGD have been updated and might have incompatible changes
* Targetnames of func_map2prop entities are carried over to converted entities

### Windows:<br>
[Download Map2Prop1.0.0.7z](releases/Map2Prop1.0.0.7z){: .btn .btn-purple }
