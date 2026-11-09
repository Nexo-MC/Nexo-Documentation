# 🎲 Block Variants

Like vanilla stone or grass, a custom block can pick randomly between several models or rotations each time it is placed.\
This works for every type of custom block, and is set with a `variants` list.

```yaml
my_stone:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      model: my_stone
      variants:
        - model: my_stone
          weight: 3
        - model: my_stone_alt
        - model: my_stone
          y: 90
          uvlock: true
```

## Properties

**model -** The model of this variant. Defaults to the `model` of the custom block\
**weight -** How likely this variant is to be picked compared to the others. Default is 1\
**x -** Rotation around the x-axis in degrees, in steps of 90. Default is 0\
**y -** Rotation around the y-axis in degrees, in steps of 90. Default is 0\
**uvlock -** Keeps the texture from rotating along with the model. Default is false\
**offset -** `x,y,z` to shift the model by, in blocks

In the example above `my_stone` is picked 3 out of 5 times, and `my_stone_alt` and the rotated `my_stone` 1 out of 5 times each.

If the custom block has no `model`, the first variant with a `model` is used, and after that `Pack.model`.

{% hint style="warning" %}
Nexo reuses the `custom_variation` of any block sharing the same model.\
If several blocks share the same model, set `custom_variation` on each of them yourself so they do not end up as the same block
{% endhint %}

## Offset

`offset` shifts the model of a variant, for example to make a plant sit slightly lower or off-center.\
It is written in blocks, so `0,-0.0625,0` moves it down by one pixel.

```yaml
my_flower:
  Mechanics:
    custom_block:
      type: STRINGBLOCK
      model: my_flower
      variants:
        - model: my_flower
        - model: my_flower
          offset: 0.1875,0,0
        - model: my_flower
          offset: 0,0,-0.1875
```

Nexo generates a shifted copy of the model for each offset, named `<model>_offset_<x>_<y>_<z>` with the values in pixels.\
Models can only reach from -1 to 2 blocks in each direction.\
If the offset pushes the model outside this, Nexo warns you and uses it without the offset.

{% hint style="info" %}
The model being offset has to exist in Nexo's own pack or be a vanilla model.\
If your pack is merged outside of Nexo, see [API](../../community-guides/api.md#packs-merged-outside-nexo)
{% endhint %}

## Directional Blocks

[Directional Blocks](noteblock-mechanic/directional-mechanic.md) whose directions do not define a model of their own use the variants of the parent block.\
Each direction rotates them to face the right way, which replaces the `x` & `y` of every variant.
