---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966830020419014666/unknown.png
coverY: 0
---

# 🧵 StringBlock Mechanic

{% hint style="info" %}
STRINGBLOCK-type allows for up-to **127** custom blocks.\
One per `custom_variation`

Another quirk with this CustomBlock is that it has 2 different hitbox-states\
All variations after 64 will have a smaller hitbox than those before.
{% endhint %}

## How does it work?

This is a type of CustomBlock best aimed at plants, rocks and other foliage.\
It uses the vanilla TripWire block and therefore will disable all normal behaviour TripWires might have.

## How do I create a stringblock?

### Nexo Resourcepack configuration

Below is an example of how to configure the model/texture to use.\
`block/cross` is what normal vanilla plants use and allows for converting a 2d-texture into a block.\
If you want an example, look at RoseBushes in-game.

```yaml
jasmine_flower:
  itemname: "<white>Jasmine Flower"
  material: PAPER
  Pack:
    parent_model: "block/cross"
    texture: custom/flowers/jasmine_flower.png # .png extension is not mandatory
```

### StringBlock Mechanic Configuration

To use this mechanic you need to tell nexo which model to use (to use the generated one, just put the id name of your item).\
Then you need to use custom\_variation that is not already used by another decoration.\
You can also configure the hardness of the block, which specifies how long a block should take to break.\
`drop.best_tool` allows you to specify which tool should be best.\
An example would be PICKAXE for a small stone

```yaml
jasmine_flower:
  Mechanics:
    custom_block:
      type: STRINGBLOCK
      custom_variation: 2
      model: jasmine_flower
      hardness: 2
      drop:
        silktouch: false
```

## Minor sub-mechanics

Stringblocks also have some additional properties.\
`placeable_on_water`allows you to place it on water like Lilypads\
`is_tall` makes the customblock have a double hitbox, much like Tall Grass\
`random_place` takes a list of strings representing other stringblock-mechanics.\
This will then place a random one of these when the "parent" is placed

### Tall Plants

Nexo has a `is_tall` - property which makes the STRINGBLOCK take up two spaces, similar to Tall Grass. This requires using a specific parent-model and two separate textures, for the top and bottom block. Nexo also provides a default parent-model for use with this.\
Below is an example config using two different PNGs

```yaml
plant:
  Pack:
    parent_model: nexo:block/tall_plant
    textures:
      bottom: bottom_texture
      top: top_texture
  Mechanics:
    custom_block:
      type: STRINGBLOCK
      is_tall: true
```

## Sapling

```yaml
sapling:
  Mechanics:
    custom_block:
      type: STRINGBLOCK
      sapling:
        grows_naturally: true # if you want only the player can grow it
        natural_growth_time: 6000 #in ticks
        grows_from_bonemeal: true
        bonemeal_growth_speedup: 1250
        grow_sound: block.grass.break
        min_light_level: 4
        requires_water_source: false #if you want it to need water
        schematic: schemTest #structure that will put
        # this also allows you to use a list of schematics:
        # schematic:
        # - schem: palmTree1
        #   chance: 0.5
        # - schem: palmTree2
        #   chance: 0.5
        replace_blocks: false
        copy_biomes: false
        copy_entities: false
```

You can also add some randomness to the growth, or just increase the delay between checks.\
Go into `mechanics.yml` and under stringblock-mechanic, adjust `sapling_growth_check_delay`\
This is in ticks, so 20 = 1 second.

## BlockLocker

You can use this to allow protection via [BlockLocker](https://www.spigotmc.org/resources/blocklocker.3268/)\
Valid protectionTypes are CONTAINER, DOOR, ATTACHABLE

```yaml
Mechanics:
  custom_block:
    type: STRINGBLOCK
    blocklocker:
      can_protect: true
      protection_type: CONTAINER
```

![](https://cdn.discordapp.com/attachments/958524021035647046/961424759718047784/unknown.png)
