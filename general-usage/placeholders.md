---
description: All placeholders and tags Nexo provides, both through PlaceholderAPI and its own systems
---

# 🏷️ Placeholders

Nexo uses two kinds of placeholders.\
PlaceholderAPI placeholders like `%nexo_heart%` are for showing Nexo content in other plugins.\
Everything written with `<>`, like `<glyph:heart>` or `<item_id>`, is Nexo's own and works in Nexo configs and any text Nexo formats.

## PlaceholderAPI

If [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) is installed, Nexo registers its `nexo` expansion automatically.

| Placeholder                   | Returns                                                                                   |
| ----------------------------- | ----------------------------------------------------------------------------------------- |
| `%nexo_<glyphid>%`            | The glyph with that ID, see [Glyph Placeholder](#glyph-placeholder)                       |
| `%nexo_shift_<pixels>%`       | A shift of that many pixels. Use a negative number to shift left, like `%nexo_shift_-8%`  |
| `%nexo_pack_hash%`            | The hash of the current Nexo ResourcePack. Stays unresolved until the pack is generated   |
| `%nexo_multipack_<template>%` | `true` if the player has that [MultiPack](../configuration/resourcepack/multipack-feature.md) template enabled, otherwise `false` |

### Glyph Placeholder

The glyph ID is the name of the glyph section in your config, not its texture or [placeholders](#glyph-placeholders).

Glyphs using the `minecraft:default` font return their raw unicode, which works anywhere.\
Glyphs using any other font return a `<glyph:glyphid>` tag instead.\
Nexo turns the tag into the glyph when the text is sent to the player, as long as [formatting](../configuration/plugin-settings.md) is enabled wherever it shows up.

{% hint style="info" %}
If you use [TAB](https://www.spigotmc.org/resources/tab-1-5-1-21.57806/), Nexo registers every `%nexo_<glyphid>%` in TAB directly.\
They return the finished glyph, so they work in the tablist, nametags and scoreboards without Nexo having to format anything
{% endhint %}

### PlaceholderAPI Tag

The `<papi>` tag lets you use any PlaceholderAPI placeholder from any plugin in Nexo text.\
`<papi:player_name>` and `<placeholderapi:player_name>` both work, and the `%` around the placeholder are optional.\
Whatever the placeholder returns is parsed as MiniMessage, so colors and tags in it are formatted too.

```yaml
my_item:
  itemname: "<gold><papi:player_name>'s Sword"
  lore:
    - "<gray>Level: <white><papi:%player_level%>"
    - "<gray>Balance: <green><papi:vault_eco_balance_formatted>"
```

You can also put several placeholders in one tag, `<papi:player_name:player_level>` shows both right after each other.

Placeholders are resolved when the text is sent, for each player separately.\
In item names and lore, everyone sees their own value, and it updates whenever the item is sent to them again.

#### Permission

Outside item names and lore, the tag needs the `nexo.papi` permission.\
In chat the sender needs it, and the placeholder resolves for the sender.\
Everywhere else the player seeing the text needs it.\
Without it, the tag is shown as plain text.

Item names and lore from your item configs skip this check, since they are written by you and not by players.\
They only need `Plugin.formatting.items.itemname` and `Plugin.formatting.items.lore` enabled in settings.yml, which they are by default.

{% hint style="warning" %}
Only give `nexo.papi` to players you trust.\
They can put any placeholder in chat, and everyone will see what it resolves to
{% endhint %}

## Nexo Tags

These tags work in all Nexo configs, like item names, lore and messages.\
They also work in text from other plugins, wherever Nexo [formats](../configuration/plugin-settings.md) it.

| Tag                                | Description                                                                          |
| ---------------------------------- | ------------------------------------------------------------------------------------ |
| `<glyph:glyphid>` or `<g:glyphid>` | Shows a glyph, see the arguments below                                               |
| `<shift:pixels>` or `<s:pixels>`   | Moves the text after it by that many pixels. Use a negative number to move it left   |
| `<papi:placeholder>`               | Shows a PlaceholderAPI placeholder, see [PlaceholderAPI Tag](#placeholderapi-tag)    |
| `<prefix>`                         | The Nexo prefix from your language file                                              |

You can add these arguments to the glyph tag, in any order

| Argument           | Description                                                                                                   |
| ------------------ | ------------------------------------------------------------------------------------------------------------- |
| `colorable` or `c` | The glyph takes the color of the text around it. Without this it is always white                              |
| `shadow` or `s`    | Gives the glyph a shadow. You can add a color after it, like `<glyph:heart:shadow:#AARRGGBB>`                 |
| A number or range  | Only shows those parts of a [Multi-Bitmap Glyph](../configuration/glyphs/multi-bitmap-glyph.md), like `<glyph:heart:2>` or `<glyph:heart:2..3>` |

When players use these tags themselves, like in chat, they need permission for them.\
`<glyph>` needs the permission of that glyph, and `<shift>` needs `nexo.shift`.\
Without it, the tag is shown as plain text.

To show a tag as plain text on purpose, put a `\` in front of it, like `\<shift:8>`.

## Glyph Placeholders

Glyphs can have their own placeholders, which are plain words that get replaced with the glyph.\
They need no tag, so they are mostly used for emojis in chat, like typing `:heart:` or `<3`.

```yaml
heart:
  texture: default/chat/heart
  placeholders:
    - ":heart:"
    - "<3"
  permission: nexo.emoji.heart
```

You can also write `placeholder`, with a single string or a list.\
Players need the permission of the glyph for their placeholders to be replaced.\
A `\` in front, like `\<3`, keeps it as plain text.

A [Reference Glyph](../configuration/glyphs/reference-glyph.md) uses the placeholders of the glyph it references, unless you give it its own.

### Placeholders in settings.yml

| Setting                     | Placeholders                                                                              |
| --------------------------- | ----------------------------------------------------------------------------------------- |
| `Glyphs.default_permission` | `<glyphid>` for the glyph ID. Defaults to `nexo.glyphs.<glyphid>`                         |
| `Glyphs.hover_text`         | `<glyph_id>` for the glyph ID, and `<glyph_placeholder>` for its first placeholder        |

## Item Template Placeholders

When an item uses an [ItemTemplate](../configuration/items/#itemtemplate), these placeholders in the template are filled in with the values of that item.

| Placeholder             | Replaced with                                                           |
| ----------------------- | ----------------------------------------------------------------------- |
| `<item_id>`             | The ID of the item                                                      |
| `<item_id_capitalized>` | The ID as a name, so `ruby_sword` becomes `Ruby Sword`                  |
| `<lore>`                | The lore of the item                                                    |
| `<model>`               | `Pack.model` of the item, or the item ID if it has none                 |
| `<parent>`              | `Pack.parent_model` of the item, or `item/generated` if it has none     |
| `<texture>`             | `Pack.texture` of the item                                              |

If `<lore>` or `<texture>` is a list entry on its own, it is replaced with every line the item has.\
If the item has none, the entry is removed.

```yaml
template_item:
  itemname: "<gold><item_id_capitalized>"
  lore:
    - "<gray>A fine weapon"
    - "<lore>"
  Components:
    item_model: nexo:<item_id>

ruby_sword:
  template: template_item
  material: DIAMOND_SWORD
  lore:
    - "<red>Forged from rubies"
```

`ruby_sword` ends up named `Ruby Sword`, with the item model `nexo:ruby_sword` and both lore lines.

## Action Placeholders

### ClickActions

[ClickActions](../mechanics/clickaction-mechanic.md) on furniture and custom blocks, and the actions of the [Custom Mechanic](../mechanics/custom-mechanic.md), can use

* `<player>` for the name of the player
* Any PlaceholderAPI placeholder, like `%player_level%`, resolved for that player

```yaml
      clickActions:
        - actions:
            - "[console] give <player> diamond 1"
            - "[message] <green>You are level %player_level%!"
```

### Commands Mechanic

The [Commands Mechanic](../mechanics/all-mechanics.md#commands) uses `<player>` for the name of the player using the item.

```yaml
myitem:
  Mechanics:
    commands:
      console:
        - "give <player> diamond 1"
```

## Message Placeholders

The messages in `plugins/Nexo/messages` have placeholders like `<player>`, `<amount>` or `<item>`.\
Each message only has the placeholders it uses by default, so you can move them around but not add new ones.\
`<prefix>` and the [Nexo Tags](#nexo-tags) work in every message.
