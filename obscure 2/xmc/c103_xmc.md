# `c103.xmc` --- C103 Digicode Keypad Layout

## Overview

`c103.xmc` defines the visual configuration of a digicode keypad. Its
root element is `<digicode>`. The file specifies dedicated texture
resources, a full-texture background region, a display region, an option
related to activated keys, and the geometry and texture coordinates for
twelve keys.

The keypad uses a conventional telephone-style arrangement:

``` text
1  2  3
4  5  6
7  8  9
*  0  #
```

The XML defines the keypad's presentation and key mapping. It does not
provide an access code, input-processing rules, or puzzle validation
logic.

## 1. Texture configuration

The `<textures>` element references three resources:

  Attribute      Value          Role indicated by the attribute name
  -------------- -------------- --------------------------------------
  `background`   `digi_c103b`   Keypad background
  `selection`    `digi_C103g`   Key selection/highlight
  `display`      `digi_C103f`   Display/key graphics

The resource names are case-sensitive as written in the XML. The file
does not contain the texture images themselves.

## 2. Activated-key display option

The XML contains:

``` xml
<show_activated_keys value="1" />
```

This explicitly sets the `show_activated_keys` option to `1`. The name
suggests that activated keys are to be shown or visually indicated, but
the XML does not define the exact rendering effect or the meaning of the
value beyond the setting itself.

## 3. Background and display regions

Two top-level elements define rectangular regions:

  Element              `u`     `v`   `width`   `height`
  ---------------- ------- ------- --------- ----------
  `<background>`       0.0     0.0       1.0        1.0
  `<display>`        0.556   0.177     0.289      0.124

The background covers the full normalized texture region (`0.0, 0.0` to
`1.0, 1.0`). The display region uses the same coordinates and dimensions
found in the previously analyzed `01.xmc` file.

These are normalized coordinates; the XML does not specify source image
dimensions or pixel positions.

## 4. Key structure

There are twelve `<key>` elements. Each one contains four child
elements:

  -----------------------------------------------------------------------
  Child element           Attributes              Purpose indicated by
                                                  its name
  ----------------------- ----------------------- -----------------------
  `<center>`              `u`, `v`, `width`,      Key position and
                          `height`                geometry

  `<selection>`           `u`, `v`, `width`,      Selection texture
                          `height`                region

  `<display>`             `u`, `v`, `width`,      Key graphic texture
                          `height`                region

  `<character>`           `width`, `height`       Character dimensions
  -----------------------------------------------------------------------

All twelve keys use the same character dimensions:

-   `width="0.03"`
-   `height="0.055"`

For every key, the `<selection>` and `<display>` elements contain
identical coordinates and dimensions. This means the selection and
display regions are mapped to the same rectangle for each key in this
configuration.

### 4.1 Key arrangement and center coordinates

The `center` coordinates establish three columns and four rows. The
following table preserves the values from the XML:

    Row Key IDs, left to right   Center `u` values                      Center `v`
  ----- ------------------------ ----------------------------------- -------------
      1 `1`, `2`, `3`            0.69140625, 0.7578125, 0.82421875      0.41796875
      2 `4`, `5`, `6`            0.69140625, 0.7578125, 0.82421875     0.482421875
      3 `7`, `8`, `9`            0.69140625, 0.7578125, 0.82421875     0.544921875
      4 `*`, `0`, `#`            0.69140625, 0.7578125, 0.82421875        0.609375

Every key uses the same center dimensions:

  Attribute          Value
  ----------- ------------
  `width`       0.05078125
  `height`      0.04296875

### 4.2 Texture-atlas regions

