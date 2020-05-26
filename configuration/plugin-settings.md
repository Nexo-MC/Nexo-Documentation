---
description: Various options impacting the plugin in its generality
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825582216237126/unknown.png
coverY: 0
---

# ⚙️ Plugin settings

## Item configurations

### Overview of Nexo-Configurations?

Nexo configuration is mainly divided into 3, items, resourcepack & glyphs.\
These folders contain the majority of custom configurations you need.

## ResourcePack

### Obfuscation

Obfuscation works by renaming all models, textures and files into random namespaces and paths\
This is to make it very hard for someone to just download and use your pack outside of your server.\
It comes with three modes, SIMPLE, FULL & NONE\
\
There is also an option to cache the obfuscated pack. \
This makes it so unless there are changes, Nexo will not reobfuscate the ResourcePack.\
This makes it so players do not have to redownload the ResourcePack every time your server starts.\


```yaml
Pack:
  obfuscation:
    type: FULL
    cache: true
```

**NONE** does no obfuscation on the ResourcePack

```makefile
📁ResourcePack
└── 📁assets
    └── 📁custom_namespace
        └── 📁models
             └── 📑custom_model.json
```

**SIMPLE** only obfuscates individual filenames, but retains the original pack-structure

```makefile
📁ResourcePack
└── 📁assets
    └── 📁custom_namespace
        └── 📑02a61ae4-2457-4dfa-91af-9598cd52fd9e.json
```

**FULL** obfuscates the entire path

```
📁ResourcePack
└── 📁assets
    └── 📁0d003f53-e176-4e74-a895-d392c82f50be
        └── 📁models
             └── 📑02a61ae4-2457-4dfa-91af-9598cd52fd9e.json
```

### PackServer

The ResourcePack Nexo generates needs to be hosted somewhere before it can be sent to players.\
Nexo has two built-in server-options, POLYMATH & SELFHOST

**POLYMATH** is Nexo's own remote server\
It is located in Germany and can therefore be slower depending on your server's location and players download speed\
\
SELFHOST is a locally hosted server on the machine and can therefore be faster if your players are closer to it. You will need to manually configure the IP-address to your servers.

```yaml
Pack:
  server:
    type: SELFHOST
      selfhost:
        public_address: 0.0.0.0   # Set to your server's IP
        port: 8082                # Set to a port you have opened on your server
      polymath:
        server: atlas.mineinabyss.com
        secret: mineinabyss
```

### Dispatch

This section is for handling when the pack should be sent to players.

```yaml
Pack:
  dispatch:
    # Sends the Resourcepack before the players loads into the server
    # Might cause issues with large packs due to long download/load times
    send_pre_join: true
    send_on_join: false
    send_on_reload: true    # Sends the pack to players after using reload-command
    delay: -1               # Delay before pack is sent, does not apply to PreJoin dispatches
    mandatory: true         # If declining the ResourcePack should kick the player
    prompt: "<#fa4943>Accept the pack to enjoy a full <b><gradient:#9055FF:#13E2DA>Nexo</b><#fa4943>experience"
```

## Misc

### hide\_scoreboard\_numbers

This option lets you hide the red scoreboard numbers.

```yaml
  hide_scoreboard_numbers: true
```

### hide\_scoreboard\_background

This option lets you hide the scoreboard background.

```yaml
  hide_scoreboard_background: true
```

### reset\_recipes

```yaml
reset_recipes: true
```

This option can causes bug with other recipes plugins. If you notice bugs with a recipes plugin when reloading Nexo, you can disable this option. If you do that, you will have to restart the server to refresh Nexo recipes.

## Nexo Inventory

```yaml
nexo_inventory:
  main_menu_title: "<shift:-18><glyph:glyphid><shift:-193>"
  menu_rows: 6
  menu_layout:
    my_item:
      slot: 1
      icon: itemid
      title: <main_menu_title>ItemID
```

This allows you to configure an icon for every section of the Nexo inventory.\
You can use Nexo ids or Minecraft materials.
