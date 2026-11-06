# `inv_live.xmc` Analysis

## Overview

`inv_live.xmc` defines live inventory and HUD-related menu elements. The XML contains four menu definitions, two input-offset declarations, and 22 input mappings. Its structure suggests that it handles the on-screen representation and controls of live inventory elements for two parameterized player/input contexts.

The file describes UI geometry, sprite classes, colors, texture coordinates, and input messages. It does not contain item names, weapon identifiers, inventory contents, or gameplay rules explaining how inventory values are updated.

## Structure

| Element | Count | Purpose |
|---|---:|---|
| `<menu>` | 4 | Defines inventory and HUD sprite groups |
| `<item>` inside menus | 22 | Defines individual sprite elements |
| `<input_offset>` | 2 | Declares offsets `0` and `40` |
| `<input>` | 22 | Maps input IDs to inventory navigation and confirmation messages |

## Menu definitions

### `IWL1` — First live weapon inventory panel

- Class: `inv_weap_live`
- Rectangle: left `48`, top `36`, right `200`, bottom `190`
- Rectangle mode: `scale`
- Contains six sprite entries:
  - Five `inv_item_live` sprites, arranged as a central/around-the-center group.
  - One `life` sprite, positioned inside the group.

The first `inv_item_live` sprite is explicitly hidden (`visible="0"`). The other four item sprites use the background color `FF004548` and include `bgradu` direction values: `down2up`, `left2right`, `up2down`, and `right2left`. These values appear to describe directional background gradients or fills, although their exact rendering behavior is not defined by this XML.

The `life` sprite occupies coordinates `left=54`, `top=54`, `right=150`, `bottom=150`.

### `IWL2` — Second live weapon inventory panel

- Class: `inv_weap_live`
- Rectangle: left `388`, top `36`, right `542`, bottom `190`
- Rectangle mode: `scale`
- Contains the same six-sprite structure as `IWL1`.

Its `inv_item_live` sprites use the background color `FF731700`, contrasting with the teal color used by `IWL1`. The sprite arrangement and directional `bgradu` values mirror the first panel. As in `IWL1`, the first item sprite is hidden, and a `life` sprite is placed in the center.

The matching layouts and different colors indicate two parallel live inventory displays. The XML alone does not identify which characters or players these panels belong to.

### `INIL` — Live item indicator elements

- Class: `inv_item_live`
- Contains six `inv_item_live` sprites.
- No menu rectangle is declared at the menu level.

All six sprites share the same horizontal bounds (`left=48`, `right=112`) and are stacked vertically in 64-unit intervals:

| Sprite | Top | Bottom | Background color | Foreground color |
|---:|---:|---:|---|---|
| 1 | 468 | 532 | `00808080` | `00FFFFFF` |
| 2 | 404 | 468 | `20808080` | `20FFFFFF` |
| 3 | 340 | 404 | `60808080` | `60FFFFFF` |
| 4 | 276 | 340 | `FF808080` | `FFFFFFFF` |
| 5 | 212 | 276 | `50808080` | `50FFFFFF` |
| 6 | 148 | 212 | `00808080` | `00FFFFFF` |

The color values vary in their alpha component, producing different opacity levels. The fourth entry is fully opaque, while the first and sixth entries are fully transparent. This may represent different item-selection or availability states, but the precise meaning of each position is not specified in the file.

### `inv_nrj` — Energy HUD element

- Class: `inv_nrj`
- Contains four sprites.
- All four sprites reference the texture `hud_nrj`.
- All use `rect_type="scale"` and white foreground color (`FFFFFFFF`).

The four sprites occupy a horizontal region around `left=227` to `right=417`, with vertical bounds approximately `top=73` to `bottom=102`. Their UV coordinates divide the texture into separate regions:

| Sprite | Screen bounds (left, top, right, bottom) | Texture UV bounds (`u1`, `v1`, `u2`, `v2`) |
|---:|---|---|
| 1 | `235, 73, 405, 100` | `0.06, 0.57, 0.93, 0.91` |
| 2 | `241, 73, 399, 102` | `0.09, 0.05, 0.90, 0.44` |
| 3 | `227, 73, 241, 102` | `0.02, 0.05, 0.09, 0.44` |
| 4 | `399, 73, 417, 102` | `0.90, 0.05, 0.98, 0.44` |

The arrangement is consistent with a composed horizontal HUD graphic made from a central section and two narrow end sections, with an additional sprite using a separate texture region. The texture itself is not included in this XML, so the exact visual appearance and the function of each segment cannot be confirmed from this file alone.

## Input configuration

The file declares two input offsets:

| Offset value | Associated parameter |
|---:|---:|
| `0` | `param="0"` |
| `40` | `param="1"` |

There are 11 input messages for each parameter, for 22 mappings total.

### Input mappings for `param="0"` and offset `0`

| Input ID | Message | Behavior flags |
|---:|---|---|
| 15 | `previous` | `just_pressed="1"` |
| 16 | `next` | `just_pressed="1"` |
| 15 | `up` | `just_pressed="0"`, `next_time="500"` |
| 16 | `down` | `just_pressed="0"`, `next_time="500"` |
| 27 | `sel_up` | — |
| 28 | `sel_right` | — |
| 29 | `sel_down` | — |
| 30 | `sel_left` | — |
| 9 | `valid` | — |
| 10 | `cancel` | — |

### Input mappings for `param="1"` and offset `40`

| Input ID | Message | Behavior flags |
|---:|---|---|
| 15 | `previous` | `just_pressed="0"` |
| 16 | `next` | `just_pressed="0"` |
| 15 | `up` | `just_pressed="40"`, `next_time="500"` |
| 16 | `down` | `just_pressed="40"`, `next_time="500"` |
| 27 | `sel_up` | — |
| 28 | `sel_right` | — |
| 29 | `sel_down` | — |
| 30 | `sel_left` | — |
| 9 | `valid` | — |
| 10 | `cancel` | — |

The messages define the following control operations:

- `previous` / `next`: move to the previous or next entry.
- `up` / `down`: vertical navigation, with a `next_time` value of `500`.
- `sel_up`, `sel_right`, `sel_down`, `sel_left`: directional selection messages.
- `valid`: confirmation.
- `cancel`: cancellation or return.

The second mapping set repeats the same input IDs and messages with `param="1"` and offset `40`. This establishes two distinct input contexts in the XML. The exact meaning of the `param`, `offset`, and `just_pressed` values depends on the engine's input handling and is not defined here.

## Notable observations

- `IWL1` and `IWL2` are parallel live weapon-inventory panels with matching geometry and sprite arrangements, but different background colors.
- Each weapon panel contains five item sprites and one life sprite. One of the five item sprites is initially hidden.
- `INIL` defines six vertically stacked item sprites with different opacity levels.
- `inv_nrj` uses four sprite regions from the `hud_nrj` texture to compose an energy-related HUD element.
- The input configuration is duplicated for two parameter/offset contexts (`0` and `40`).
- The XML defines visual components and input-message mappings, but does not identify the actual controller buttons, the inventory data structures, or the runtime logic that updates these elements.

## Conclusion

`inv_live.xmc` is a live inventory/HUD layout and input-configuration file. It defines two color-distinguished weapon inventory panels, a six-position item indicator group, an energy HUD graphic assembled from the `hud_nrj` texture, and navigation/confirmation controls duplicated across two input contexts. Its contents are primarily presentation and input-mapping data rather than a catalog of inventory items or weapons.
