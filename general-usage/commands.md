---
description: A simple explanation to use the plugin commands
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966827022758330398/unknown.png
coverY: 0
---

# ⌨️ Commands

## 📋 Getting Started

All the nexo-commands can be found under `/nexo` or it's aliases `/n` `/nx`

## 🎁 Getting/Removing items

### 📦 Nexo Inventory

The main benefit of this method is that it allows you to see all the items at the same time in categories based on your `Nexo/items/filename.yml`\
You can grab copies of items here but cannot give it to other players.

#### Usage: `/nexo inventory` or `/nexo inv`

#### Permission: `nexo.command.inventory`

### 🎯 Give Item

This command will be mainly useful if you want to give an item to another player or when you want to automate the give

#### Usage: `/nexo give <item> [amount] [player]`

#### Permission: `nexo.command.give`

### 🫳 Drop Item

This command will be useful if you want to drop an item to another player

#### Usage: `/nexo drop <item> [amount] [player]`

#### Permission: `nexo.command.drop`

### 🫴 Take Item

This command will be useful if you want to remove an item from a player

#### Usage: `/nexo take <item> [player]`

#### Permission: `nexo.command.take`

### :printer: Dump Item

This command is useful for debugging a NexoItem or held item to find the Data & Components on it

#### Usage: `/nexo dumpitem <itemid>`

#### Permission: `nexo.command.dumpitem`

***

## 🎨 Dyeing Items

This command allows you to dye the item in your hand, whether it's a dyeable Nexo item or just a normal dyeable item.

#### Usage: `/nexo dye <color>`

{% hint style="info" %}
`color` can be dye names (red, green), rgb (`0,255,0` for pure green), or hex (`0xFF0000` or `#00FFFF`)
{% endhint %}

#### Permission: `nexo.command.dye`

***

## 🔧 Recipe Commands

This command allows you to add new recipes to the configuration directly from the game using recipes builder. For more information on how to use it, see [Recipes](recipes.md).

#### Usage:

```yaml
/nexo recipe builder <type>    # Start building a new recipe
/nexo recipe save <name>       # Save your recipe
/nexo recipe show all          # See all your recipes
/nexo recipe show <recipe>     # Check a specific recipe
```

#### Permission: `nexo.command.recipes`

***

## 📩 Manual Pack Sending

This command allows you to send the pack to a group of players.\
Useful if the automatic sending failed or for testing

#### Usage: `/nexo pack <player>`

#### Permission: `nexo.command.pack`

***

## ⬆️ Updating Items and Furnitures

This command allows you to update furnitures and items.\
Useful if the auto update failed or if you disabled it in settings

#### Usage:

```yaml
/nexo update furniture <radius>   # Update furniture in a radius
/nexo update item <player>        # Update the Nexo items in a players inventory
```

#### Permission: `nexo.command.update`

***

## 🔍 Item Info

This command allows you to print general info about a Nexo Item for debugging.\
An example of the output:

```yaml
ItemID: my_cool_item                 # this is the ID of the item
CustomModelData: 1000                # the custommodeldata of the item
Material: PAPER                      # the material used for the item
Model Name: minecraft:my_cool_item   # the name of the model, in the final pack you can find this in minecraft/models/my_cool_item.json
```

#### Usage: `/nexo iteminfo <itemid>`

#### Permission: `nexo.command.iteminfo`

## 🔍 Glyph Info

This command allows you to print general info about a Nexo Glyph for debugging.\
An example of the output:

```yaml
GlyphID: required                          # this is the ID of the glyph
Texture: minecraft:required/exit_icon.png  # the texture path of the glyph
Font: minecraft:default                    # the font that the glyph uses
Unicode: ꐏ                                 # the character used for displaying the glyph (you should use <glyph:id>)
```

#### Usage: `/nexo glyphinfo <glyphid>`

#### Permission: `nexo.command.glyphinfo`

## 🟩 Block Info

This command allows you to print general info about a Nexo Block for debugging.\
An example of the output for a noteblock:

```yaml
ItemID: my_cool_block  # this is the ID of the item that the block is tied to
Intrument: PIANO       # this is the instrument the noteblock uses
Note: 1                # the note
Powered: false         # the powered state
```

this is different for other block types

#### Usage: `/nexo blockinfo <iteminfo>`

#### Permission: `nexo.command.blockinfo`

***

## 🙂 Emoji List

This command opens a book with all the emojis (glyphs with `is_emoji: true`).

#### Usage: `/nexo emojis`

#### Permission: `nexo.command.emojis`

***

## 🔄 Reload

This command allows you to reload Nexo configurations.\
Reloading items updates any changes you might have made, and updates all old copies players might have.\
Reloading pack regenerates the resourcepack, and if `Pack.dispatch.send_on_reload` is enabled in `settings.yml`, will be dispatched to all players.

#### Usage

```yaml
/nexo reload           # Refresh everything - items, recipes, and pack
/nexo reload items     # Just update items
/nexo reload pack      # Rebuild and resend the resource pack
/nexo reload recipes   # Reload recipe configurations
/nexo reload configs   # Reload configs
/nexo reload dialogs   # Reload Dialog configs (new dialogs require a restart)
```

#### Permission: `nexo.command.reload`

***

## 🐛 Debug Mode

This command just toggles the debug-state of Nexo.\
In case you run into a bug or an error, you might be asked to toggle this to provide support with a more full error-log of the bug.

#### Usage: `/nexo debug`

#### Permissions: `nexo.command.debug`

***

## ℹ️ Nexo Version

This command simply shows you the version of Nexo.\
If using devbuilds, we might ask you to give us the full jar-file name.

#### Usage: `/nexo version`

#### Permissions: `nexo.command.version`

***

## ❌ Reset Custom Model data

This command deletes the custom\_model\_data from all of your Nexo Items.\
Mainly useful for swapping Nexo to a "ItemModel" based system for 1.21.4+ servers.\
You can get more info about the difference between ItemModels and CustomModelDatas, and why ItemModels are the recommended choice at [itemmodels-vs.-custommodeldata.md](faq/itemmodels-vs.-custommodeldata.md "mention")

#### Usage: `/nexo reset_custom_model_data`

#### Permissions: `nexo.command.resetcmd`
