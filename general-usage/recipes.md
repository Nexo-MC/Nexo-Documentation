---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966826759293136996/unknown.png
coverY: 0
---

# 🧑‍🍳 Recipes

Recipes can be created directly in the relevant file within the `Nexo/recipes` directory, or through the ingame RecipeBuilder.\
The RecipeBuilder can be accessed with the command `/nexo recipes builder`.\
Drag your desired items into the crafting slots to create your recipe. Make sure to set the "output" slot to the item you want to give.

Each Recipe-type has its own folder in `plugins/Nexo/recipes`, meaning you can organize recipes inside each folder into different files, sub-folders, etc.\
The RecipeBuilder will store recipes inside `plugins/Nexo/recipes/X/X_recipes.yml`, X being the type (shaped, shapeless, etc.)

### Available Recipe Types:

* SHAPELESS - Allows each ingredient to be put in any slot
* SHAPED - Requires ingredients to be in a specific shape
* FURNACE - Recipe for the Furnaces
* BLASTING - Recipe for the Blast Furnace
* SMOKING - Recipe for the Smoker
* STONECUTTING - Recipe for the Stone Cutter
* BREWING - Recipe for the Brewing Stand
* SMITHING - Recipe for the Smithing Table - This is added via [NexoAddon](https://nexoaddon.gitbook.io/docs/recipes/smithing-recipe)

## Examples:

### Shapeless

`amount` in result specifies how many of said item you should get

```yaml
grass_block_shapeless:
  result:
    minecraft_type: GRASS_BLOCK
    amount: 2
  ingredients:
    A:
      minecraft_type: MOSS_CARPET
    B:
      minecraft_type: DIRT
    C:
      minecraft_type: DIRT
```

<div align="left"><figure><img src="../.gitbook/assets/shapeless.png" alt=""><figcaption></figcaption></figure></div>

***

### Shaped

You can also use Minecraft tags and Nexo items in recipes

```yaml
forest_axe:
  result:
    nexo_item: forest_axe
  ingredients:
    A:
      tag: minecraft:leaves
    B:
      minecraft_type: STICK
  shape:
  - _AA
  - _BA
  - _B_

```

<div align="left"><figure><img src="../.gitbook/assets/shaped.png" alt=""><figcaption></figcaption></figure></div>

***

### Furnace + Blasting + Smoking

```yaml
raw_iron_block_to_iron:
  result:
    minecraft_type: IRON_INGOT
    amount: 9
  input:
    minecraft_type: RAW_IRON_BLOCK
  cookingTime: 100
  experience: 20
```

<div align="left"><figure><img src="../.gitbook/assets/smelting.png" alt=""><figcaption></figcaption></figure></div>

***

### Stonecutting

```yaml
stripped_spruce_log:
  result:
    minecraft_type: STRIPPED_SPRUCE_LOG
  input:
    minecraft_type: SPRUCE_LOG
```

<div align="left"><figure><img src="../.gitbook/assets/stonecutting.png" alt=""><figcaption></figcaption></figure></div>

***

### Brewing

```yaml
diamond:
  result:
    minecraft_type: DIAMOND
  input:
    minecraft_type: GLASS_BOTTLE
  ingredient:
    nexo_item: rainbow_ingot
```

<div align="left"><figure><img src="../.gitbook/assets/brewing.png" alt=""><figcaption></figcaption></figure></div>
