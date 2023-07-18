---
title: Data Types
layout: default
parent: Format Specifications
nav_order: 1
---

## Primitive data types notations used in format specifications

These are based on C Types.

Where applicable square brackets will denote an array of this type.
A number between the square brackets means its a fixed-length array of this length, otherwise it's variable.<br>
For example, a string of 16 bytes might be represented by `char[16]`.

| Type         | Size (bytes)       | Description              |
|:-------------|:-------------------|:-------------------------|
| char         | 1                  | signed char              |
| u_char       | 1                  | unsigned char            |
| short        | 2                  | signed short             |
| int          | 4                  | signed integer           |
| u_int        | 4                  | unsigned integer         |
| float        | 4                  | float                    |
| _Bool        | 1                  | boolean                  |
| char[n]      | n                  | string                   |
| p_char[]     | variable (max 256) | pascal string [^1]       |
| pint_char[]  | variable           | pascal string (int) [^2] |
| nt_char[n]   | n                  | null-terminated string   |

## Notes
[^1]: Pascal strings are length-prefixed with a single byte, and thus the string length is limited to 255 bytes.
[^2]: Pascal string length-prefixed with a 4-byte int.
