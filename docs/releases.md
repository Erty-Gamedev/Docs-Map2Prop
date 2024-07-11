---
title: Releases
layout: default
nav_order: 2
---

# Releases
<br />
[Latest (v1.0.0)](#goldsrc-map2prop-v100){: .btn .btn-green }

---

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
[Download Map2Prop1.0.0.7z](releases/Map2Prop1.0.0.7z){: .btn .btn-blue }

---

## GoldSrc Map2Prop v0.9.1 Unchromed <span class="label label-blue">Beta</span>

### Changelog:

* Fixed issues related to floating-point precision
* Option to disable chrome render mode for textures with `CHROME` in the name (renames these textures prior to compilation)
  * Can either be set per-entity using the `chrome = 1` keyvalue,
  * or enabled globally using the `--renamechrome` CLI argument or setting `rename chrome = yes` in config.ini

### Windows:<br>
[Download Map2Prop0.9.1.7z](releases/Map2Prop0.9.1.7z){: .btn .btn-purple }

---

## GoldSrc Map2Prop v0.9.0 Toolfaced <span class="label label-blue">Beta</span>

### Changelog:

* Implemented handling of various tool textures
  * `BOUNDINGBOX` can be used to manually set the `$bbox` QC command
  * `BEVEL` can set volumes within which all vertices are fully smooth-shaded
  * `CLIP` can be used to manually set the `$cbox` QC command
  * `CLIPBEVEL` can set volumes within which all vertices are fully flat-shaded
  * Any brushes with a `CONTENTWATER` face will duplicate and invert all faces
  * An `ORIGIN` brush can be used to set a model's origin
* Added a feature to read `func_map2prop` solid entities along with a FGD defining this entity
  * `func_map2prop` can define objects that will compile as separate model files
  * The entity can also configure settings such as smoothing thresholds, rotation, scaling and gamma per object

### Windows:<br>
[Download Map2Prop0.9.0.7z](releases/Map2Prop0.9.0.7z){: .btn .btn-purple }

---

## GoldSrc Map2Prop v0.8.6 <span class="label label-blue">Beta</span>

### Changelog:

* Fixed bug causing failure to extract textures when converting from MAP

### Windows:<br>
[Download Map2Prop0.8.6.7z](releases/Map2Prop0.8.6.7z){: .btn .btn-purple }

---

## GoldSrc Map2Prop v0.8.5 MapReader <span class="label label-blue">Beta</span>

### Changelog:

* Added support for converting MAP files
* Fixed issue of reading JMF files with Quake III/Volatile curves (simply ignores these)

### Windows:<br>
[Download Map2Prop0.8.5.7z](releases/Map2Prop0.8.5.7z){: .btn .btn-purple }

---

## GoldSrc Map2Prop v0.8.4 <span class="label label-blue">Beta</span>

### Changelog:

* Added support for JMF version 122 (J.A.C.K December 2023 update)

### Windows:<br>
[Download Map2Prop0.8.4.7z](releases/Map2Prop0.8.4.7z){: .btn .btn-purple }

---

## GoldSrc Map2Prop v0.8.3 <span class="label label-blue">Beta</span>

### Changelog:

* Fix for issue where junk bytes after texture name were attempted decoded as ASCII
* ValueErrors should now halt the program and show the error message instead of instantly exiting

### Windows:<br>
[Download Map2Prop0.8.3.7z](releases/Map2Prop0.8.3.7z){: .btn .btn-purple }

---

## GoldSrc Map2Prop v0.8.2 Nompy <span class="label label-blue">Beta</span>

### Changelog:

* Removed Numpy dependency (smaller executable)
* Fix bug when reading .wad archives for .obj format

### Windows:<br>
[Download Map2Prop0.8.2.7z](releases/Map2Prop0.8.2.7z){: .btn .btn-purple }

---

## GoldSrc Map2Prop v0.8.0 Neonymous <span class="label label-blue">Beta</span>

### Changelog:

* Release public beta of GoldSrc Map2Prop

### Windows:<br>
[Download Map2Prop0.8.0.7z](releases/Map2Prop0.8.0.7z){: .btn .btn-purple }

---
