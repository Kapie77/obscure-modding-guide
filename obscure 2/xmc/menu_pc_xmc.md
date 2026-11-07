# `menu_pc.xmc` --- Analysis

## Overview

`menu_pc.xmc` defines the PC main-menu interface and its navigation
structure. It includes two variants of the root menu (one with
`steam="0"` and one with `steam="1"`), new-game and load/save entries,
exit confirmation, general options, video and brightness settings, and a
substantial set of keyboard/controller configuration panels.

The file also defines delayed new-game transition panels, a message-box
border, a debug-menu file reference, and the global input mappings.

The XML describes menu structure, visual elements, string identifiers,
option identifiers, and action dispatch. It does not contain the
localized text represented by the `string_id` values or the
implementation of the actions.

## File-level structure

  Element                                            Count / value
  --------------------------- ------------------------------------
  Root element                                             `menus`
  Root attribute                                       `video="1"`
  Menu definitions                                              25
  Menu items                                                   109
  Input-offset declarations                          2 (`0`, `80`)
  Input mappings                                                11
  External menu files           1 (`menus\\debug.xml`, debug-only)

There are 25 `<menu>` elements, but only 24 distinct menu IDs because
`ROOT` is defined twice. The two `ROOT` definitions represent
alternative main-menu layouts.

### Menu item types

  Item type         Count Purpose indicated by the XML
  --------------- ------- -------------------------------------------------------
  `text`               78 Menu labels and selectable text entries
  `sprite`             22 Borders, copyright graphic, and preview placeholder
  `rect`                5 Solid-color visual backgrounds and brightness samples
  `textdelayed`         4 Text displayed progressively or after a delay

## Main menu

### `MAIN`

`MAIN` is a visible panel. It contains one sprite:

-   Texture: `m_copyright`
-   Rectangle: left `64.0`, top `420.0`, right `576.0`, bottom `484.0`
-   `rect_type="scale"`
-   `select="0"`

This is the only item declared directly inside `MAIN`.

### `ROOT` --- non-Steam variant

The first `ROOT` definition has:

-   `subtype="SUBP"`
-   `default="1"`
-   `visible="1"`
-   `steam="0"`
-   Panel bounds: left `25.0`, right `75.0`, top `50.0`, bottom `68.0`

It contains a border sprite and five text entries:

  String ID / label   Action   Destination
  ------------------- -------- -------------
  `04000009`          `show`   `NGME`
  `0400000A`          `show`   `LOD2`
  `0400000B`          `show`   `OPTN`
  `0400000C`          `show`   `EXIT`
  Literal `[DEBUG]`   `show`   `DMAI`

The debug entry has `debug="1"`. `DMAI` is referenced here, but no menu
with that ID is defined in this file; the debug menu file is separately
included through a debug-only `<menufile>` reference.

### `ROOT` --- Steam variant

The second `ROOT` definition also has `default="1"` and `visible="1"`,
but uses `steam="1"` and a slightly different vertical layout.

It contains a border sprite and six text entries:

  -----------------------------------------------------------------------
  String ID / label       Action                  Destination
  ----------------------- ----------------------- -----------------------
  `04000009`              `show`                  `NGME`

  `0400000A`              `show`                  `LOD2`

  `0400000B`              `show`                  `OPTN`

  `FFFFFF00`              `achievements`          No submenu ID; invokes
                                                  the achievements action

  `0400000C`              `show`                  `EXIT`

  Literal `[DEBUG]`       `show`                  `DMAI`
  -----------------------------------------------------------------------

The Steam variant adds an achievements entry and places the exit entry
after it. The XML does not identify the localized label associated with
`FFFFFF00`.

## New-game flow

### `NGME`

`NGME` is a submenu of `ROOT`. It contains a border sprite and two
selectable text entries:

  String ID    Action   Destination
  ------------ -------- -------------
  `0400000D`   `show`   `NGM1`
  `0400000E`   `show`   `NGM2`

These entries lead to two separate new-game transition panels.

### `NGM1`

`NGM1` is a panel parented to `MAIN`. It contains:

1.  A full-panel black rectangle (`bg_color="FF000000"`).
2.  A progressive text element using string ID `0C600008`, displayed
    with `show="progressive"` and `time="3000"`.
