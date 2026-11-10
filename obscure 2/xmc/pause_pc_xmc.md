# `pause_pc.xmc` --- PC Pause Menu System

## Overview

`pause_pc.xmc` defines the PC pause-menu interface and several panels
that can be opened from it. The resource includes two variants of the
main pause menu, distinguished by the `steam` attribute, as well as
confirmation, save/load, options, video, brightness, and
controller-configuration panels.

The XML describes menu layout, string identifiers, navigation actions,
option identifiers, and input mappings. It does not contain the
localized text represented by the string IDs or the runtime
implementation of the associated actions.

## Structural inventory

  ------------------------------------------------------------------------
  Element                                      Count Notes
  --------------------- ---------------------------- ---------------------
  `<menu>`                                        23 22 distinct menu IDs;
                                                     `PAUS` is defined
                                                     twice

  `<item>`                                       105 76 text, 24 sprite, 3
                                                     rectangle, and 2
                                                     `text2p` items

  `<action>`                                      69 Includes actions
                                                     nested inside items
                                                     and menu-level
                                                     actions

  `<input_offset>`                                 3 Values `40`, `0`, and
                                                     `80`

  `<input>`                                       12 Navigation,
                                                     validation, and
                                                     cancellation mappings
  ------------------------------------------------------------------------

### Action types

  Action type        Count Purpose indicated by the XML
  ---------------- ------- ------------------------------------------
  `CKEY`                32 Controller/key binding entries
  `show`                20 Opens another menu panel
  `setopt`               5 Sets an option value
  `resume_game`          4 Resumes gameplay
  `p2_leave`             2 Two-player leave action
  `back`                 2 Returns to the previous menu
  `achievements`         1 Opens or invokes the achievements action
  `changeState`          1 Changes game state to `main_menu`
  `applyvideo`           1 Applies video settings
  `defkeys`              1 Restores/defaults key bindings

## Menu definitions

### `MAIN`

A visible panel containing a single full-panel sprite using
`m_load.bmp`. The XML does not provide further behavior for this panel.

### `PAUS` --- main pause menu

The `PAUS` menu is defined twice:

-   **Steam variant (`steam="1"`):** visible by default, uses the `SUBP`
    subtype, and occupies the region from 15--85% horizontally and
    35--68% vertically. It contains a border sprite and seven text
    entries.
-   **Non-Steam variant (`steam="0"`):** also visible by default and
    uses the same general horizontal placement, but its bottom boundary
    is 62%. It contains a border sprite and six text entries.

Both variants provide these entries:

  String ID / label   Action          Destination or behavior
  ------------------- --------------- ------------------------------------
  `0C100001`          `resume_game`   Resumes gameplay
  `0C100002`          `p2_leave`      Two-player leave action (`text2p`)
  `0C100003`          `show`          Opens `LOAD`
  `0C100004`          `show`          Opens `OPTN`
  `0C100005`          `show`          Opens `BACK`

The Steam variant additionally contains:

-   `FFFFFF00` --- invokes `achievements`.
-   A `SAVE` text entry that opens the `SAVE` panel.

The non-Steam variant does not include the achievements entry. Both
variants contain the `SAVE` entry, marked `debug="1"`, and both define a
menu-level `resume_game` action for the `cancel` message.

The `SAVE` entry is positioned at coordinate 110 in both variants,
beyond the last ordinary pause-menu entry. Its `debug="1"` attribute
suggests it is intended as a debug-only entry, although the XML alone
does not establish how the runtime enforces that flag.

### `BACK` --- return/exit confirmation

A child panel of `PAUS`, with a border sprite and three text items:

-   `0C100006`: a non-selectable centered text item, likely the
    confirmation prompt.
-   `0400001B`: invokes `back`.
-   `0400001A`: invokes `changeState` with `state="main_menu"`.

The string contents are not included, so the exact wording of the prompt
and choices cannot be recovered from this file alone.

### `SAVE` and `LOAD` --- save/load panels

Both are child panels of `PAUS` and use the `load_save` class.

  Property          `SAVE`         `LOAD`
  ----------------- -------------- --------------
  `load`            `0`            `1`
  `preload`         `0`            `0`
  Class             `load_save`    `load_save`
  Preview texture   `m_save0210`   `m_save0210`

Each panel contains two border sprites and one preview sprite. The
preview uses the `preview` class and occupies the right-hand portion of
the panel. The XML does not define save-slot contents, slot count, or
the runtime save/load procedure.

### `MBPO`

A message-box menu using the `mb` class. It contains one border sprite
using `m_border`, positioned between 8--92% horizontally and 40--80%
vertically. No message text or buttons are defined in this menu.

### `OPTN` --- options menu

A child panel of `ROOT`, using the `options` class. It contains:

  String ID    Entry configuration   Destination / option
  ------------ --------------------- ----------------------
  `0400000F`   Text item             Opens `BRGT`
  `04000024`   Text item             Opens `VDEO`
  `04000022`   Text item             Opens `PAD1`
  `04000023`   Text item             Opens `PAD2`
  `04000012`   `special="LTRG"`      Option `VIBR`
  `04000013`   `special="LTRG"`      Option `SUBT`

The `PAD1` and `PAD2` destination panels are present as empty panel
definitions in this resource.

### `BRGT` --- brightness panel

A child panel of `OPTN` with `class_name="brightness"`. It contains:

-   A border sprite.
-   A text item using string ID `0400000F`.
-   A full-panel black rectangle (`FF000000`).
-   Two darker sample rectangles (`FF030303` and `FF060606`).
-   A text item using string ID `0400001E` and `special="KSYM"`.

