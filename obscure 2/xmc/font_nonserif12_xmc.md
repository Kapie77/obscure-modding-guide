# `font_nonserif12.xmc` — XML Analysis

## Overview

The extracted `font_nonserif12.xml` defines a bitmap font named `Font_Nonserif12`. Its settings declare a texture size of **512 × 256 pixels**. The name suggests a non-serif font at size 12, although the XML alone does not confirm its exact in-game use or rendered size.

## Font Structure

- **Root element:** `tag_BFA4CE15`
- **Font name:** `Font_Nonserif12`
- **Declared texture dimensions:** 512 × 256 pixels
- **Glyph entries:** 141 `char` elements
- **Glyph height:** 25 pixels for the listed entries
- **Glyph widths:** Variable, depending on the character

The font uses individually positioned glyphs in a bitmap texture rather than a fixed-width grid. The listed glyph coordinates fall within the declared texture dimensions.

## Character Coverage

The entries include:

- Uppercase Latin letters (`A–Z`)
- Lowercase Latin letters (`a–z`)
- Digits (`0–9`)
- Common punctuation, brackets, and mathematical/operator symbols
- Accented Latin characters
- Additional symbols and character codes

This coverage indicates that the font supports more than basic English text. The precise rendering and appearance of each glyph should be verified against the associated texture image.

## Data Quality Notes

Several `attr_0BB5AC54` values are empty or contain replacement characters such as `�` or `��`. This may indicate a character-encoding or extraction issue, but the cause cannot be established from the XML alone.

Some entries also warrant verification:

- The apostrophe-like entries at character codes `39` and `8217` share the same listed position (`x=195`, `y=26`) but have different widths.
- Character code `339` has an underscore-like attribute, which appears inconsistent with the numeric code.
- Some additional symbol entries have empty attributes.

These observations should be treated as unresolved data questions, not confirmed defects in the original game resource.

## Texture Verification

The XML declares a **512 × 256** texture, and the listed glyph coordinates are within those bounds. However, the associated texture image has not been visually checked here, so the glyph-to-texture mapping and actual appearance remain unverified.

## Conclusion

`font_nonserif12.xmc` defines a variable-width bitmap font with broad Latin character coverage, including accented letters and additional symbols. The XML structure and coordinates can be documented, but several character attributes appear empty or corrupted, and comparison with the corresponding texture is still needed before drawing conclusions about the font's visual appearance or whether the data issues originate in the original resource or the extraction process.