3.  A delayed text element using string ID `04000005`, displayed with
    `show="delayed"` and `time="4000"`.

The final text item has a `changeState` action that sets
`state="newGame"` when `valid` is received.

### `NGM2`

`NGM2` is another panel parented to `MAIN`, with the same black
background structure.

It contains:

1.  A progressive text element using string ID `0C600001` and
    `time="5000"`.
2.  A delayed text element using string ID `04000005` and `time="5000"`.

Its `changeState` action sets `state="newGame2"`.

The XML establishes two distinct new-game state transitions, but does
not explain the gameplay differences between `newGame` and `newGame2`.

## Load/save panel

### `LOD2`

`LOD2` is a submenu of `ROOT` with `class_name="load_save"` and
`preload="1"`.

Its panel geometry includes `x1="3.2"`, `x2="10"`, `y1="4"`, and
`dy="9"`. It contains three sprites:

-   A border using `m_border`, spanning the left portion of the panel.
-   A second `m_border` sprite positioned from `left="61.0"` to
    `right="100.0"`.
-   A `preview` sprite with an empty `texture` attribute, positioned in
    the right-hand area.

The preview sprite has `left="63.0"`, `top="5.0"`, `right="98.0"`, and
`bottom="95.0"`. The actual save/load slot behavior is not described by
these elements; it is presumably handled by the `load_save` class at
runtime.

## Exit confirmation

### `EXIT`

`EXIT` is a submenu of `ROOT`. It contains a border sprite and two text
entries:

  String ID    Action
  ------------ --------------------
  `04000028`   No action declared
  `0400001B`   `back`
  `0400001A`   `exitgame`

The `back` and `exitgame` actions are triggered by the `valid` message.
The XML does not provide the actual confirmation text.

## General options

### `OPTN`

`OPTN` is a submenu of `ROOT` using `class_name="options"`. It contains
a border sprite and six option entries:

  String ID    Option / action    Destination or behavior
  ------------ ------------------ -------------------------
  `0400000F`   `show`             `BRGT` --- brightness
  `04000024`   `show`             `VDEO` --- video
  `04000022`   `show`             `PAD1`
  `04000023`   `show`             `PAD2`
  `04000012`   `special="LTRG"`   Option `VIBR`
  `04000013`   `special="LTRG"`   Option `SUBT`

`PAD1` and `PAD2` are declared as child panels of `OPTN`, but contain no
items in this XML. Their behavior may be supplied by runtime code or
other resources; this file does not explain it.

### `BRGT` --- brightness

`BRGT` is a child panel of `OPTN` with `class_name="brightness"`. It
contains:

-   A border sprite.
-   A text label using string ID `0400000F`.
-   A full-panel black rectangle (`FF000000`).
-   Two sample rectangles:
    -   `FF030303`, positioned between 20--40% horizontally and 35--60%
        vertically.
    -   `FF060606`, positioned between 60--80% horizontally and 35--60%
        vertically.
-   A text item using string ID `0400001E` with `special="KSYM"`.

The `brightness` class name and the two near-black rectangles suggest a
brightness calibration screen. The XML does not specify the runtime
adjustment algorithm or the meaning of the `KSYM` special handler.

### `VDEO` --- video settings

`VDEO` is a child panel of `OPTN`. It contains a border sprite and three
entries:

  String ID    Special / option   Behavior
  ------------ ------------------ -------------------------
  `04000025`   `LTRG` / `VMOD`    Video mode option
  `04000026`   `LTRG` / `VDPT`    Video-depth option
  `04000027`   Text action        `applyvideo` on `valid`

The names `VMOD` and `VDPT` indicate video mode and video depth
settings. The final entry invokes `applyvideo`. Exact supported values
are not listed in this file.

## Controller and input configuration

### `PADM` --- controller settings hub

`PADM` is a child panel of `OPTN`. It contains a border sprite and eight
selectable entries:

  String ID    Special / option                     Destination
  ------------ ------------------------------------ -------------
  `14100008`   `EXCL`, `param="5"`, option `CTRL`   `PMCS`
  `14100001`   `EXCL`, `param="4"`                  `PMMC`
  `14100002`   `EXCL`, `param="0"`                  `PMMV`
  `14100003`   `EXCL`, `param="0"`                  `PMWS`
  `14100004`   `EXCL`, `param="0"`                  `PMAC`
  `14100005`   `EXCL`, `param="0"`                  `PMQI`
  `14100006`   `EXCL`, `param="0"`                  `PMIV`
  `14100007`   No `EXCL` attribute                  `DKCF`

