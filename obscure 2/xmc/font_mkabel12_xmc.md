# `font_mkabel12.xmc` — Analysis

## Overview

`font_mkabel12.xmc` defines a compact bitmap-font atlas. The XML contains 12 glyph entries: the ten digits (`0`–`9`), slash (`/`), and hyphen (`-`). This limited character set suggests a numeric-display use case, such as dates, counters, or interface indicators, although the exact use is not specified in the XML.

## Texture settings

The `<settings>` element declares:

- **Name:** `font_mkabel12`
- **Texture dimensions:** 128 × 32 pixels

The name may suggest a font family or size, but the XML does not establish the original typeface or point size.

## Glyph entries

All glyphs begin at `y="2"` and have a height of 17 pixels. Their horizontal positions and widths are:

| Code | Character | X | Width | Height |
|---:|:---:|---:|---:|---:|
| 48 | `0` | 2 | 9 | 17 |
| 49 | `1` | 13 | 6 | 17 |
| 50 | `2` | 21 | 9 | 17 |
| 51 | `3` | 32 | 9 | 17 |
| 52 | `4` | 43 | 9 | 17 |
| 53 | `5` | 54 | 8 | 17 |
| 54 | `6` | 64 | 9 | 17 |
| 55 | `7` | 75 | 8 | 17 |
| 56 | `8` | 85 | 9 | 17 |
| 57 | `9` | 96 | 9 | 17 |
| 47 | `/` | 106 | 7 | 17 |
| 45 | `-` | 115 | 5 | 17 |

The codes correspond to the Unicode values for the listed ASCII characters.

## Attribute interpretation

Each `<char>` entry also includes `attr_0BB5AC54`, whose value matches the displayed character (`"0"`–`"9"`, `"/"`, or `"-"`). This suggests that the attribute stores a character label or identifier, while `code` stores its numeric character code. The XML does not explicitly document the attribute's semantics, so this interpretation remains tentative.

## Texture-boundary check

The glyph coordinates fit within the declared 128 × 32 texture:

- **Horizontal:** the final glyph starts at `x=115` and is 5 pixels wide, ending at x=120.
- **Vertical:** every glyph starts at `y=2` and is 17 pixels high, ending at y=19.

No glyph extends beyond the declared texture bounds. The actual appearance of the glyphs and their correspondence with the associated texture cannot be verified from this XML alone.

## Conclusion

`font_mkabel12.xmc` describes a small bitmap font containing ten digits and two punctuation symbols. Glyph heights are fixed at 17 pixels, while widths vary from 5 to 9 pixels, indicating variable-width glyph definitions.

**Analysis status:** XML analyzed; visual verification against the associated texture has not been performed.
