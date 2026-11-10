# `save.xmc` --- Save Interface

## Overview

`save.xmc` defines a compact save-interface resource. It contains three
menu definitions:

-   `SBGD`: the visible background panel.
-   `SFLO`: the save-list panel, using the `load_save` class.
-   `SPOP`: a message-box panel, using the `mb` class.

The file also declares three input-offset contexts and seven input
mappings for navigation, confirmation, and cancellation.

## Structural inventory

  ------------------------------------------------------------------------
  Element                                      Count Notes
  --------------------- ---------------------------- ---------------------
  `<menu>` definitions                             3 `SBGD`, `SFLO`,
                                                     `SPOP`

  Distinct menu IDs                                3 No duplicate IDs

  `<item>` elements                                5 One background
                                                     sprite, three
                                                     save-panel sprites,
                                                     one message-box
                                                     border

  `<input_offset>`                                 3 Values `40`, `0`, and
  elements                                           `80`

  `<input>` mappings                               7 Navigation,
                                                     confirmation, and
                                                     cancellation
  ------------------------------------------------------------------------

## Menu definitions

### `SBGD` --- Background

``` xml
<menu type="panel" id="SBGD" visible="1">
  <item type="sprite" texture="m_load.bmp"
        left="0.0" top="0.0" right="100.0" bottom="100.0"
        select="0" />
</menu>
```

This is a visible panel (`visible="1"`) containing one sprite that fills
the full 0--100 coordinate area. Its texture is `m_load.bmp`.

The XML identifies it as the background panel, but does not specify any
animation or runtime behavior for the texture.

### `SFLO` --- Save-list panel

``` xml
<menu parent_id="SBGD" type="panel" load="0" id="SFLO"
      sel_color="FFFDDEA9" class_name="load_save" preload="0"
      x1="3.2" x2="10" y1="4" dy="9"
      left="8.0" top="32.0" right="92.0" bottom="73.0">
```

`SFLO` is a child of `SBGD` and uses the `load_save` class. It has
`load="0"` and `preload="0"`. Its selection color is `FFFDDEA9`.

The panel contains three sprites:

  -----------------------------------------------------------------------
  Sprite class      Texture           Position / size   Apparent role
                                      attributes        from XML
  ----------------- ----------------- ----------------- -----------------
  `border`          `m_border`        `left=0`,         Left portion of
                                      `top=0`,          the panel border
                                      `right=60`,       
                                      `bottom=100`;     
                                      `width=32`,       
                                      `height=32`       

  `border`          `m_border`        `left=61`,        Right portion of
                                      `top=0`,          the panel border
                                      `right=100`,      
                                      `bottom=100`;     
                                      `width=32`,       
                                      `height=32`       

  `preview`         `m_save0210`      `left=63`,        Save-preview
                                      `top=5`,          image area
                                      `right=98`,       
                                      `bottom=95`;      
                                      `width=32`,       
                                      `height=32`       
  -----------------------------------------------------------------------

The panel also declares layout-related attributes `x1="3.2"`, `x2="10"`,
`y1="4"`, and `dy="9"`. Their exact interpretation is not defined in
this XML.

The `load="0"` attribute is recorded as-is; the file alone does not
establish the complete save/load logic or the meaning of every internal
`load_save` class setting.

### `SPOP` --- Message box

``` xml
<menu id="SPOP" class_name="mb" sel_color="FFFDDEA9"
      markers="1" left="8.0" top="32.0" right="92.0" bottom="73.0">
  <item type="sprite" class_name="border" texture="m_border"
        width="32" height="32"
        left="0.0" top="0.0" right="100.0" bottom="100.0"
        select="0" />
</menu>
```

`SPOP` uses the `mb` class and has the same selection color as `SFLO`.
It declares `markers="1"` and contains one full-area border sprite using
`m_border`.

No text item or message string is defined inside this menu. The actual
message content, conditions for displaying it, and behavior of the
message box are not specified in this file.

## Input configuration

### Input offsets

The file declares three input-offset values, in this order:

    Declaration   Value
  ------------- -------
              1    `40`
              2     `0`
              3    `80`

These are three declared input contexts. The XML does not explicitly
associate each offset with a particular menu.

### Input mappings

    Input ID Message    Additional attributes
  ---------- ---------- ---------------------------------------
         `1` `up`       `just_pressed="0"`, `next_time="500"`
         `2` `down`     `just_pressed="0"`, `next_time="500"`
        `27` `up`       `just_pressed="0"`, `next_time="500"`
        `29` `down`     `just_pressed="0"`, `next_time="500"`
         `9` `valid`    None declared
        `10` `cancel`   None declared
        `24` `cancel`   None declared

The mappings provide two pairs of navigation inputs (`up` and `down`),
one confirmation input (`valid`), and two cancellation inputs
(`cancel`).

For the four navigation mappings, `just_pressed="0"` and
`next_time="500"` are explicitly declared. The confirmation and
cancellation mappings have no additional attributes in the XML.

## Interpretation and limitations

The XML supports the following conclusions:

-   The resource contains a background panel, a save-list panel, and a
    message-box panel.
-   The save-list panel is identified by the `load_save` class and
    includes two border sprites plus a preview sprite.
-   The preview uses the texture `m_save0210`.
-   The message box uses the `mb` class and a border sprite.
-   The declared controls cover vertical navigation, confirmation, and
    cancellation.

The XML does **not** establish:

-   How save slots are enumerated or populated.
-   Where save data is stored, or how saving is performed.
-   Whether `load="0"` selects a save-only mode or has another
    class-specific meaning.
-   The contents of the save preview or the data used to generate it.
-   The text or conditions associated with `SPOP`.
-   The exact runtime meaning of the layout attributes or input-offset
    values.

These points would require additional resources or runtime/code
analysis.

## Conclusion

`save.xmc` is the layout and input-definition resource for a
save-related interface. Its main functional panel is `SFLO`, which uses
the `load_save` class and provides a preview region; `SBGD` supplies the
background, while `SPOP` defines a reusable message-box frame. The file
declares seven input mappings across three input-offset contexts, but
does not expose the underlying save-data operations or message text.
