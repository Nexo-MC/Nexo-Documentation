---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966827878706708560/unknown.png
coverY: 0
---

# Directional Mechanic

This mechanic allows you to place blocks and have them change their texture depending on the direction in which they are placed, like for example logs.\
There are 4 types of directional blocks: **LOG, BARREL, FURNACE & DROPPER**

**LOG** is made up of 3 Custom Block variations, to mimic behaviour of a vanilla log\
**BARREL** is made up of 6 Custom Block variations. It s used for when you need a block to be rotatable in all 6 directions (north, west, south, east, up & down)

**FURNACE** is made up of 4 Custom Block variations. It is for when you want a block that rotates to face the player with a front in the 4 horizontal directions (north, south, east, west)\
**DROPPER** is made up of 6 Custom Block variations. It is for the same purpose as **Furnace** but with support for up & down facings as well.

{% hint style="info" %}
Every sub-block can have a `model` property, which Nexo will use to determine what to display.\
If there is no `model` property on the sub-block, Nexo will use the model from the parent-block.
{% endhint %}

{% hint style="info" %}
Models are also automatically rotated depending on the direction in which the block is placed.\
This means you can use the same model, and it will be rotated accordingly.\
If the sub-block has a model defined, it will not be rotated, allowing you to use different models for different directions.
{% endhint %}

{% embed url="https://user-images.githubusercontent.com/62521371/167680557-750dac77-b4c4-4804-9513-184d776a012d.mp4" %}

### Configuration

The most basic of configuration setups for a directional blocks is reusing the same model and having it be rotated accordingly. Below is such an example

```yaml
custom_log:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      directional:
        type: LOG
```

Nexo will here automatically generate 3 fake dummy-items for each direction and assign a `custom_variation` for each. The config will then look something like this after

```yaml
custom_log:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      directional:
        type: LOG
        y_variation: 1
        x_variation: 2
        z_variation: 3
      custom_variation: 1 #This can be the same as y-variation to save 1 block-slot
```

This applies to the three other types aswell; BARREL, FURNACE & DROPPER.\
You can also set a model explicitly for each rotation like shown in DROPPER example.\
If this is done, Nexo will not apply the standard rotations to it.