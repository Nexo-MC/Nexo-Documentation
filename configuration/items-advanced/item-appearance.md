---
description: How to customize your item appearance?
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966824489490976798/unknown.png
coverY: 0
---

# Special Item Appearance

### Use a different model for Inventory Icon vs Equipped/In-Hand

{% hint style="info" %}
This is for 1.21.2+ servers & clients only
{% endhint %}

If you want to say have an item with a 2D icon in the inventory but when worn on head or held in your hand, it uses a 3D model or another 2D icon, you can do so by following the below

You need to provide an ItemModel that specifies when to show what model.\
Here is an example using a `mymodel_icon` model for the GUI and a "fallback" for everything else.\
This approach can be used for most other contexts, which you can find [here](https://minecraft.wiki/w/Items_model_definition#display_context).\
This is not a detailed guide on ItemModels, but you can do very complex things with them beyond this.

```json
{
  "model": {
    "type": "select",
    "property": "display_context",
    "cases": [
      {
        "when": "gui",
        "model": {
          "type": "model",
          "model": "namespace:mymodel_icon" // The model to display for the GUI
        }
      }
    ],
    "fallback": {
      "type": "model",
      "model": "namespace:mymodel" //The model that is used everywhere else
    }
  }
}
```

You can put this inside `Nexo/pack/assets/namespace/items/mymodel.json` .

Then you can make your NexoItem-config, which will reference this ItemModel

```yaml
myitem:
  itemname: "My Item"
  Components:
    item_model: namespace:mymodel
```

### Use a blocking json model (for shield)

```yaml
myitem:
  Pack:
    model: example_shield.json #json extension is not mandatory
    blocking_model: example_shield_blocking.json #json extension is not mandatory
```

### Use a pulling json model (for bows)

```yaml
myitem:
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
myitem:
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
myitem:
  Pack:
    model: default/fishing_rod
    cast_model: default/fishing_rod_cast
```

This also works with cast\_texture if you only have texture files

### Use damaged\_model json model (for different durability levels)

```yml
myitem:
  Pack:
    model: default/diamond_sword
    damaged_models:
      - default/diamond_sword_damaged1
      - default/diamond_sword_damaged2
      - default/diamond_sword_damaged3
```

This also works with damaged\_textures if you only have texture files
