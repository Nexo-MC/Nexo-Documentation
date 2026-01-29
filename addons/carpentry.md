---
cover: ../.gitbook/assets/image (12).png
coverY: 0
---

# 🚪 Carpentry

This is an addon for Nexo that adds several new CustomBlock types.\
It allows for custom doors, trapdoors, stairs, slabs and transparent blocks.\
Below will be examples for each of the different types

[Polymart](https://polymart.org/product/7640/carpentry-nexo-addon) | [MCModels](https://mcmodels.net/products/13997/carpentry)

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption><p>Default Ashen Oak wood-set included in Carpentry's Default Items</p></figcaption></figure>

{% hint style="warning" %}
Note that each of the types are currently limited to only 4 variations.

If you are unsure how to reference a ResourcePack-File in a NexoItem config; [#how-do-i-reference-a-resourcepack-file-in-a-config](../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}

### Custom Stairs

```yaml
custom_stair:
  material: PAPER
  itemname: Custom Stair
  Pack:
    parent_model: block/stairs
    texture: nexo:items/carpentry_blocks/ashen_oak_planks
    #textures:                      # Example if one wants different textures
    #  bottom: block/reinforced_deepslate_bottom
    #  side: block/reinforced_deepslate_side
    #  top: block/reinforced_deepslate_top
  Mechanics:
    custom_block:
      type: STAIR
      custom_variation: 1          # 1-4 are available
```

### Custom Slabs

```yaml
custom_slab:
  material: PAPER
  itemname: Custom Slab
  Pack:
    parent_model: block/slab
    texture: nexo:items/carpentry_blocks/ashen_oak_planks
    #textures:                      # Example if one wants different textures
    #  bottom: block/reinforced_deepslate_bottom
    #  side: block/reinforced_deepslate_side
    #  top: block/reinforced_deepslate_top
  Mechanics:
    custom_block:
      type: SLAB
      custom_variation: 1          # 1-4 are available
```

### Custom Doors

Door-setup is a bit different than the other blocks, as it requires two configs.\
This is because the item-model in hand will look incorrect if it uses the block-parent-models\
The second config is just so that Nexo generates the necessary models\
If you provide your own json-model, you can skip the second config\\

ItemConfig for held item:

```yaml
custom_door:
  material: PAPER
  itemname: Custom Door
  Pack:
    parent_model: item/generated   # This is used for the item when held in hand
    # The texture to use for the item in hand
    texture: nexo:items/carpentry_blocks/ashen_oak_door_icon
  Mechanics:
    custom_block:
      type: DOOR
      custom_variation: 1          # 1-4 are available
      model: custom_door_placed    # The itemid of the second config, that generates the block-model
```

ItemConfig for placed-block:

```yaml
custom_door_placed:
  # Handles the generation of the model the placed blocks should use
  # This is the same as all other block-types use in their Pack section
  # But split apart due to how held door-items work
  Pack:
    parent_model: block/door_bottom_left        # Default parent-model for doors
    textures:
      bottom: nexo:items/carpentry_blocks/ashen_oak_door_bottom
      top: nexo:items/carpentry_blocks/ashen_oak_door_top
  # Extra properties to prevent item from being "registered" as a NexoItem
  injectId: false
  excludeFromInventory: true
  excludeFromCommands: true
```

### Custom Trapdoors

```yaml
custom_trapdoor:
  material: PAPER
  itemname: Custom Trapdoor
  Pack:
    parent_model: block/template_orientable_trapdoor_bottom
    texture: nexo:items/carpentry_blocks/ashen_oak_trapdoor
  Mechanics:
    custom_block:
      type: TRAPDOOR
      custom_variation: 1         # 1-4 are available
```

### Custom Transparent

This type allows for transparent blocks, useful for leaves etc.\
For normal blocks that do not require transparency, use [NoteBlock Mechanic](../mechanics/custom-block-mechanics/noteblock-mechanic/)

```yaml
custom_grate:
  material: PAPER
  itemname: Custom Grate
  Pack:
    parent_model: block/cube_all
    texture: nexo:items/carpentry_blocks/ashen_oak_leaves
  Mechanics:
    custom_block:
      type: GRATE
      custom_variation: 1          # 1-4 are available
```

{% hint style="warning" %}
The BlockTypes below here require a 1.21.10+ server
{% endhint %}

### Custom Chain

This type allows for custom chains, like iron or copper ones.\
The config is very basic and only requires you to have a Texture for it

```yaml
custom_chain:
  material: PAPER
  itemname: Custom Chain
  Pack:
    parent_model: block/template_chain
    texture: my_texture/path
  Mechanics:
    custom_block:
      type: CHAIN
```

### Custom Lantern

This type allows for custom chains, like copper & normal ones.\
The config is very basic and only requires you to have a Texture for it

```yaml
custom_lantern:
  material: PAPER
  itemname: Custom Lantern
  Pack:
    parent_model: block/template_lantern
    texture: my_texture/path
  Mechanics:
    custom_block:
      type: LANTERN
```

### Custom Bars

This type allows for custom bars, like iron bars in vanilla.\
The config is very basic and only requires you to have a Texture for it

```yaml
custom_bars:
  material: PAPER
  itemname: Custom Bars
  Pack:
    parent_model: block/template_bars
    texture: my_texture/path
  Mechanics:
    custom_block:
      type: BARS
```
