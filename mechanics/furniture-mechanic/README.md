---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966828778028417125/unknown.png
coverY: 0
---

# 🪑 Furniture Mechanic

The furniture mechanic is the main way to implement custom furniture using Nexo.\
Below are an assortment of config file examples to help you in setting up your server.

## Furniture Mechanic

```yaml
myitem:
  itemname: "<gray>Table"
  material: PAPER
  Pack:
    model: default/table
  Mechanics:
    furniture:
      block_sounds:
        place_sound: block.stone.place
        break_sound: block.stone.break
        hit_sound: my.custom.hitsound     # Custom sound as defined in Nexo/sound.yml
        step_sound: my.custom.stepsound   # Requires a sound-file in the Nexo/pack-folder aswell
        fall_sound: my.custom.fallsound
      hitbox:
        barriers:
          - 0,0,0
      drop:
        silktouch: false
        # If no loots section is defined, will drop itself
        #loots:
        #  - { nexo_item: table, probability: 1.0 }
```

{% hint style="info" %}
If you are unsure how to reference a ResourcePack-File in a NexoItem config; [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq.md#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}

### Furniture-Properties

#### Display Transform

The `display_transform` dictates how the model will be displayed.\
By default it is set to `NONE`, which will show it as it looks when you open the model in BlockBench.\
As some other plugins might use ArmorStands and add the furniture to its head, you can set this option to `HEAD` for the same effect.\
There is also: `FIRSTPERSON_LEFTHAND`, `FIRSTPERSON_RIGHTHAND`, `FIXED`, `GROUND`, `GUI`, `THIRDPERSON_LEFTHAND`, `THIRDPERSON_RIGHTHAND`.\
All of these will be displayed ingame as shown in BlockBench's Display Tab under the specified type.\
Look at [Furniture Position](https://github.com/Nexo-MC/Nexo-Documentation/blob/master2/mechanics/furniture-mechanic/broken-reference/README.md) for an example on FIXED (ItemFrame Position)

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        display_transform: NONE
```

There is also a `default_properties` in `mechanics.yml` for changing the global default values of properties. These properties are applied first onto every furniture NexoItem, and any changes in the config itself would take priority

#### Tracking Rotation / Billboard

The `tracking_rotation`-property defines whether you want the furniture to "track" the player.\
This is mainly for stuff like billboard and leaderboards you want the player to see, not normal furniture.\
Options are:\
`FIXED` - No rotation\
`VERTICAL` - Pivots around vertical axis\
`HORIZONTAL` - Pivots around horizontal axis\
`CENTER` - Pivots around center point

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        tracking_rotation: FIXED
```

#### Translation

The \`translation\`-property lets you offset the model of your furniture. Can be useful to adjust visually without editing the model-json itself\
Config should look like this:

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        translation: 1.0,0,2
```

#### Brightness

The `brightness`-property lets you override the vanilla lighting-values of the furniture.\
It has a `block_light` and `sky_light` property for the different types of lighting Minecraft has. Config should look like this:

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        brightness:
          block_light: 15
          sky_light: 0
```

#### Scale

The `scale`-property is a way to scale the furniture.\
It has a `x`, `y` and `z` property for scaling on each axis. Config should look like this:

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        scale: 1,1,1
```

`view_range`, `shadow_radius`, `shadow_strength` should be self-explanatory.

### Custom Sounds

Furniture, like custom blocks, can have custom sounds

```yaml
myitem:
  Mechanics:
    furniture:
      block_sounds:
        place_sound: block.stone.place
        break_sound: block.stone.break
        hit_sound: my.custom.hitsound     # Custom sound as defined in Nexo/sounds.yml
        step_sound: my.custom.stepsound   # Requires a sound-file in the Nexo/pack-folder aswell
        fall_sound: my.custom.fallsound
```

All the volume and pitch values are set to be what Minecraft uses for blocks normally.\
If you want to change the volume or pitch, you can do so by using the format below.\
Keep in mind these two formats are compatible with eachother.\
We recommend just use the default one, but the option is there if you want to change it.

```yaml
myitem:
  Mechanics:
    furniture:
      block_sounds:
        place:
          sound: block.stone.place
          volume: 1.0
          pitch: 0.2
        break_sound: block.stone.break
        hit_sound: my.custom.hitsound     # Custom sound as defined in Nexo/sounds.yml
        step_sound: my.custom.stepsound   # Requires a sound-file in the Nexo/pack-folder aswell
        fall_sound: my.custom.fallsound
```

### Custom Drops

By default a NexoFurniture will drop itself when broken. This can be changed if you want and customized with several properties.

```yaml
my_block:
  Mechanics:
    furniture:
      drop:
        silktouch: false    # If Silktouch will make the block drop itself
        fortune: false      # If fortune should affect the amount of items dropped
        minimal_type: null  # Refers to the lowest material, if any, this drop requires
        best_tool: null     # Refers to the type of tool, if any, this drop requires
        loots:
          - nexo_item: my_item
          - minecraft_type: DIAMOND
            amount: 1
          - crucible_item: my_crucible_item
            amount: 1..2
          - mmoitem_type: TYPE
            mmoitem_id: ID
            probability: 1.0
```

**minimal\_type -** Refers to a tier of material the drop will require. This can be _WOODEN, STONE, IRON, GOLDEN, DIAMOND_ or _NETHERITE._ This also supports ItemType-Mechanic if it is specified in `mechanics.yml` `tool_types` list. If unspecified it is null, or no specific type required.

**best\_tool -** Refers to the type of tool this drop requires, if any. This can be _AXE, PICKAXE, SWORD, SHOVEL & HOE._ If unspecified it is null, or no specific tool required.

### Rotatable

To make a furniture rotatable, simply add the following to your item's config.

```yaml
myitem:
  Mechanics:
    furniture:
      rotatable: true
```

### ModelEngine Furniture

To make use of a ModelEngine model as your furniture, simply add the following to your item's config:

```yaml
myitem:
  Mechanics:
    furniture:
      modelengine_id: name_of_your_bbmodel_file
```

### Jukebox

Lets this furniture accept music discs and custom music discs which will be played.\
You can tweak the `volume` and `pitch` of the music from the jukebox.\
There is also a `permission` field, which can be used if you only want certain players to be able to play music from the jukebox.\
By default permission is blank, which means anyone can play music from the jukebox.

```yaml
myitem:
  Mechanics:
    furniture:
      jukebox:
        volume: 1.0
        pitch: 1.0
        permission: "nexo.jukebox.play"
```

### Restrict Rotation

You can restrict the amount of rotation-facings a furniture has with `restricted_rotation`.\
It can be set to STRICT or VERY\_STRICT, with 8 and 4 facings respectively.\\

```yaml
myitem:
  Mechanics:
    furniture:
      restricted_rotation: VERY_STRICT #STRICT is default if unspecified
```

### Limited placing

You can customize what blocks a custom block/furniture can be placed on with `limited_placing` subsection. You can use the `roof`, `floor` and `wall` options to dictate where a block can be placed. By default, all are set to `true`.\
The `type` specifies if it should only be allowed on or denied on specific blocks.\
If type is `ALLOW` the block can only be placed on the given blocks.\
If the type is `DENY` can be placed on all blocks not matching the given blocks.\
There is also a `radius_limitation` option, which allows you to limit the amount of a certain furniture within a radius.

```yaml
myitem:
  Mechanics:
    furniture:
      limited_placing:
        radius_limitation:
          radius: 20
          amount: 10
        roof: false
        floor: true
        wall: false
        type: ALLOW
        block_types:
          - GRASS_BLOCK
          - DIRT
        block_tags:
          - base_stone_nether
        nexo_blocks:
          - chair
          - ruby_ore
```

The `block_tags` can be found at [this page](https://minecraft.fandom.com/wiki/Tag#Block_tags). Useful if you want to allow/deny a group of blocks.\
The `block_types` are materials. Useful if you want to allow/deny a specific list block.\
The `nexo_blocks` are blocks/furniture from Nexo.\
This allows all custom blocks and furniture in here, but furniture requires a barrier-hitbox.

### Storage

This is a sub-mechanic for furniture & noteblock mechanics, that let you make a custom storage container.\
Essentially a chest, closet or whatever you might want.

There's a few different types: _STORAGE, PERSONAL, ENDERCHEST & DISPOSAL_.\
**STORAGE** is similar to a normal chest. Anyone can open it and view the content of it.\
**PERSONAL** is essentially a custom enderchest, letting you edit the row-count and so on.\
**ENDERCHEST** is literally just the enderchest inventory, but letting you make a custom block/furniture to access it.\
**DISPOSAL** is a custom trashcan, letting you throw items in it, and they will be deleted when closed.\\

```yaml
myitem:
  Mechanics:
    furniture:
      storage:
        type: STORAGE
        rows: 5                             # Default: 6
        title: "<red>My Storage"            # Default: "Storage"
        open_sound: entity.shulker.open     # Default: entity.chest.open
        close_sound: entity.shulker.close   # Default: entity.chest.close
```

### Waterloggable

You can make furniture waterloggable when placed underwater by following the below.\
This mainly applies to the barrier-hitboxes of your furniture

```yaml
myitem:
  Mechanics:
    furniture:
      waterloggable: true
```

### BlockLocker

You can use this to allow protection via [BlockLocker](https://www.spigotmc.org/resources/blocklocker.3268/)\
Valid protectionTypes are CONTAINER, DOOR, ATTACHABLE

```yaml
myitem:
  Mechanics:
    furniture:
      blocklocker:
        can_protect: true
        protection_type: CONTAINER
```
