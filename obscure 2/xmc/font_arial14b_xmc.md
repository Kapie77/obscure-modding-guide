# `font_arial14b.xmc` — Bitmap Font Definition

## Overview

`font_arial14b.xmc` defines a bitmap-font character map associated with the font name `Arial`. It maps character codes and textual character values to rectangular regions of a texture. The accompanying texture, `font_arial14b.tga`, provides the visual glyph artwork.

The XML metadata and TGA image are consistent with a bitmap-font resource, but the supplied files contain a significant dimension/coordinate mismatch.

## Texture Settings

The XML declares the following settings:

| Property | Value |
|---|---|
| Font name | `Arial` |
| Texture width | 256 pixels |
| Texture height | 128 pixels |

The supplied TGA image is 256 × 128 pixels, confirming the dimensions declared in the XML. The image contains light-colored glyph artwork with dark outlines on a transparent background.

## Character Mapping

Each `<char>` element associates a character with metadata:

- `code`: numeric character code.
- `attr_0BB5AC54`: textual representation of the character.
- `x`, `y`: top-left coordinates of the glyph region in the texture.
- `w`, `h`: width and height of the glyph region.

For example:

```xml
<char code="65" x="9" y="2" w="13" h="22" attr_0BB5AC54="A" />
```

This entry maps the character `A` to a 13 × 22 pixel rectangle beginning at `(9, 2)`.

Glyph widths vary by character, which is consistent with a proportional font rather than a monospaced font. Most entries specify a height of 22 pixels.

## Character Coverage

The mapping includes:

- Uppercase letters `A–Z`.
- Lowercase letters `a–z`.
- Digits `0–9`.
- Punctuation and common symbols, including brackets, quotation marks, arithmetic operators, and slashes.
- Accented Latin characters, including `é`, `è`, `ê`, `ç`, `à`, `á`, `ñ`, and several accented uppercase letters.
- Currency and typographic symbols, including `$`, `€`, `£`, `¥`, `©`, `®`, and a final entry with numeric code `8482`.

The final entry uses code `8482`, which corresponds to the trademark symbol `™`, but its textual attribute appears as `��` in the extracted XML. This may reflect a text-encoding or extraction issue; the provided data does not establish its cause.

## Confirmed Texture/Coordinate Mismatch

The XML and supplied TGA agree on a texture size of 256 × 128 pixels, but some glyph coordinates extend beyond the image bounds.

The last group of characters begins at `y="122"` and declares `h="22"`. Those rectangles extend to `y = 144`, exceeding the image's 128-pixel height by 16 pixels. The entries in this group include accented characters and symbols such as `ü`, `ô`, `á`, `ñ`, `Á`, `É`, `€`, `©`, `®`, and the code-8482 entry.

In the supplied TGA, the visible glyph rows appear to stop around the preceding row, rather than providing a complete row at `y=122`. Therefore, the last group of glyphs defined by the XML is not visibly represented in the corresponding region of this image.

Possible explanations include:

1. The TGA is incomplete or truncated.
2. The XML and TGA originate from different versions or variants of the resource.
3. The original resource data contains incorrect dimensions or glyph coordinates.

The available files do not establish which explanation is correct. The XML coordinates should not be changed without comparing other font resources or verifying the original game assets.

## Interpretation and Limitations

The resource is best described as a bitmap-font atlas mapping file for a font named `Arial`. The XML supplies character metadata and texture coordinates; it does not contain the glyph pixels themselves.

The files alone do not establish the font's exact in-game usage, the intended nominal point size, the rendering implementation, or why the final character row falls outside the supplied texture. The filename `font_arial14b` may suggest a 14-point bold Arial variant, but that interpretation is not confirmed by the XML metadata, which only explicitly names `Arial`.

## Conclusion

`font_arial14b.xmc` defines a proportional bitmap font with Latin letters, digits, punctuation, accented characters, and selected symbols. The accompanying `font_arial14b.tga` confirms a 256 × 128 pixel texture, but the XML's final glyph row extends beyond its bounds. The mismatch and the malformed textual representation of the final symbol should be documented as unresolved resource inconsistencies until the original assets or related font files can be compared.
