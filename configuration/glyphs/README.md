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
`font` is the font you want to use. If unspecified, it will use the Default Font in settings.yml at `Glyphs.default_font`\
Unless you need the Glyph for the Escape Menu, as this place only supports the `minecraft:default` font, to use a custom font to limit conflicts & unintended uses\
\
You can also set a `permission` towards your Glyph to limit who can use it.\
If unspecified, Nexo will use the default permission defined in settings.yml at `Glyphs.default_permission` . You can specify `<glyph_id>` or `<glyph_placeholder`> which Nexo will then replace for you

Glyphs can also have `placeholders` which can be used to make more chat-friendly use-cases\
This is defined as a list of strings and will let players use shorthands for a given Glyph

```yaml
heart:
  texture: default/chat/heart
  ascent: 8
  height: 8
  #font: namespace:fontname     Optional, unspecified uses font in settings.yml
  #permission: nexo.glyph.heart Optional, unspecified uses permission in settings.yml
  #placeholders:
  #  - "<3"
```

{% hint style="warning" %}
If your texture is above 256x256 resolution you need to either downscale it or make a [multi-bitmap-glyph.md](multi-bitmap-glyph.md "mention")
{% endhint %}

### How to use the Glyph

Nexo implements a custom MiniMessage tag for each glyph, which lets you use it more or less anywhere\
You can use \<glyph:glyphid> and it will display your glyph, naturally replace glyphid with your Glyphs ID. Above this would be `heart`\
This tag can then be used in tablists, scoreboards, titles, chat prefixes via LuckPerms or otherwise.\
It is advised to use the Glyph-Tag over raw unicodes whenever possible\


The Glyph-tag also have some optional arguments you can pass.\
For [multi-bitmap-glyph.md](multi-bitmap-glyph.md "mention")'s you can specify the index to display.\
For example if you make a 2x2 Glyph, you can do `<glyph:heart:2>` or `<glyph:heart:2..3>` to display only those parts of the Glyph.

If you want your Glyph to be colorable, you can do `<glyph:heart:colorable>` or `<glyph:heart:c>` \
This will make your Glyph accept any previous color that might apply, and not force it to white or normal

As of 1.21.4 there is also a new "shadow-color" tag, letting you change the color and alpha-value of the Glyphs-shadow\
You can use this by using the argument shadow, or s, like this; `<glyph:heart:shadow:#AARRGGBB>`&#x20;

All these arguments can be combined, letting you specify a specific Bitmap-Index, make it colorable and change the shadow

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
This applies to the vast majority of places you would want to use a glyph. If the tag does not work you can use the [PlaceholderAPI Placeholder](./#placeholderapi)\
\
To adjust the horizontal position of your texture/glyph in the inventory, use the shift-tag.\
For example; `<shift:-8>` for moving 8 pixels back, and `<shift:211>` for moving 211 pixels forward.

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

The placeholders can be used in chat by players with the required permission (if permission is specified, it is not mandatory).

## How to make glyphs tabcomplete?

Simply set `tabcomplete: true` in the chat-section. If not specified, this will default to `false`

By default tabcompletion will use the raw unicode. This only works for glyphs using the Default-font (used if none is specified). If you want it to use the chat placeholders, you can do so by disabling `unicode_completions` in settings.yml.

```yaml
myemoji:
  #font: minecraft:default
  tabcomplete: true
  placeholders:
    - "<3"
  permission: "nexo.emoji.heart"
```

## PlaceholderAPI

### What's my glyph placeholder?

The section name is the glyph id. In this example the glyph id is `heart`, the placeholder is `%nexo_glyphid%`, so in this example: `%nexo_heart%`\
Glyph-ID is the first line in any glyphs config, it is not the texturename or the placeholder. you can also do shifts using PAPI by doing `%nexo_shift_-8%` or `%nexo_shift_8%`&#x20;

Do note if the font of a Glyph isnt `minecraft:default` this will just default to using a Glyph-Tag, not unicodes
