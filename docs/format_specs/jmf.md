---
title: JMF
layout: default
parent: Format Specifications
nav_order: 3
---

# JMF Format Specification
{: .no_toc }

J.A.C.K Map Format. Similar to the RMF format but supports objects being part of multiple VisGroups.
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
    char[4] magic;                      // File format magic number
    char[4] unknown;                    // I'm unsure what this is. In all tests it came up as 0x79000000
    int ep_count;                       // Number of recent export paths
    pint_char[ep_count] export_paths;   // Recent export paths
    int group_count;                    // Number of groups in the map
    Group[group_count] groups;          // Group objects
    int visgroup_count;                 // Number of VisGroups
    VisGroup[visgroup_count] visgroups; // VisGroups objects
    Vector cordon_min;                  // Minimum corner of the Cordon box
    Vector cordon_max;                  // Maximum corner of the Cordon box
    int camera_count;                   // Number of Camera objects
    Camera[camera_count] cameras;       // Camera objects
    int path_count;                     // Number of path objects
    Path[path_count] paths;             // Path objects (created with the Path tool)
    Entity[] entities;                  // All entities including worldspawn
} Jmf;
```

The magic number is 4 bytes represented by the string `JHMF` in ascii.
This likely reflects J.A.C.K's old name which was Jackhammer.

All world brushes are stored within the worldspawn entity. The `entities` array is read until the end of file.

# Common Structures

## Color

```c
typedef struct {
    char[4] color;      // One byte each for red, green, blue and alpha channel
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
    pint_char[] key;    // Key of the property
    pint_char[] value;  // Value of the property
} KeyValue;
```

# Group

```c
typedef struct {
    int group_id;           // The ID number of this group
    int group_parent_id;    // ID of the group this group is nested within
    int flags;              // Editor flags
    int count;              // Number of objects in the group
    Color color;            // Editor color of the object
} Group;
```

# VisGroup

```c
typedef struct {
    pint_char[] name;   // VisGroup name
    int visgroup_id;    // VisGroup's ID number
    Color color;        // Editor color of the VisGroup
    _Bool visible;      // Whether the VisGroup is visible or not
} VisGroup;
```

# Camera

```c
typedef struct {
    Vector eye_position;        // The position of the camera in world coordinates
    Vector lookat_position;     // The target position in world coordinates the camera will look at
    int flags;                  // Editor flags (bit 0x02 flags whether it's selected)
    Color color;                // Editor color of the Camera
} Camera;
```

# Path

Paths are placed using the Path tool in J.A.C.K and offer an alternative to placing `path_` entities manually. It works similar to the Path tool in Hammer although can offer a "preview" in the 3D viewport of a camera travelling along the path with the speed specified by each node. One can read more about this in the [J.A.C.K VDKManual](https://store.steampowered.com/manual/496450).

```c
typedef struct {
    pint_char[] classname;      // Typically path_corner or path_track
    pint_char[] path_name;      // The base name for this path
    int path_type;              // The direction of the path
    int unknown;
    Color color;                // Editor color of the Path
    int node_count;             // Number of nodes in the path
    Node[node_count] nodes;     // The nodes that make up the path
} Path;
```

The `path_name` will be used as the base name for the nodes belonging to this path, i.e. for a path named
`my_path` each node will be named `my_path`, `my_path_1`, etc.

The path's direction or `path_type` can have one of three different values:<br>
`0`: One way (from first to last node and stops there).<br>
`1`: Circular (from first to last and back to first again, as an endless loop).<br>
`2`: Ping pong (from first to last and reverse direction back to first, in an endless loop).

## Node

```c
typedef struct {
    pint_char[] name_override;      // Name to use instead of auto-generated one
    pint_char[] fire_on_pass;       // Trigger this target when this node has been reached
    Vector position;                // The node's position in world coordinates
    Vector angles;                  // The node's angles
    int flags;                      // Editor flags
    int kv_count;                   // Number of node's key-value pairs
    KeyValue[kv_count] keyvalues;   // Node's key-value pairs (properties)
} Node;
```

# Entity

```c
typedef struct {
    p_char[] classname;                 // The entity's classname
    Vector origin;                      // The origin if it's a point entity
    int flags;                          // Editor flags
    int group_id;                       // ID of the group this entity belongs to
    int root_group_id;                  // The top-most group this entity is nested within
    Color color;                        // Editor color of the Path
    pint_char[13] special_keys;         // The names of various special attributes used by J.A.C.K
    int sp_spawnflags;
    Vector sp_angles;
    int sp_rendering;
    Color sp_fx_color;
    int sp_rendermode;
    int sp_render_fx;
    short sp_body;
    short sp_skin;
    int sp_sequence;
    float sp_framerate;
    float sp_scale;
    float sp_radius;
    char[28] unknown;
    int kv_count;                       // Number of node's key-value pairs
    KeyValue[kv_count] keyvalues;       // Node's key-value pairs (properties)
    int vg_count;                       // Number of VisGroups
    KeyValue[vg_count] visgroup_ids;    // The ID numbers of the VisGroups the entity belongs to
    int brush_count;                    // Number of brushes
    Brush[brush_count] brushes;         // The brushes making up this entity (empty if point entity)
} Entity;
```

I am still unsure about the J.A.C.K special attributes section.
The fields and their data types here just reflect how they're described in MESS and should not be
taken as a definite guide for parsing this part of the file.
During my own testing I noticed the special attribute keys change depending on the type of entity
and it's possible different data types are used according to the key.

# Brush

```c
typedef struct {
    int curve_count;                    // Unused in GoldSrc, possibly related to Quake III/Volatile curve surfaces
    int flags;                          // Editor flags
    int group_id;                       // ID of the group this entity belongs to
    int root_group_id;                  // The top-most group this entity is nested within
    Color color;                        // Editor color of the Path
    int vg_count;                       // Number of VisGroups
    KeyValue[vg_count] visgroup_ids;    // The ID numbers of the VisGroups the entity belongs to
    int face_count;                     // Number of faces (polygons) making up the brush
    Face[face_count] faces;             // The brush's faces
} Brush;
```

It's possible there's an array of curve surfaces following `curve_count`.
I do not know the structure of these but at least for game profiles with
Map Type set to *Half-Life / TFC* there is nothing here.

# Face

```c
typedef struct {
    int render_flags;               // I'm unsure what this does. Editor flags perhaps?
    int vertex_count;               // Number of vertices in the face
    Vector right_axis;              // The texture's projected right axis
    float shift_x;                  // Horizontal shift of the texture
    Vector down_axis;               // The texture's projected down axis
    float shift_y;                  // Vertical shift of the texture
    float scale_x;                  // Horizontal scale multiplier
    float scale_y;                  // Vertical scale multiplier
    float angle;                    // The angle of the applied rotation
    char[20] unknown1;
    nt_char[64] texture_name;       // Name of the texture applied to the face
    char[20] unknown2;
    Vertex[vertex_count] vertices;  // The vertices that make up the face
} Face;
```

## Vertex

```c
typedef struct {
    Vector coordinates;     // Vertex coordinates
    Vector normal;          // MESS speculates this is the normal vector for the vertex
} Vertex;
```

# Sources
- [MESS](https://github.com/pwitvoet/mess/blob/master/MESS/Formats/JmfFormat.cs)