The first seven entries open controller/input configuration panels. The
last opens the default-key configuration panel.

### `DKCF` --- default keys

`DKCF` contains a border sprite, a text item with string ID `14100031`,
and two selectable entries:

-   `0400001B` invokes `back`.
-   `0400001A` invokes `defkeys`.

Both actions are triggered by `valid`.

### `PMCS` --- controller selection

`PMCS` has `option="CTRL"` and five selectable entries. Each invokes
`setopt` with `id="CTRL"` and a different value:

    Item `param`   Value assigned to `CTRL`
  -------------- --------------------------
             `1`                        `1`
             `3`                        `3`
             `4`                        `4`
             `5`                        `5`
             `6`                        `6`

The available values skip `2`. The XML does not explain the meaning of
the numeric controller modes.

### `PMMC`

`PMMC` is declared as an empty child panel of `PADM`. It has no items in
this file.

### `PMMS` --- mouse settings

`PMMS` contains a border sprite and three `LTRG` option entries:

  String ID    Option
  ------------ --------
  `1410000A`   `MSIV`
  `1410000B`   `MSIH`
  `1410000C`   `MSSV`

These identifiers suggest mouse-related settings, but their exact labels
and effects are not defined in this XML.

### `PMCM` --- camera controls

`PMCM` contains five selectable entries, each using a `CKEY` action:

  String ID    Option
  ------------ --------
  `1410002C`   `CMUP`
  `1410002D`   `CMDW`
  `1410002E`   `CMLF`
  `1410002F`   `CMRG`
  `14100030`   `CMCT`

The option identifiers suggest camera movement and centering controls.
The XML does not define the actual key bindings.

### `PMMV` --- movement controls

`PMMV` contains four selectable `CKEY` entries:

  String ID    Option
  ------------ --------
  `1410000D`   `MVUP`
  `1410000E`   `MVDW`
  `1410000F`   `MVLF`
  `14100010`   `MVRG`

These identifiers suggest up, down, left, and right movement bindings.

### `PMWS` --- weapon switching controls

`PMWS` contains four selectable `CKEY` entries:

  String ID    Option
  ------------ --------
  `14100011`   `WSW1`
  `14100012`   `WSW2`
  `14100013`   `WSW3`
  `14100014`   `WSW4`

The identifiers suggest four weapon-switching bindings.

### `PMAC` --- action controls

`PMAC` contains nine selectable `CKEY` entries:

  String ID    Option   Additional attributes
  ------------ -------- -------------------------------
  `14100018`   `ACAC`   ---
  `14100019`   `ACCL`   ---
  `14100017`   `ACAP`   ---
  `1410001C`   `ACWK`   `special="EXCL"`, `param="1"`
  `1410001B`   `ACCC`   ---
  `1410001D`   `ACP2`   `special="EXCL"`, `param="3"`
  `14100016`   `ACLK`   ---
  `14100015`   `ACAK`   ---
  `1410001A`   `ACRL`   ---

The option codes identify configurable actions, but the exact localized
labels and gameplay meanings are not present in the XML.

### `PMQI` --- quick-item controls

`PMQI` contains four selectable `CKEY` entries:

  String ID    Option
  ------------ --------
  `1410001E`   `QIUS`
  `1410001F`   `QINX`
  `14100020`   `QIPR`
  `14100021`   `QIMN`

The option identifiers suggest quick-item selection or navigation
bindings.

### `PMIV` --- inventory controls

`PMIV` contains six selectable `CKEY` entries:

  String ID    Option   Additional attributes
  ------------ -------- -------------------------------
  `14100022`   `IVOP`   ---
  `14100024`   `IVPR`   ---
  `14100023`   `IVNX`   ---
  `14100025`   `IVWP`   `special="EXCL"`, `param="3"`
  `14100026`   `IVIT`   `special="EXCL"`, `param="3"`
  `14100027`   `IVTM`   `special="EXCL"`, `param="3"`

