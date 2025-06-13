---
description: Crucible is an addon for MythicMobs
cover: >-
  https://git.mythiccraft.io/uploads/-/system/project/avatar/51/unknown.png?width=64
coverY: 0
---

# MythicCrucible

### Import a MythicCrucible item into your NexoItem

The compatibility with Crucible allows you to import items created with MythicMobs & Crucible and use them as a base for your Nexo-items (you will keep everything configured with Crucible and add your own mechanics, textures, 3d models, etc).

```yaml
example_crucible:
  itemname: "<gradient:#59A7EA:#F1D2FF>Test"
  crucible_id: my_crucible_itemid
```

### MythicCrucible Items in Nexo Furniture/CustomBlock drops

You can also specify a crucible to be dropped directly when breaking a furniture or a custom block.\
You just need to specify the `crucible_item` like below;

```yaml
myitemid:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      drop:
        loots:
          - crucible_item: my_crucible_itemid
            amount: 1..3 #Optional
    furniture:
      drop:
        loots:
          - crucible_item: my_crucible_itemid
            amount: 1..3 #Optional
```

### MMOItems in Nexo-Recipes

You can also make a recipe in Nexo that takes an Crucible Item as an ingredient or as the result.\
Like with drops, you just need to specify the `crucible_item`\
Below is an example of a shaped recipe using a CrucibleItem. Using the RecipeBuilders ingame should also do this for you if the item you use is an CrucibleItem

```yaml
myrecipeid:
  result:
    crucible_item: my_crucible_itemid
  ingredients:
    A:
      crucible_item: my_crucible_itemid
  shape:
  - ___
  - ___
  - _A_
    
```
