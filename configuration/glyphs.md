---
description: How to add new glyphs to the game?
cover: https://i.imgur.com/T76ianD.png
coverY: 0
---

# 🌀 Glyphs

## What is a glyph?

A glyph is a textured unicode symbol. It can be used in any place text is rendered ingame (chat, item name, lore and more). They can be used to do very, very powerful things (custom inventories, extra bars) but their simplest use is to be emoji.

## Configuring a Glyph

You can then add your section to any YAML file from the glyphs directory.\
A glyph has a few main properties, `texture`, `ascent`, `height` and `font`\
The texture is the path and name of the texture file in the format of `namespace:path`\
`height` is the scale of your glyph, height must also never be lower than ascent.\
`ascent` is the vertical offset of your glyph, and must be equal or lower than height.\
`font` is the font you want to use. If unspecified, `minecraft:default` will be used.\
It is generally adviced to set a font unless you want to use the glyph in Esc Menu, as that only accepts the default font.

```yaml
heart:
  texture: default/chat/heart
  ascent: 8
  height: 8
  font: namespace:fontname
```

### Multi-Bitmap glyphs

If you have a texture consisting of several emotes or a texture larger than the allowed 256x256, you can make it a multi-bitmap.\
This means you can, tie several unicodes to one image.\
In your glyph you can specify an amount of rows and columns your glyph needs.\
This will make nexo assign unicodes based on your needs.

Example for using a 512x512 texture:

{% code lineNumbers="true" fullWidth="false" %}
```yaml
myglyph:
  #texture: required/ui/menu_items
  #ascent: 37
  #height: 256
  rows: 2     # Tells Nexo this glyph should have 2 rows when assigning unicodes/chars
  columns: 2  # Tells Nexo this glyph should have 2 columns when assigning unicodes/chars
```
{% endcode %}

This will make nexo assign 4 unicodes for this glyph, which will be displayed when used.

It should be noted that some cases newlines are not supported. An example is in lore, where it would not correctly align your glyph. A workaround is by using an "range index" in your glyph-tag. Example for using in lore of your NexoItem:

```yaml
myitem:
  lore:
    - "<glyph:myglyph:1..2>"
    - "<glyph:myglyph:3..4>"
```

This would correctly align your glyph in lore. In cases where newlines are supported, you dont need to specify such a range. Nexo would by default append that to the text and align it.

### Reference Glyphs

Reference-glyphs are used when you want to "reference" a part of a Multi-Bitmap Glyph.\
For example if you have a multi-bitmap glyph with 10 emojis, you can reference a specific one like follows

```yaml
multi_bitmap:
  texture: spritesheet
  rows: 2
  columns 5

#index is the row and column number
first_emoji:
  reference: multi_bitmap
  index: 1
...
tenth_emoji:
  reference: multi_bitmap
  index: 10
```

### Custom GUIs

With Nexo-glyphs you can create custom textured GUI's\
Nexo does not handle the GUI-Inventory itself, only the visual part of it.\
Simply make a glyph like shown below:

```yaml
customshop:
  texture: required/ui/menu_items
  #font: minecraft:my_font      # Optional, defaults to minecraft:default
  ascent: 37
  height: 256
```

Then in the Inventory-Title you just put `<glyph:glyphid>` and Nexo will handle the rest.\
This applies to the vast majority of places you would want to use a glyph. If the tag does not work you can use the [PlaceholderAPI Placeholder](glyphs.md#placeholderapi)\
\
To adjust the horizontal position of your texture/glyph in the inventory, use the shift-tag.\
For example;  `shift:-8>` for moving 8 pixels back, and `<shift:211>` for moving 211 pixels forward.

### Emoji List

To make a glyph appear under `/nexo emojis` you need to specify that it is one, like below.\
If not specified, this will default to `false`

```yaml
heart:
  texture: default/chat/heart
  is_emoji: true
```

It will also, by default, only show emojis the player has the permission for.\
In `settings.yml` you can toggle the `only_show_emojis_with_permission` setting.\
This will show all emojis to every player, and adds a hover-message indicating if they have permission or not. ![img](https://cdn.discordapp.com/attachments/758785982005903431/1002564595099111474/unknown.png)

## How to use it in the chat?

You need to add a chat subsection to your glyph section:

```yaml
chat:
  placeholders:
    - "<3"
  permission: "nexo.emoji.heart"
```

The placeholders can be used in chat by players with the required permission (if permission is specified, it is not mandatory).

If it does not format your glyph in chat, change the `chat-handler` in settings.yml, as your chat-plugin is likely using `LEGACY` logic.

## How to make glyphs tabcomplete?

Simply set `tabcomplete: true` in the chat-section. If not specified, this will default to `false`&#x20;

By default tabcompletion will use the raw unicode. This only works for glyphs using the Default-font (used if none is specified). If you want it to use the chat placeholders, you can do so by disabling `unicode_completions` in settings.yml.

```yaml
myemoji:
  #font: minecraft:default
  chat:
    tabcomplete: true
    placeholders:
      - "<3"
    permission: "nexo.emoji.heart"
```

## PlaceholderAPI

### What's my glyph placeholder?

The section name is the glyph id. In this example the glyph id is `heart`, the placeholder is `%nexo_glyphid%`, so in this example: `%nexo_heart%`\
Glyph-ID is the first line in any glyphs config, it is not the texturename or the placeholder.

### How do I use this in Prefixes / Luckperms

To add a glyph to a luckperms prefix, commonly to display ranks, simply add `%nexo_glyphid%` to your prefix solution of choice.\
For example, if using LuckPerms, you can use the command: `/lp group default meta setprefix %nexo_glyphid%` and it will replace it with the glyph.\
Because most plugins only parse the placeholders one time, the %luckperms\_prefix% will not be parsed again.\
You will most likely need to get the Utils-Expansion for PlaceholderAPI aswell.\
To get this, go to [this link](https://api.extendedclip.com/media/Utils-Expansion-1.0.1.jar), and place it in your plugins/PlaceholderAPI/expansions folder.\
Then in your plugin of choice use `%utils_parse:2_luckperms_prefix%` to parse the prefix again.\
\
**Keep in mind** your chatplugin must support PlaceholderAPI for this to work.\
If this does not work for whatever reason, you can always use the raw unicode from your glyph-config's `char`-property

### How do I use a glyph in name/lore of an item?

Any glyph can be used in name and lore of your item configurations, by using `<glyph:glyphid>`
