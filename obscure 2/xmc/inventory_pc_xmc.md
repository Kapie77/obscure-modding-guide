# `inventory_pc.xmc` Analysis

## Overview

`inventory_pc.xmc` defines the main inventory interface and its related screens. The XML contains six menu definitions covering weapon selection, item/clue display, team selection, document display, a full-screen menu placeholder, and a small message box.

It also defines three input-offset contexts (`0`, `40`, and `80`) and additional inventory-function messages. The file contains visual layout data, weapon identifiers, character/chapter metadata, clue texture coordinates, and input mappings.

## Structure

| Element | Count | Purpose |
|---|---:|---|
| `<menu>` | 6 | Defines inventory interface screens and components |
| `<item>` | 60 | Defines sprites and text elements within menus |
| `<clue>` | 20 | Maps clue IDs to texture UV regions |
| `<input_offset>` | 3 | Declares input offsets `0`, `40`, and `80` |
| `<input>` | 35 | Maps input IDs to navigation and inventory messages |

## Menu definitions

### `IWEA` — Weapon inventory

- Class: `inv_weapon`
- Icon dimensions: `48 × 46`
- Icon spacing: `50` horizontally and vertically
- Icon origin: `icon_x=221`, `icon_y=243`
- Contains 37 visual items.

The menu defines the weapon-selection screen background and supporting UI elements:

- A full-area background sprite using `bg_weapon`.
- Two background panels using the `bg` class.
- Two `inv_name` sprite areas and two `inv_desc` text areas for weapon information.
- Two additional `inv_name` text fields for the selected weapon's name or related text.
- Two `inv_desc` sprites.
- A grid of weapon-selection sprites.
- Two selection sprites using `m_selection1` and `m_selection`.

#### Weapon grid

The main grid contains 16 positions arranged in four columns and four rows. Fifteen positions have explicit `weapon_type` identifiers; one position has no `weapon_type` attribute.

| Weapon code | Grid position |
|---|---|
| `CLUB` | Row 1, column 1 |
| `BEAT` | Row 1, column 2 |
| `UBET` | Row 1, column 3 |
| `CROS` | Row 1, column 4 |
| `CSAW` | Row 2, column 1 |
| `GUN` | Row 2, column 2 |
| `FLGU` | Row 2, column 3 |
| `FLBA` | Row 2, column 4 |
| `TASE` | Row 3, column 1 |
| `CBOW` | Row 3, column 2 |
| `SHOT` | Row 3, column 3 |
| `UZI` | Row 3, column 4 |
| `UBFL` | Row 4, column 1 |
| `DYNA` | Row 4, column 2 |
| `FLBG` | Row 4, column 3 |
| — | Row 4, column 4; no `weapon_type` specified |

The weapon sprites use `class_name="inv_weap"` and include `a_up`, `a_down`, `a_left`, and `a_right` attributes. These attributes define explicit navigation links between selection positions. The links reference item indices rather than weapon codes, so their runtime interpretation depends on the inventory UI implementation.

#### Additional weapon positions

Eight more `inv_weap` sprites are positioned around the left and right sides of the main grid. These entries also define directional navigation links, but do not specify a `weapon_type`. They may represent additional slots or navigation targets; their exact purpose is not established by the XML alone.

#### Selection graphics

Two selection sprites are declared:

- `m_selection1`, with foreground color `FF731700`.
- `m_selection`, with foreground color `FF004548`.

These provide two differently colored selection graphics for the weapon interface.

### `IITE` — Item and clue inventory

- Class: `inv_item`
- Contains five visual items and 20 clue definitions.
- Uses the `bg_items` texture for its background.

The menu includes:

- A background sprite using `bg_items`.
- An `inv_name` text field positioned near the bottom-center area.
- An `inv_desc` sprite for item-related imagery.
- An `inv_objective` text field, likely intended for objective-related text based on its class name.
- A selection sprite using `m_selection2`.

The XML does not provide the actual item names or descriptions; those appear to be supplied elsewhere, likely through text/string resources or runtime data.

#### Clue texture regions

The `<clue>` entries associate numeric clue IDs with rectangular UV coordinates. The texture coordinates use normalized values between `0.0` and `1.0`, indicating regions within a texture atlas.

The 20 clue IDs are:

`1`, `2`, `5`, `6`, `7`, `8`, `9`, `11`, `12`, `13`, `17`, `18`, `19`, `20`, `25`, `26`, `27`, `28`, `29`, `30`.

The menu also declares clue icon layout parameters:

- Origin: `icon_x=48`, `icon_y=73`
- Icon size: `46 × 45`
- Spacing: `50` horizontally and vertically

A separate `<items>` element defines another icon layout:

- Origin: `icon_x=345`, `icon_y=73`
- Icon size: `46 × 45`
- Spacing: `50` horizontally and vertically

The file establishes the clue IDs and their texture regions, but does not identify the clue text or the meaning of each clue.

