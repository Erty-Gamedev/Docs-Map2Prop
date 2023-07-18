---
title: WAD3
layout: default
parent: Format Specifications
nav_order: 5
---

# WAD3 Format Specification
{: .no_toc }

Derived from Quake's WAD2 format.
All data types uses little endian byte order.

After the format's header there are `num_dirs` directory entries that contains data about all the files within the WAD3 archive, as well as their position within the file.

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

# Header

```c
typedef struct {
    char[4] magic;     // File format magic number
    int num_dirs;      // Number of Directory entries
    int dir_offset;    // Offset from the WAD3 data's beginning for first Directory entry
} Header;
```

The magic number is 4 bytes represented by the string `WAD3` in ascii.

# Directory Entry

```c
typedef struct {
    int entry_offset;           // Offset from the beginning of the WAD3 data
    int disk_size;              // The entry's size in the archive in bytes
    int entry_size;             // The entry's uncompressed size
    char file_type;             // File type of the entry
    _Bool compressed;           // Whether the file was compressed
    short padding;
    nt_string[16] texture_name  // Null-terminated texture name
} DirEntry;
```

The file entries archived in the WAD3's directory are described using an array of DirEntry structures.

## File types

The WAD3 format can store up to 256 different entry types, but only three are actually supported in GoldSrc:
* [qpic (0x42)](#qpic-image): A simple image of any size.
* miptex (0x43): World texture with dimensions that are multiple-of-16 and 4 mipmaps. This is the typical entry type.
* font (0x45): Fixed-height font for 256 ascii characters.

# File Entry

The description of the files within the WAD3 archive varies depending on its file type:

## Qpic Image

A simple image of any size. I'm unsure what this is used for.

```c
typedef struct {
    int width, height;
    char[height][width] data;
    short colors_used;
    char[colors_used][3] palette;
} QpicT;
```

## Miptex Image

This is the file type used by world textures and is the typical type of file you find in WAD3 archives.
The structure is similar to what's used to describe textures in the BSP format.

```c
// Image structure used by each mip level
typedef struct {
    char[width][height] data;         // Raw image data. Each byte points to an index in the palette
} MipImage;

// Color palette
typedef struct {
    char[256][3] colors;             // 256 triples of bytes (RGB)
} Palette;

// Texture structure
typedef struct {
    nt_string[16] texture_name;      // Null-terminated texture name
    u_int width, height;             // Dimensions of the texture (must be divisible by 16)
    u_int[4] mip_offsets;            // Offset from start of texture file to each mipmap level's image
    MipImage[4] mip_images;          // One MipImage for each mipmap level
    short padding;
    Palette[width][height] palette    // The color palette for the mipmaps
} MipTex;

```

## Font

Fixed-height font.

```c
typedef struct {
    short startoffset;
    short charwidth;
} CharInfo;

typedef struct {
    int width, height;
    int row_count;
    int row_height;
    CharInfo[256] font_info;
    char[height][width] data;
    short colors_used;
    char[colors_used][3] palette;
} Font;
```

# Sources
- [The hlbsp Project](https://hlbsp.sourceforge.net/index.php?content=waddef)
- [Valve Developer Community](https://developer.valvesoftware.com/wiki/WAD)
