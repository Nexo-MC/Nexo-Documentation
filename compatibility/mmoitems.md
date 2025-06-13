---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966832308395049000/unknown.png
coverY: 0
---

# MMOItems

### Import an MMOItem into your NexoITem

The compatibility with MMOItem allows you to import items created with this plugin and use them as a base for your Nexo-items (you will keep everything configured with MMOItem and add your own mechanics, textures, 3d models, etc).

```yaml
example_mmoitem:
  itemname: "<gradient:#59A7EA:#F1D2FF>Test"
  mmoitem:
    type: SWORD
    id: FALCON_BLADE
    level: 10 # Optional
    tier: RARE # Optional
    match_level: true # Optional
```

### MMOItems in NexoFurniture & Custom Block drops

You can also specify an mmoitem to be dropped directly when breaking a furniture or a custom block.\
You just need to specify the `mmoitems_id` & `mmoitems_type` in drop like shown below;

```yaml
myitemid:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      drop:
        loots:
          - mmoitems_id: FALCON_BLADE
            mmoitems_type: SWORD
            amount: 1..3 #Optional
    furniture:
      drop:
        loots:
          - mmoitems_id: FALCON_BLADE
            mmoitems_type: SWORD
            amount: 1..3 #Optional
```

### MMOItems in Nexo-Recipes

You can also make a recipe in Nexo that takes an MMOItem as an ingredient or as the result.\
Like with drops, you just need to specify the `mmoitems_id` & `mmoitems_type` \
Below is an example of a shaped recipe using an MMOItem. Using the RecipeBuilders ingame should also do this for you if the item you use is an MMOItem

```yaml
myrecipeid:
  result:
    mmoitems_id: FALCON_BLADE
    mmoitems_type: SWORD
  ingredients:
    A:
      mmoitems_id: FALCON_BLADE
      mmoitems_type: SWORD
  shape:
  - ___
  - ___
  - _A_
    
```
