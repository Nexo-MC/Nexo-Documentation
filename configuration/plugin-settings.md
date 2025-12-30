---
description: Various options impacting the plugin in its generality
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825582216237126/unknown.png
coverY: 0
---

# ⚙️ Plugin settings

## Item configurations

Nexo configuration is mainly divided into 3, items, resourcepack & glyphs.\
These folders contain the majority of custom configurations you need.

## Formatting

Nexo has some settings for toggling its handling of various packets. Most of these are for transforming Glyph-Tags in packets that handle text or Items.\
Some of these can in some cases cause desync or other issues for some servers.\
These can be toggled of in such cases without much downside.

## ResourcePack

### Obfuscation

Obfuscation works by renaming all models, textures and files into random namespaces and paths\
This is to make it very hard for someone to just download and use your pack outside of your server.\
It comes with three modes, SIMPLE, FULL & NONE\
\
There is also an option to cache the obfuscated pack.\
This makes it so unless there are changes, Nexo will not reobfuscate the ResourcePack.\
This makes it so players do not have to redownload the ResourcePack every time your server starts.\\

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

### Hiding Scoreboard & Tablist

This option lets you hide the red scoreboard numbers.

```yaml
hide_scoreboard_numbers: true
hide_scoreboard_background: true
```

{% hint style="danger" %}
This might not work for 1.21.8+ servers due to changes in core shaders by Mojang
{% endhint %}

## Nexo Inventory

Nexo has a `inventory.yml` which can be configured to tweak how the NexoInventory works.\
It lets you change between two types for sorting the inventory, FILE & DIRECTORY.\
FILE is the default and organized everything into one main-page where each item-config file is shown on the main menu.\
DIRECTORY organizes the menu into subpages, following the structure you have inside `plugins/Nexo/items`

You can also specify the menu\_layout to tweak the individual buttons irrespective of the type above.\
This lets you set the slot a button is in, the icon/item to display with it and the title of the sub-page it opens. By default Nexo sorts slots by a-z of filenames & icon defaults to the first item in the config.\
You specify it like below, with it referencing the path to the item. The path depends on if you use FILE or DIRECTORY.\
If using FILE, the path is just the `filename`. If using DIRECTORY it is the entire path `folder.filename`&#x20;

```yaml
nexo_inventory:
  menu_title: <shift:-37><glyph:menu_items_search>
  search_title: <shift:256>NexoInventory Search<shift:256>
  style_default_names: true
  type: FILE
  menu_rows: 6
  menu_layout:
    my_item:
      slot: 1
      icon: itemid
      title: <main_menu_title>ItemID
```

The NexoInventory also has some other features & buttons which can be customized like below.\
This can reference a NexoItem or an ItemModel directly from the ResourcePack

```yaml
next_page_icon: next_page_icon
previous_page_icon: previous_page_icon
exit_icon: cancel_icon
search_icon: nexo:search_icon
directory_icon: nexo:directory_icon
```
