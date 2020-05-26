---
description: A simple explanation to use the plugin commands
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966827022758330398/unknown.png
coverY: 0
---

# ⌨️ Commands

## General informations

All the nexo-commands can be found under `/nexo`

## Get the items

### Nexo-Inventory Command

The main benefit of this method is that it allows you to see all the items at the same time in categories based on your `Nexo/items/filename.yml`\
You can grab copies of items here but cannot give it to other players.

#### Usage: `/nexo inventory` or `/nexo inv`

#### Permission: `nexo.command.inventory`

### Item-Give Command

This command will be mainly useful if you want to give an item to another player or when you want to automate the give

#### Usage: `/nexo give <player> <item> <amount>`

#### Permission: `nexo.command.give`

## Recipe-Commands

This command allows you to add new recipes to the configuration directly from the game using recipes builder. For more information on how to use it, see [Recipes](recipes.md).

#### Usage:

```yaml
/nexo recipe builder <builder> # Creates a recipe builder of type <builder> and opens it
/nexo recipe save <name> # Saves your recipe with name <name>
/nexo recipe show all # Show you the loaded recipes
/nexo recipe show <recipe> # Show you one recipe
```

#### Permission: `nexo.command.recipes`

## Pack-Command

This command allows you to send the pack to a group of players. \
Useful if the automatic sending failed or for testing

#### Usage: `/nexo pack <player>`

#### Permission: `nexo.command.pack`

## Item-Info Command

This command allows you to print general info about a NexoItem for debugging

#### Usage: `/nexo iteminfo <itemid>`

#### Permission: `nexo.command.iteminfo`

## Reload-Command

This command allows you to reload Nexo configurations.\
Reloading items updates any changes you might have made, and updates all old copies players might have.\
Reloading pack regenerates the resourcepack, and if `Pack.dispatch.send_on_reload` is enabled in `settings.yml`, will be dispatched to all players.

#### Usage

```yaml
/nexo reload all # Reloads items configuration, Reloads recipes configuration, regenerates the pack and upload it
/nexo reload items # Reloads items configuration
/nexo reload pack # Regenerates resourcepack and upload it
/nexo reload recipes # Reloads recipes configuration
```

#### Permission: `nexo.command.reload`

## Debug-Command

This command just toggles the debug-state of Nexo.\
In case you run into a bug or an error, you might be asked to toggle this to provide support with a more full error-log of the bug.

#### Permissions: `nexo.command.debug`
