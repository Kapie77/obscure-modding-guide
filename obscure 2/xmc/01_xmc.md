# `01.xmc` --- Digicode Keypad Layout

## Overview

`01.xmc` defines the visual layout and texture-coordinate regions for a
numeric keypad interface identified by the root element `<digicode>`.
The configuration describes the keypad textures, the background and
display regions, and the geometry and texture mapping of each key.

The file contains **12 key definitions**: - Numeric keys: `0` through
`9` - Action keys: `CANCEL` and `VALID`

This is a visual/layout definition. It does not contain a numeric access
code, puzzle solution, input-processing logic, validation rules, or any
explicit link to a particular door or puzzle.

## 1. Root and texture configuration

The root element is:

``` xml
<digicode>
```

Its `<textures>` child references four texture identifiers:

  Attribute      Value        Role indicated by the attribute name
  -------------- ------------ --------------------------------------
  `background`   `digicode`   Background texture
  `display`      `digit`      Texture used for the display/digits
  `selection`    `di_glow`    Selection/highlight texture

The XML supplies these resource identifiers but does not include the
image files themselves or explain how the rendering system loads them.

## 2. Background and display regions

Two top-level regions define normalized texture coordinates:

  Element              `u`     `v`   `width`   `height`
  ---------------- ------- ------- --------- ----------
  `<background>`       0.5     0.5       0.5        0.5
  `<display>`        0.556   0.177     0.289      0.124

These values describe rectangular regions in texture-coordinate space.
The XML does not state the source texture dimensions, pixel coordinates,
or whether the coordinates represent a top-left origin or another
convention.

## 3. Key structure

Every `<key>` contains the same four child elements:

  -----------------------------------------------------------------------
  Child element           Purpose indicated by    Data stored
                          its name                
  ----------------------- ----------------------- -----------------------
  `<center>`              Key placement/geometry  `u`, `v`, `width`,
                                                  `height`

  `<selection>`           Selection texture       `u`, `v`, `width`,
                          region                  `height`

  `<display>`             Key image/glyph texture `u`, `v`, `width`,
                          region                  `height`

  `<character>`           Character dimensions    `width`, `height`
  -----------------------------------------------------------------------

All keys use the same selection rectangle (`0, 0, 1, 1`). The numeric
keys also share character dimensions of `0.03 × 0.055`. The two action
keys use `0.1 × 0.1`.

### 3.1 Numeric keys

The `center` values below are reproduced exactly from the XML. The
`display` values identify the corresponding rectangular region used for
each numeric key.

  -----------------------------------------------------------------------------------
   Key ID   Center   Center   Center   Center   Display   Display   Display   Display
               `u`      `v`    width   height       `u`       `v`     width    height
  ------- -------- -------- -------- -------- --------- --------- --------- ---------
      `0`    0.712    0.796     0.10     0.33      0.00      0.00      0.25      0.25

      `1`    0.617    0.422     0.10     0.33      0.25      0.00      0.25      0.25

      `2`    0.710    0.419     0.10     0.33      0.50      0.00      0.25      0.25

      `3`    0.811    0.417     0.10     0.33      0.75      0.00      0.25      0.25

      `4`    0.615    0.545     0.10     0.33      0.00      0.25      0.25      0.25

      `5`    0.712    0.545     0.10     0.33      0.25      0.25      0.25      0.25

      `6`    0.811    0.543     0.10     0.33      0.50      0.25      0.25      0.25

      `7`    0.618    0.670     0.10     0.33      0.75      0.25      0.25      0.25

      `8`    0.712    0.669     0.10     0.33      0.00      0.50      0.25      0.25

      `9`    0.810    0.667     0.10     0.33      0.25      0.50      0.25      0.25
  -----------------------------------------------------------------------------------

The numeric key display regions form a regular `4 × 3` texture-atlas
grid: - Each cell is `0.25 × 0.25`. - The first row contains keys
`0`--`3` in atlas order. - The second row contains keys `4`--`7`. - The
third row contains keys `8` and `9` in the first two columns.

This is the order of the texture regions, not necessarily the physical
arrangement of the keypad. Physical placement is described separately by
each key's `<center>` element.

### 3.2 Action keys

  --------------------------------------------------------------------------------------------------------------
  Key ID       Center   Center   Center   Center   Display   Display   Display   Display   Character   Character
                  `u`      `v`    width   height       `u`       `v`     width    height       width      height
  ---------- -------- -------- -------- -------- --------- --------- --------- --------- ----------- -----------
  `CANCEL`      0.617    0.800     0.10     0.33       0.1       0.1       0.2       1.0         0.1         0.1

  `VALID`       0.812    0.794     0.10     0.33       0.1       0.1       0.2       1.0         0.1         0.1
  --------------------------------------------------------------------------------------------------------------

Both action keys use identical display and character dimensions. Their
display rectangle differs from the quarter-cell atlas regions used by
the numeric keys.

The names suggest cancellation and confirmation actions, respectively.
The XML does not define what those actions do when activated.

## 4. Structural counts

  Element or property           Count / value
  -------------------------- ----------------
  Root element                 1 (`digicode`)
  `<textures>`                              1
  Top-level `<background>`                  1
  Top-level `<display>`                     1
  `<key>`                                  12
  Numeric keys                             10
  Action keys                               2
  `<center>`                               12
  Key-level `<selection>`                  12
  Key-level `<display>`                    12
  `<character>`                            12

Each key has exactly one of each of the four child elements listed in
the key-structure section.

## 5. What can be concluded

The file provides evidence for the following: - It configures a
digicode-style numeric keypad. - It references separate background,
digit/display, and selection textures. - It defines ten numeric keys and
two named action keys. - Key placement and key texture mapping are
configured independently. - Numeric key graphics are mapped to regular
quarter-size cells in a texture atlas.

## 6. What the XML does not establish

The file does **not** reveal: - The correct code for any in-game
keypad. - Whether the keypad accepts a fixed-length or variable-length
code. - How entered digits are stored or compared. - What happens after
pressing `CANCEL` or `VALID`. - Which game level, door, or puzzle uses
this particular layout. - The actual appearance or pixel dimensions of
the referenced textures.

Those details would require other resources or runtime/game-code
evidence.

## Summary

`01.xmc` is a compact visual configuration for the game's digicode
interface. Its main function is to map a keypad background, display
area, numeric key graphics, selection region, and two action keys to
normalized layout and texture coordinates. It is a layout/texture
mapping resource rather than a definition of a keypad puzzle's code or
logic.