### `ITEA` — Team selection

- Class: `inv_team`
- Contains 15 visual items.
- Uses `bg_team` as the background and `m_team` for character portraits.

Eight character entries are defined:

| Character code | Character label | Chapter | Chapter state | Description ID |
|---|---|---:|---:|---|
| `BOY2` | `b2` | 1 | 0 | `10104002` |
| `GIR2` | `g2` | 1 | 0 | `10104006` |
| `BOY4` | `b4` | 2 | 0 | `10104004` |
| `GIR3` | `g3` | 2 | 0 | `10104007` |
| — | `prof` | 3 | 3 | `10104009` |
| `BOY3` | `b3` | 5 | 0 | `10104003` |
| `GIR4` | `g4` | 5 | 100 | `10104008` |
| `GIR1` | `g1` | 7 | 0 | `10104005` |
| `BOY1` | `b1` | 7 | 0 | `10104001` |

The `prof` entry is notable because it has a character label and description ID but no `chara_id` attribute. The other seven entries map to the character codes shown in the table.

The menu also defines:

- A selection sprite using `m_selection2`.
- A portrait/description sprite using `m_weap_b1`.
- A name graphic using `m_weap_b1_name`.
- A text field for character information or description.

The `chapter` and `chapter_state` attributes are stored directly on each character entry. The XML does not explain how these values control character availability.

### `IDOC` — Document display

- Class: `inv_document`
- Contains one text item.
- The text item has an empty `string` attribute and a small rectangle positioned at `(120,120)` to `(140,140)`.

This appears to be a minimal document-text placeholder. No document content is embedded in this entry.

### `IFSC` — Full-screen menu

- Class: `full_screen`
- Contains no child items or additional attributes.

The menu is declared as a full-screen interface component, but its actual contents or behavior are not defined in this file.

### `IPOP` — Message box

- Class: `mb`
- Contains two items.

The first item is a border sprite using the `m_border` texture. The second is a centered text element using the `mb_text` class.

This defines a small message-box layout, but no message text or button choices are specified here.

## Input configuration

The file declares three input offsets:

| Offset value | Parameter context |
|---:|---|
| `0` | `param="0"` |
| `40` | `param="1"` |
| `80` | `param="0"` |

### Navigation mappings

The first two offset groups (`0` and `40`) each define ten mappings:

| Input ID | Message | Function |
|---:|---|---|
| 18 | `up` | Move upward |
| 19 | `down` | Move downward |
| 20 | `left` | Move left |
| 21 | `right` | Move right |
| 9 | `valid` | Confirm |
| 10 | `cancel` | Cancel |
| 27 | `up` | Alternative upward navigation |
| 29 | `down` | Alternative downward navigation |
| 30 | `left` | Alternative left navigation |
| 28 | `right` | Alternative right navigation |

The mappings at offset `0` use `param="0"` on the primary directional and confirmation/cancel entries. The mappings at offset `40` use `param="1"` for those same entries. The additional directional entries do not consistently specify a `param` attribute.

The offset `80` group contains nine mappings: the four primary directions, confirmation (`valid`), and four alternative directional inputs. It does not define a `cancel` mapping in this group.

Most directional entries use `just_pressed="0"` and `next_time="500"`, indicating repeat/navigation timing parameters. The exact timing behavior depends on the engine's input system.

### Additional inventory messages

Six more inputs are declared without an explicit offset:

| Input ID | Message |
|---:|---|
| 22 | `invf1` |
| 23 | `invf2` |
| 24 | `invf3` |
| 25 | `next` |
| 26 | `previous` |
| 17 | `leave` |

These messages indicate additional inventory functions, page/entry navigation, and an exit action. Their exact effects are not defined by this XML.

## Notable observations

- `inventory_pc.xmc` describes a broader inventory interface than `inv_live.xmc`: it includes weapon selection, item/clue browsing, team selection, document display, and a message box.
- The weapon screen explicitly lists 15 weapon codes, matching the set of weapon identifiers used in the debug inventory menus.
- The weapon grid has 16 positions, but only 15 have a `weapon_type` value.
- Eight additional weapon sprites sit around the main grid and have navigation links but no explicit weapon codes.
- The team menu contains seven entries with character codes and one `prof` entry without a `chara_id`.
- The clue menu defines 20 clue IDs and their texture-atlas coordinates.
- The input setup contains three offset groups and six additional inventory-specific messages.
- The XML defines interface structure and metadata, but does not contain the actual item descriptions, clue text, document contents, message-box text, or the runtime rules for character availability.

## Conclusion

`inventory_pc.xmc` defines the game's main inventory interface for weapon selection, item and clue browsing, team selection, document display, and message-box presentation. It includes 15 explicit weapon identifiers, eight team entries, 20 clue texture mappings, and input mappings across three offset contexts. The file is primarily a UI layout and navigation configuration; the content and runtime behavior behind several interface elements must be supplied by other resources or game code.
