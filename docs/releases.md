---
title: Releases
layout: default
nav_order: 2
---

# Releases

<br>
[Latest (v0.9.1-beta)](#goldsrc-map2prop-v091-unchromed-beta){: .btn .btn-green }

---

## GoldSrc Map2Prop v0.9.1 Unchromed <span class="label label-blue">Beta</span>

### Changelog:

* Fixed issues related to floating-point precision
* Option to disable chrome render mode for textures with `CHROME` in the name (renames these textures prior to compilation)
  * Can either be set per-entity using the `chrome = 1` keyvalue,
  * or enabled globally using the `--renamechrome` CLI argument or setting `rename chrome = yes` in config.ini

### Windows:<br>
[Download Map2Prop0.9.1.7z](releases/Map2Prop0.9.1.7z){: .btn .btn-blue }

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