The `<selection>` and `<display>` rectangles use the same atlas
coordinates. They form a three-column by four-row grid:

  -------------------------------------------------------------------------------
                    Row Left cell        Middle cell            Right cell
  --------------------- ---------------- ---------------------- -----------------
                      1 `1`: U           `2`: U                 `3`: U
                        0.0--0.328125, V 0.328125--0.6640625, V 0.6640625--1.0, V
                        0.0--0.25        0.0--0.25              0.0--0.25

                      2 `4`: U           `5`: U                 `6`: U
                        0.0--0.328125, V 0.328125--0.6640625, V 0.6640625--1.0, V
                        0.25--0.5        0.25--0.5              0.25--0.5

                      3 `7`: U           `8`: U                 `9`: U
                        0.0--0.328125, V 0.328125--0.6640625, V 0.6640625--1.0, V
                        0.5--0.75        0.5--0.75              0.5--0.75

                      4 `*`: U           `0`: U                 `#`: U
                        0.0--0.328125, V 0.328125--0.6640625, V 0.6640625--1.0, V
                        0.75--1.0        0.75--1.0              0.75--1.0
  -------------------------------------------------------------------------------

The columns are not represented by perfectly equal-width intervals in
the XML: - First column: `0.328125` - Second column: `0.3359375` - Third
column: `0.3359375`

Each row spans a vertical interval of `0.25`.

## 5. Structural counts

  Element or property           Count / value
  -------------------------- ----------------
  Root element                 1 (`digicode`)
  `<textures>`                              1
  `<show_activated_keys>`                   1
  Top-level `<background>`                  1
  Top-level `<display>`                     1
  `<key>`                                  12
  `<center>`                               12
  Key-level `<selection>`                  12
  Key-level `<display>`                    12
  `<character>`                            12
  Numeric keys                             10
  Symbol keys                    2 (`*`, `#`)

## 6. Comparison with `01.xmc`

Both files configure a digicode interface and define twelve keys, but
their layouts and texture references differ.

  ---------------------------------------------------------------------------------
  Feature                 `01.xmc`                `c103.xmc`
  ----------------------- ----------------------- ---------------------------------
  Background texture      `digicode`              `digi_c103b`

  Selection texture       `di_glow`               `digi_C103g`

  Display texture         `digit`                 `digi_C103f`

  Key IDs                 `0`--`9`, `CANCEL`,     `0`--`9`, `*`, `#`
                          `VALID`                 

  Physical arrangement    Numeric keypad with     Telephone-style 3 × 4 keypad
                          separate action keys    

  Background region       U 0.5, V 0.5, width     Full region: U 0, V 0, width 1,
                          0.5, height 0.5         height 1

  Activated-key option    Not present             `show_activated_keys value="1"`

  Key selection/display   Different for some key  Identical for each key
  regions                 types                   
  ---------------------------------------------------------------------------------

The two files share the same top-level display rectangle (`u="0.556"`,
`v="0.177"`, `width="0.289"`, `height="0.124"`), but the key
identifiers, texture resources, and layout geometry are different.

## 7. What can be concluded

The XML establishes that: - `c103.xmc` configures a twelve-key digicode
with digits `0`--`9` and symbols `*` and `#`. - The keypad is arranged
in four rows and three columns. - It references three C103-specific
texture resources. - The background uses the full normalized texture
region. - `show_activated_keys` is explicitly set to `1`. - Each key has
separate position and atlas-region definitions. - Selection and display
regions are identical for each key.

## 8. What the XML does not establish

The file does not reveal: - The correct code or expected sequence. -
Whether `*` and `#` have special input functions. - What visual change
is produced by `show_activated_keys`. - Whether the keypad accepts a
fixed number of digits. - What happens after a correct or incorrect
entry. - Which door or puzzle uses this layout. - The pixel dimensions
or actual appearance of the referenced textures.

Those details require other resource files or runtime/game-code
evidence.

## Summary

`c103.xmc` is a visual layout and texture-mapping definition for a C103
digicode. It describes a telephone-style keypad with twelve keys,
C103-specific background, selection, and display textures, and an
enabled `show_activated_keys` setting. It does not define the keypad's
code or input-validation behavior.
