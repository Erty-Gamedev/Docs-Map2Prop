---
title: Tool Textures
layout: default
nav_order: 4
---

# Tool Textures

Certain textures that can be found in either halflife.wad or zhlt.wad have special properties when used with Map2Prop. Any brushes with these textures will be removed after processing.

---

## NULL

Just as with map compile tools, any faces with NULL texture will be stripped out of the mesh.<br />
This behaviour is shared with all other tool texture that are not listed below.

## BEVEL / CLIPBEVEL

All vertics within the volume of a brush covered in BEVEL texture will be smooth-shaded.

Meanwhile all vertices within the volume of a CLIPBEVEL brush will be flat-shaded.

## BOUNDINGBOX

Used to set the values for the `$bbox` QC command.

## CLIP

Similar to BOUNDINGBOX but for the `$cbox` QC command. Useful for manually setting the model's Clipping Box, for example in case the model compiler gets it wrong and the model is culled from rendering when it shouldn't be.

## CONTENTWATER

Any brushes with at least one face textured with CONTENTWATER will have all its faces duplicated and flipped, essentially turning off backface culling.
The faces with CONTENTWATER will be stripped out.

## ORIGIN
The center of a brush completely covered in this texture will be used as the model's origin point.