The XML establishes the panel's brightness-related class and visual
samples, but does not specify the brightness algorithm or the meaning of
each sample value.

### `VDEO` --- video settings

A child panel of `OPTN` with a border sprite and three entries:

  String ID    Special / option   Behavior
  ------------ ------------------ ----------------------
  `04000025`   `LTRG`, `VMOD`     Video mode option
  `04000026`   `LTRG`, `VDPT`     Video depth option
  `04000027`   ---                Invokes `applyvideo`

The names `VMOD` and `VDPT` are option identifiers; the XML does not
define their available values.

### `PADM` --- controller configuration hub

A child panel of `OPTN`. It contains eight entries leading to
controller/input configuration panels:

  String ID    Option / parameter    Destination
  ------------ --------------------- -------------
  `14100008`   `CTRL`, `param="5"`   `PMCS`
  `14100001`   `param="4"`           `PMMC`
  `14100002`   `param="0"`           `PMMV`
  `14100003`   `param="0"`           `PMWS`
  `14100004`   `param="0"`           `PMAC`
  `14100005`   `param="0"`           `PMQI`
  `14100006`   `param="0"`           `PMIV`
  `14100007`   ---                   `DKCF`

Most entries use `special="EXCL"` and open their corresponding
subpanels.

### `DKCF` --- key defaults/confirmation panel

A child of `PADM`. It contains a border sprite, a non-selectable text
item (`14100031`), and two selectable actions:

-   `0400001B` invokes `back`.
-   `0400001A` invokes `defkeys`.

The string text is not present, so the precise wording of the prompt and
the `defkeys` operation's user-facing label cannot be established here.

### Controller and key-binding panels

The following panels contain entries with `option` identifiers and
`CKEY` actions. These appear to define configurable control bindings.

  ------------------------------------------------------------------------
  Menu                                       Entries Option identifiers
  --------------------- ---------------------------- ---------------------
  `PMCS`                                           5 `CTRL` values `1`,
                                                     `3`, `4`, `5`, and
                                                     `6`

  `PMMC`                                           0 Empty panel

  `PMMS`                                           3 `MSIV`, `MSIH`,
                                                     `MSSV`

  `PMCM`                                           5 `CMUP`, `CMDW`,
                                                     `CMLF`, `CMRG`,
                                                     `CMCT`

  `PMMV`                                           4 `MVUP`, `MVDW`,
                                                     `MVLF`, `MVRG`

  `PMWS`                                           4 `WSW1`, `WSW2`,
                                                     `WSW3`, `WSW4`

  `PMAC`                                           9 `ACAC`, `ACCL`,
                                                     `ACAP`, `ACWK`,
                                                     `ACCC`, `ACP2`,
                                                     `ACLK`, `ACAK`,
                                                     `ACRL`

  `PMQI`                                           4 `QIUS`, `QINX`,
                                                     `QIPR`, `QIMN`

  `PMIV`                                           6 `IVOP`, `IVPR`,
                                                     `IVNX`, `IVWP`,
                                                     `IVIT`, `IVTM`
  ------------------------------------------------------------------------

`PMCS` is a controller-selection panel: each of its five entries uses
`special="CTRL"` and invokes `setopt` with option ID `CTRL` and a
corresponding numeric value (1, 3, 4, 5, or 6).

`PMMS` uses `special="LTRG"` rather than `CKEY` actions, and its three
entries are option controls. `PMMC` is defined but has no child items.

The `PMCM`, `PMMV`, `PMWS`, `PMAC`, `PMQI`, and `PMIV` panels use `CKEY`
actions for their listed control identifiers. Some entries also carry
`special="EXCL"` and a `param` attribute; those values are retained as
configuration metadata in the XML.

## Input mappings

The resource declares three input offsets: `0`, `40`, and `80`.

    Offset   Input ID Message      `next_time`   `just_pressed`
  -------- ---------- ---------- ------------- ----------------
       ---          1 `up`                 300                0
       ---          2 `down`               300                0
       ---          3 `left`               300                0
       ---          4 `right`              300                0
       ---          9 `valid`              ---              ---
       ---         27 `up`                 500                0
       ---         29 `down`               500                0
       ---         30 `left`               500                0
       ---         28 `right`              500                0
         0         10 `cancel`             ---              ---
        40         10 `cancel`             ---              ---
        80         35 `cancel`             ---              ---

The first nine mappings have no explicit `offset` attribute. The three
cancellation mappings explicitly use offsets 0, 40, and 80. The XML does
not explain which physical devices or runtime contexts correspond to
each offset.

## Important observations and limitations

-   The pause menu has separate Steam and non-Steam definitions. The
    Steam version adds an achievements entry and uses a different
    vertical layout.
-   Both pause-menu variants include a `SAVE` entry marked `debug="1"`.
-   The pause menu supports resuming gameplay both through a selectable
    entry and through a menu-level `cancel` action.
-   The `BACK` panel distinguishes returning to the previous menu
    (`back`) from changing the game state to `main_menu`.
-   Save and load panels share the `load_save` class and preview
    texture, but use different `load` values.
-   The options system includes brightness, video, vibration, subtitles,
    and controller-related panels.
-   Several panels are placeholders or empty definitions (`PAD1`,
    `PAD2`, and `PMMC`).
-   String IDs are present, but localized strings are not included.
    Their displayed wording cannot be determined from this XML alone.
-   The XML describes UI structure and action identifiers; it does not
    reveal the internal implementation of save/load, achievements, video
    settings, controller handling, or game-state transitions.
