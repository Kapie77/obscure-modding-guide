# `mc.xmc` --- Analysis

## Overview

`mc.xmc` defines a small interface related to the memory-card system. It
declares a main panel using the `check_mc` class, a message-box menu
using the `mb` class, one border sprite, and input mappings for
navigation, confirmation, and cancellation.

The XML describes the menu layout and input configuration. It does not
specify the exact memory-card operation performed or the message
displayed to the user.

## Menu definitions

The file contains two menu definitions:

  ------------------------------------------------------------------------
  ID                Type              Class             Configuration
  ----------------- ----------------- ----------------- ------------------
  `MAIN`            `panel`           `check_mc`        Initially visible
                                                        (`visible="1"`).

  `MCMB`            Not specified     `mb`              Message-box menu
                                                        with selection
                                                        color `FFFDDEA9`.
  ------------------------------------------------------------------------

### `MAIN`

The main menu is declared as a panel with `class_name="check_mc"`. Its
`visible` attribute is set to `1`.

### `MCMB`

`MCMB` uses the `mb` class and defines the selection color `FFFDDEA9`.
It contains one visual element:

  Attribute      Value
  -------------- ------------
  Element type   `sprite`
  Class          `border`
  Texture        `m_border`
  Width          `32`
  Height         `32`
  Left           `8.0`
  Top            `30.0`
  Right          `92.0`
  Bottom         `70.0`
  Select         `0`

The XML identifies the sprite and its layout attributes, but does not
provide the texture asset itself.

## Input offsets

Two input offsets are declared:

    Offset value Context
  -------------- ----------------------
             `0` First input context
            `80` Second input context

The XML does not explicitly associate individual mappings with a named
context; it only lists the offsets and input entries in sequence.

## Input mappings

The file defines seven input mappings:

      ID Message        `next_time`   `just_pressed`
  ------ ---------- --------------- ----------------
     `1` `up`                 `500`              `0`
     `2` `down`               `500`              `0`
    `27` `up`                 `500`              `0`
    `29` `down`               `500`              `0`
     `9` `valid`      Not specified    Not specified
    `10` `cancel`     Not specified    Not specified
    `24` `cancel`     Not specified    Not specified

The four navigation mappings (`up` and `down`) specify `next_time="500"`
and `just_pressed="0"`. The confirmation and cancellation mappings do
not define these attributes.

## Summary

`mc.xmc` contains:

-   **2** menu definitions (`MAIN` and `MCMB`).
-   **1** visual element: the `m_border` sprite.
-   **2** input-offset declarations (`0` and `80`).
-   **7** input mappings for upward/downward navigation, confirmation
    (`valid`), and cancellation (`cancel`).

The `check_mc` and `mb` class names suggest a memory-card check or
confirmation interface. However, the XML alone does not establish the
exact operation, runtime behavior, or displayed message.
