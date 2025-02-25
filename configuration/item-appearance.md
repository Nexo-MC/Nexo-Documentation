---
description: How to customize your item appearance?
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966824489490976798/unknown.png
coverY: 0
---

# Item Appearance

### The pack folder

This folder contains all your ResourcePack content.\
It's structure is the same as any normal resourcepack, but with a few tweaks.\
Textures and models can simply be dragged into `pack/assets/minecraft/(models/textures)` respectively, if you have individual files.\
If you have a full resourcepack, you can add it to `pack/external_packs`

### Create a basic 2d item

Put the textures that you need in the textures directory of the pack folder.\
You can then reference the textures in your item & make Nexo generate the necessary model-file:

```yaml
my_item:  
  Pack:
    parent_model: "item/handheld"
    textures:
      - example_image1.png #png extension is not needed
      - example_image2.png
```

The parent\_model field is required by minecraft.\
It is mainly used to inherit certain rendering properties of models.\
Most items will use `item/generated`, but `item/handheld` is often used by tools and weapons.

You can also use an alternative way of declaring textures, especially nice when using block parent-models. This lets you specify the texture-ids to use specifically.

```yaml
Pack:
  parent_model: "block/cube"
  textures:
    top: example_image.png
    side: example_image2.png
```

### Use your own JSON Model

{% hint style="danger" %}
ALWAYS USE LOWER CASE FOR MODEL AND TEXTURE NAMES. Upper case is n longer supported by minecraft vanilla since 1.11 (even though it still works for users using optifine).
{% endhint %}

```yaml
  Pack:
    model: example_model.json #json extension is not mandatory
```

#### ⚠️ Pro tips when you use a json model!

Usually the templates you get place the textures in a folder, to make sure, open the json file and look at the first few lines, you should find something similar:

```json
{
  "textures": {
    "particle": "custom/my_item",
    "texture": "custom/my_item",
    "bonesword_palette": "custom/my_item"
  }
}
```

As above shows the model is set to look for textures in `custom/my_item`\
The file should then be put inside `Nexo/pack/assets/minecraft/textures/custom/my_item`\
The normal structure for model & texture-paths are `namespace:some/path`, which is the same as `pack/assets/namespace/(models/textures)/some/path(.png/.json)`\`

### Use a blocking json model (for shield)

```yaml
  Pack:
    model: example_shield.json #json extension is not mandatory
    blocking_model: example_shield_blocking.json #json extension is not mandatory
```

### Use a pulling json model (for bows)

```yaml
  Pack:
    model: default/combat_bow
    pulling_models:
      - default/combat_bow_pulling_0
      - default/combat_bow_pulling_1
      - default/combat_bow_pulling_2
```

This also works with pulling\_textures if you only have texture files

### Use charged\_model json model (for Crossbows)

```yml
  Pack:
    model: default/custom_bow
    pulling_models:
      - default/custom_bow_pulling_0
      - default/custom_bow_pulling_1
      - default/custom_bow_pulling_2
    charged_model: default/custom_bow_pulling_2
    firework_model: default/custom_bow_charged #Optional
```

This also works with charged\_texture & firework\_texture if you only have texture files

### Use cast\_model json model (for fishing rods)

```yml
  Pack:
    model: default/fishing_rod
    cast_model: default/fishing_rod_cast
```

This also works with cast\_texture if you only have texture files

### Use damaged\_model json model (for different durability levels)

```yml
Pack:
  model: default/diamond_sword
  damaged_models:
    - default/diamond_sword_damaged1
    - default/diamond_sword_damaged2
    - default/diamond_sword_damaged3
```

This also works with damaged\_textures if you only have texture files