The option identifiers suggest inventory opening, navigation, and
category selection. Their exact meanings are not specified by the XML.

## Message box

### `MBPO`

`MBPO` uses `class_name="mb"`, has `markers="1"`, and uses selection
color `FFFDDEA9`. It contains one border sprite using `m_border`,
positioned with left `8.0`, right `92.0`, top `50.0`, and bottom `90.0`.

No message text or actions are defined in this menu.

## Debug menu reference

The file includes:

``` xml
<menufile path="menus\debug.xml" debug="1" />
```

This declares an external debug menu resource. Its contents are not part
of `menu_pc.xmc` and must be analyzed separately in `debug.xmc` or the
corresponding XML resource.

## Input configuration

Two input offsets are declared: `0` and `80`.

The 11 input mappings are:

      ID Message             Offset     `next_time`   `just_pressed`
  ------ ---------- --------------- --------------- ----------------
     `1` `up`         Not specified           `300`              `0`
     `2` `down`       Not specified           `300`              `0`
     `3` `left`       Not specified           `300`              `0`
     `4` `right`      Not specified           `300`              `0`
    `27` `up`         Not specified           `500`              `0`
    `29` `down`       Not specified           `500`              `0`
    `30` `left`       Not specified           `500`              `0`
    `28` `right`      Not specified           `500`              `0`
     `9` `valid`      Not specified   Not specified    Not specified
    `10` `cancel`               `0`   Not specified    Not specified
    `35` `cancel`              `80`   Not specified    Not specified

The four directional mappings with IDs `1`--`4` use a repeat interval of
`300`; the second directional set (`27`--`30`) uses `500`. Both sets
have `just_pressed="0"`. The confirmation mapping is `valid`;
cancellation is mapped twice, explicitly using offsets `0` and `80`.

Although the file declares input-offset values `0` and `80`, only the
two cancellation entries explicitly carry an `offset` attribute. The XML
does not label the physical keys or buttons represented by these numeric
IDs.

## Action inventory

The file contains 69 action elements:

  Action type        Count Role indicated by the XML
  ---------------- ------- -----------------------------------
  `CKEY`                32 Control/key binding entries
  `show`                24 Open another menu
  `setopt`               5 Set an option value
  `back`                 2 Return/back action
  `changeState`          2 Change game state
  `achievements`         1 Invoke achievements
  `exitgame`             1 Exit game
  `applyvideo`           1 Apply video settings
  `defkeys`              1 Restore/default key configuration

All listed actions are triggered by the `valid` message.

## Important observations and limitations

-   The two `ROOT` entries are alternative menu definitions
    distinguished by `steam="0"` and `steam="1"`. The Steam variant adds
    an achievements entry.
-   The menu hierarchy exposes separate areas for new game, load/save,
    exit, general options, video, brightness, and controller/input
    configuration.
-   Several panels (`PAD1`, `PAD2`, and `PMMC`) are empty in this XML.
    Their content or behavior may be supplied elsewhere or by runtime
    code; this file alone does not establish which.
-   `LOD2` relies on the `load_save` class, and `BRGT` relies on the
    `brightness` class. Their runtime behavior is not defined by the
    listed items alone.
-   Most visible labels are represented by numeric `string_id` values.
    Their actual text must be resolved from the game's
    localization/string resources.
-   Option codes such as `VIBR`, `SUBT`, `VMOD`, `VDPT`, `MVUP`, and
    `WSW1` are preserved as identifiers. Their meanings beyond what
    their names suggest are not formally defined here.
-   `DMAI` is referenced by the debug entry but is not defined as a menu
    in this file. The separate debug resource is included through a
    debug-only menu-file reference.

## Summary

`menu_pc.xmc` defines the PC main-menu system and its
options/configuration interface. It contains 25 menu definitions (24
distinct IDs, with two alternative `ROOT` definitions), 109 menu items,
69 actions, two input-offset declarations, and 11 input mappings.

Its contents cover the main menu, Steam-specific achievements access,
new-game transitions, load/save presentation, exit confirmation,
brightness and video settings, controller selection, and
keyboard/mouse/gameplay control bindings. The XML provides the interface
structure and action identifiers, while localized strings, physical
input labels, save-slot behavior, and most runtime option semantics
depend on other resources or game code.
