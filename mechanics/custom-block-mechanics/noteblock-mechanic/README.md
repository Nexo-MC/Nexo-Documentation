---
description: How to add your own blocks to the game
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966827878706708560/unknown.png
coverY: 0
layout:
  width: default
  cover:
    visible: false
    size: full
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# 🎶 NoteBlock Mechanic

{% hint style="info" %}
NOTEBLOCK-type allows for up-to **1149** custom blocks.\
One per `custom_variation`
{% endhint %}

## How to create a simple block?

### Parent Models

The Nexo-item root configuration is the same as for any item (you can use any material like a diamond for example) and set an itemname, etc.\
It is recommended to not use a block for your material, sticking to such materials as PAPER\
For the pack section you can use your own model or texture for your block.\
If all you have is a texture, you can specify a parent\_model and Nexo will generate the needed files for you. A Normal 1x1x1 block uses "block/cube\_all"

```yaml
my_block:
  itemname: "My block"
  material: DIAMOND
  Pack:
    parent_model: "block/cube_all"
    texture: my_block_texture.png
```

Each of these parent models take a different amount of textures.\
`block/cube_all` takes 1 texture, `block/cube_column` takes 2, `block/cross` takes 1, `block/orientable` takes 3 and `block/orientable_vertical` takes 2.\
For example, if you want to make a log block using the Directional Block mechanic, you should use `block/cube_column`.

All the vanilla models can be found at [MCAsset](https://mcasset.cloud/1.21.3/assets/minecraft/models/block). Find the one you want to use for your usecase.\
Recommend using a "texture map" in the config for multi-texture setups.

```yaml
my_block:
  itemname: "My block"
  material: DIAMOND
  Pack:
    parent_model: "block/cube_top"
    textures:
      side: my_side_texture.png
      top: my_top_texture.png
```

### CustomBlock Mechanic configuration

To use this mechanic you need to tell to Nexo which model to use (to use the generated one, just put the name id of your item).

A Custom Block must also be assigned unique _custom\_variation_. This is a number between 1 & 1149.\
If unspecified, Nexo will automatically set one for you.

Keep in mind this should not be changed after a block is being used. The only think linking a placed block to a given NexoItem is its BlockData, which is defined by this variation

<pre class="language-yaml"><code class="lang-yaml">my_block:
<strong>  Mechanics:
</strong>    custom_block:
      type: NOTEBLOCK
      custom_variation: 2
      model: my_block
      drop:
        silktouch: false 
        minimal_type: STONE
</code></pre>

### Custom Sounds

Furniture, like custom blocks, can have custom sounds

```yaml
myitem:
  Mechanics:
    custom_block:
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
    custom_block:
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

### Customize the breaking speed

You can customize the breaking speed and the most suitable tools with the hardness subsection.\
`drop.best_tool` dictates the "preferred tool" for this block which further tweaks the speed

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 2
      model: my_block
      hardness: 20 # this makes it really hard to mine
      drop:
        silktouch: false 
        minimal_type: STONE
        best_tool: PICKAXE
```

### Custom Drops

By default a Nexo CustomBlock will drop itself when mined. This can be changed if you want and customized with several properties.

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
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

### Limited placing

You can customize what blocks a custom block/furniture can be placed on with `limited_placing` subsection. You can use the `roof`, `floor` and `wall` options to dictate where a block can be placed. By default, all are set to `true`.\
The `type` specifies if it should only be allowed on or denied on specific blocks.\
If type is `ALLOW` the block can only be placed on the given blocks.\
If the type is `DENY` can be placed on all blocks not matching the given blocks.

```yaml
amethyst_ore:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      limited_placing:
        roof: true
        floor: true
        wall: true
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
The `nexo_blocks` are blocks defined in the nexo configuration.\
This allows all custom blocks and furniture in here, but furniture requires a barrier-hitbox.

### Beacon Base

You can also make a custom block work in beacons with the following:

{% code lineNumbers="true" %}
```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      beacon_base_block: true
```
{% endcode %}

{% hint style="info" %}
A beacon will "activate" if any noteblock is in the pyramid, but the effect is only given when said noteblock(s) are base\_beacon\_blocks\
This is because it requires a Datapack that adds noteblocks to the given Tag, but it does not support individual blockstates
{% endhint %}

### Blast-Resistant

You can make your custom-block blast-resistant by adding the following.\
If unspecified it defaults to false.\
You can also make your block drop something when it explodes by adding `in_explosion: true`to your Loot like below

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      blast_resistant: true
      drop:
        loots:
          - nexo_item: my_block
            in_explosion: true
```

### BlockLocker

You can use this to allow protection via [BlockLocker](https://www.spigotmc.org/resources/blocklocker.3268/) Valid protectionTypes are CONTAINER, DOOR, ATTACHABLE

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      blocklocker:
        can_protect: true
        protection_type: CONTAINER
```

### Storage

This is a sub-mechanic for furniture and noteblock mechanics, that let you make a custom storage container.\
Essentially a chest, closet or whatever you might want.

There's a few different types: _STORAGE, PERSONAL, ENDERCHEST & DISPOSAL_.\
**STORAGE** is similar to a normal chest. Anyone can open it and view the content of it.\
**PERSONAL** is essentially a custom enderchest, letting you edit the row-count and so on.\
**ENDERCHEST** is literally just the enderchest inventory, but letting you make a custom block/furniture to access it.\
**DISPOSAL** is a custom trashcan, letting you throw items in it, and they will be deleted when closed.\\

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      storage:
        type: STORAGE
        rows: 5                             # Default: 6
        title: "<red>My Storage"            # Default: "Storage"
        open_sound: entity.shulker.open     # Default: entity.chest.open
        close_sound: entity.shulker.close   # Default: entity.chest.close
```

### Falling Blocks

This is a sub-mechanic that mimics sand & gravel for your custom block. Placing it next to another block, with no block beneath, will make it fall

```yaml
my_block:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      is_falling: true # Default to false if unspecified
```
