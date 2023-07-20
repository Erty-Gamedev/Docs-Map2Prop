---
title: RMF
layout: default
parent: Format Specifications
nav_order: 2
---

# RMF Format Specification
{: .no_toc }

An alternative to the MAP format which provides some more features such as saving VisGroups.
All data types uses little endian byte order.


<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

# Overall Structure

```c
typedef struct {
    float version;                      // File format version (typically 2.2)
    char[3] magic;                      // File format magic number
    int visgroup_count;                 // Number of VisGroups
    VisGroup[visgroup_count] visgroups; // VisGroups objects
    p_char[] cmapworld;                 // The string "CMapWorld" in ascii
    char[7] unkown1;
    int object_count;                   // Number of objects
    MapObject[object_count] objects;    // Map objects (Brush, Entity, Group)
    p_char[] worldspawn;                // The string "worldspawn" in ascii
    char[4] unknown2;
    int spawnflags;                     // Worldspawn spawnflags (not used)
    int kv_count;                       // Number of worldspawn's key-value pairs
    KeyValue[kv_count] keyvalues;       // Worldspawn's key-value pairs (properties)
    char[12] unknown3;
    int path_count;                     // Number of path objects
    Path[path_count] paths;             // Path objects (created with the Path tool)
    nt_char[8] docinfo;                 // The string "DOCINFO"
    float camera_version;               // Possibly version number of the camera data
    int activate_camera;                // Index of the activate camera
    int camera_count;                   // Number of camera objects
    Camera[camera_count];               // Camera objects
} Rmf;
```

The magic number is 3 bytes represented by the string `RMF` in ascii.

# Common Structures

## Color

```c
typedef struct {
    char[3] color;      // One byte each for red, green and blue channel
} Color;
```

## Vector

```c
typedef struct {
    float[3] vector;    // One float each for x, y and z component
} Vector;
```

## KeyValue

```c
typedef struct {
    p_char[] key;       // Key of the property
    p_char[] value;     // Value of the property
} KeyValue;
```

# VisGroup

```c
typedef struct {
    nt_char[128] name;      // VisGroup name
    Color color;            // Editor color of the VisGroup
    char unknown1;
    int visgroup_id;        // VisGroup's ID number
    _Bool visible;          // Whether the VisGroup is visible or not
    char[3] unknown2;
} VisGroup;
```

# Map Objects

All map objects starts with a length-prefixed string specifying its type.

## Brush (CMapSolid)

```c
typedef struct {
    p_char[] object_type;   // "CMapSolid" in the case of a brush object
    int visgroup_id;        // ID of the VisGroup the object belongs to
    Color color;            // Editor color of the object
    char[4] unknown1;
    int face_count;         // Number of faces (polygons) making up the brush
    Face[face_count]        // The brush's faces
} Brush;
```

### Face

```c
typedef struct {
    nt_char[256] texture_name;      // Name of the texture applied to the face
    char[4] unknown1;
    Vector right_axis;              // The texture's projected right axis
    float shift_x;                  // Horizontal shift of the texture
    Vector down_axis;               // The texture's projected down axis
    float shift_y;                  // Vertical shift of the texture
    float angle;                    // The angle of the applied rotation
    float scale_x;                  // Horizontal scale multiplier
    float scale_y;                  // Vertical scale multiplier
    char[16] unknown2;
    int vertex_count;               // Number of vertices in the face
    Vector[vertex_count] vertices;  // The vertices that make up the face
    Vector[3] plane_points;         // A triplet of points that define the face plane
} Face;
```

The `angle` value is what has *already* been applied to the face and is reflected in the `right_axis`
and `down_axis`. In other words, any texture projected along `right_axis` and `down_axis` will already
be rotated. You will mostly only use this to *undo* the rotation done to the texture.

## Entity (CMapEntity)

```c
typedef struct {
    p_char[] object_type;           // "CMapEntity" in the case of an entity object
    int visgroup_id;                // ID of the VisGroup the object belongs to
    Color color;                    // Editor color of the object
    int brush_count;                // Number of brushes tied to the entity
    Brush[brush_count] brushes;     // Brushes that are tied to the entity
    p_char[] classname;             // The entity's classname
    char[4] unknown1;
    int flags;
    int kv_count;                   // Number of entity's key-value pairs
    KeyValue[kv_count] keyvalues;   // Entity's key-value pairs (properties)
    char[14] unknown2;
    Vector origin;                  // The origin if it's a point entity
    char[4] unknown3;
} Entity;
```

## Group (CMapGroup)

```c
typedef struct {
    p_char[] object_type;       // "CMapGroup" in the case of a group object
    int visgroup_id;            // ID of the VisGroup the object belongs to
    Color color;                // Editor color of the object
    int object_count;           // Number of objects belonging to the group
    MapObject[object_count]     // The objects that make up the group
} Group;
```

# Path

Paths are placed using the [Path tool](https://twhl.info/wiki/page/Tutorial%3A_Intro_to_the_Tools_of_Hammer#_img:hamtut-ico-pat_inline_PATH_TOOL_(Shift+P))
in Hammer and offer an alternative to placing `path_` entities manually.

```c
typedef struct {
    nt_char[128] path_name;     // The base name for this path
    nt_char[128] classname;     // Typically path_corner or path_track
    int path_type;              // The direction of the path
    int node_count;             // Number of nodes in the path
    Node[node_count] nodes;     // The nodes that make up the path
} Path;
```

The `path_name` will be used as the base name for the nodes belonging to this path, i.e. for a path named
`my_path` each node will be named `my_path01`, `my_path02`, etc.

The path's direction or `path_type` can have one of three different values:<br>
`0`: One way (from first to last node and stops there).<br>
`1`: Circular (from first to last and back to first again, as an endless loop).<br>
`2`: Ping pong (from first to last and reverse direction back to first, in an endless loop).

## Node

```c
typedef struct {
    Vector position;                // The node's position in world coordinates
    int index;                      // The node's index in the path
    nt_char[128] name_override;     // Name to use instead of auto-generated one
    int kv_count;                   // Number of node's key-value pairs
    KeyValue[kv_count] keyvalues;   // Node's key-value pairs (properties)
} Node;
```

# Camera

```c
typedef struct {
    Vector eye_position;        // The position of the camera in world coordinates
    Vector lookat_position;     // The target position in world coordinates the camera will look at
} Camera;
```

# Sources
- [MESS](https://github.com/pwitvoet/mess/blob/master/MESS/Formats/RmfFormat.cs)
- [Valve Developer Community](https://developer.valvesoftware.com/wiki/RMF_(Rich_Map_Format))
