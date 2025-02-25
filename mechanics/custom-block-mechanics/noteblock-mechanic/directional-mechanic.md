---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966827878706708560/unknown.png
coverY: 0
---

# Directional Mechanic

### What is this?

This mechanic allows you to place blocks and have them change their texture depending on the direction in which they are placed, like for example logs.\
There are 3 types of directional blocks: `LOG`, `FURNACE` and `DROPPER`.\
`LOG` takes up 3 custom block variations, `FURNACE` takes 4 and `DROPPER` takes 6.

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

### Parent-Block example:

```yaml
main_block:
  itemname: "<white>Frozen Mushroom Stem"
  material: PAPER
  Pack:
    model: main_block_model
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      model: mainBlockModel
      custom_variation: 1
      directional:
        # Valid values are LOG, FURNACE and DROPPER
        directional_type: LOG
        # LOG
        y_block: main_block_y
        x_block: main_block_x
        z_block: main_block_z
        # FURNACE and DROPPER
        north_block: main_block_north
        east_block: main_block_east
        south_block: main_block_south
        west_block: main_block_west
        # DROPPER needs these aswell
        up_block: main_block_up
        down_block: main_block_down
      hardness: 1
      drop:
        minimal_type: WOOD
        best_tools:
          - AXE
        silktouch: false
```

#### LOG-type example:

```yaml
#This doesn't include the parent block from the above example
main_block_y:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 1
      directional:
        parent_block: main_block #base block which will give drop
      
main_block_x:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 2
      directional:
        parent_block: main_block #base block which will give drop

main_block_z:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 3
      directional:
        parent_block: main_block #base block which will give drop
```

#### FURNACE-type example:

```yaml
#This doesn't include the parent block from the above example
main_block_north:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      model: mainBlockModel
      custom_variation: 1
      directional:
        parent_block: main_block #base block which will give drop
      
main_block_south:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      model: mainBlockModel
      custom_variation: 2
      directional:
        parent_block: main_block #base block which will give drop

main_block_west:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      model: mainBlockModel
      custom_variation: 3
      directional:
        parent_block: main_block #base block which will give drop

main_block_east:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      model: mainBlockModel
      custom_variation: 4
      directional:
        parent_block: main_block #base block which will give drop
```

#### DROPPER-type example:

```yaml
#This doesn't include the parent block from the above example
main_block_north:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 1
      directional:
        parent_block: main_block #base block which will give drop
      
main_block_south:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 2
      directional:
        parent_block: main_block #base block which will give drop

main_block_west:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 3
      directional:
        parent_block: main_block #base block which will give drop

main_block_east:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      custom_variation: 4
      directional:
        parent_block: main_block #base block which will give drop

main_block_up:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      model: mainblockmodel_vertical
      custom_variation: 5
      directional:
        parent_block: main_block #base block which will give drop

main_block_down:
  excludeFromInventory: true # Makes inventory only contain base-block
  material: PAPER
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      model: mainblockmodel_vertical
      custom_variation: 6
      directional:
        parent_block: main_block #base block which will give drop
```
