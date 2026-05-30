---
description: How to customize your item appearance?
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966824489490976798/unknown.png
coverY: 0
---

# Special Item Appearance

## The basics: 2D texture vs 3D model

Everything under `Pack` controls what your item _looks like_. Before the special cases below, there are two foundational ways to give an item its appearance:

* **`Pack.texture`** — point at a single **PNG**. Nexo generates a flat, sprite-style model for you (the same look as a vanilla `paper` or `apple`). This is all you need for most items.
* **`Pack.model`** — point at a **JSON model** (e.g. one exported from BlockBench). Use this when you want real 3D geometry, or any look that a flat sprite can't produce.

Use **one or the other** — `texture` for a flat icon, `model` for a custom model. You don't need both.

{% hint style="info" %}
Not sure how the `nexo:item/...` reference maps to a file on disk? See [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention"). In short: `nexo:item/ruby` → `assets/nexo/textures/item/ruby.png` for a texture, and `assets/nexo/models/item/ruby.json` for a model.
{% endhint %}

### Simple — a 2D texture only

This is the simplest possible custom item: a single PNG shown as a flat icon, both in the inventory and in-hand.

```yaml
ruby:
  itemname: "<red>Ruby"
  material: PAPER
  Pack:
    texture: nexo:item/ruby
```

**File layout**

```
📁 Nexo/pack/assets/nexo/textures/item
└── 📑 ruby.png
```

That's it — Nexo automatically builds a generated model around `ruby.png`, so no `.json` model file is needed.

{% hint style="info" %}
`material: PAPER` is recommended. Nexo assigns the item its own ItemModel, so it never collides with other items sharing the same material. See [itemmodels-vs.-custommodeldata.md](../../general-usage/faq/itemmodels-vs.-custommodeldata.md "mention").
{% endhint %}

Need more than one stacked sprite (e.g. a base layer plus an overlay)? `texture` also accepts a **list** — each entry becomes a layer (`layer0`, `layer1`, …), drawn bottom to top:

```yaml
ruby:
  material: PAPER
  Pack:
    texture:
      - nexo:item/ruby        # layer0 (bottom)
      - nexo:item/ruby_shine  # layer1 (drawn on top)
```

### Advanced — a 3D model

When a flat sprite isn't enough, design a model in [BlockBench](https://www.blockbench.net/) and reference its exported `.json` with `Pack.model`. The item then renders with full 3D geometry wherever it's shown.

```yaml
ruby_chalice:
  itemname: "<red>Ruby Chalice"
  material: PAPER
  Pack:
    model: nexo:item/ruby_chalice
```

**File layout** — the model JSON goes under `models`, and any PNGs it uses go under `textures`:

```
📁 Nexo/pack/assets/nexo
├── 📁 models/item
│   └── 📑 ruby_chalice.json   ← exported from BlockBench
└── 📁 textures/item
    └── 📑 ruby_chalice.png    ← texture(s) the model points at
```

**Workflow**

1. Build your model in BlockBench and paint/assign its texture.
2. Export it as a **Java Block/Item model** (`File → Export → Java Block/Item Model`).
3. Drop the `.json` into `assets/nexo/models/...` and its texture(s) into `assets/nexo/textures/...`.
4. Make sure the texture paths **inside** the `.json` match where you placed the PNGs — a mismatch here is the usual cause of a purple-and-black (missing texture) model.
5. Reference the model with `Pack.model` as shown above.

{% hint style="info" %}
A BlockBench model already defines its own parent and geometry, so `Pack.parent_model` only applies to Nexo's **generated** models (the `texture` path above), where it defaults to `item/generated`. You rarely need to set it for a full 3D model.
{% endhint %}

***

### Invisible Item (1.21.4+)

To make an invisible item with Nexo, you can use the Nexo provided ItemModel `nexo:empty`.\
This will render nothing for that Item no matter where it is used.

Here is a basic config-example for an invisible NexoItem

```yaml
invisible_item:
  Components:
    item_model: nexo:empty
```

You can also use this in any other plugin, assuming they allow you to specify the ItemModel of your Item.

### Oversized Items in GUI (1.21.6+)

As of 1.21.6+, Mojang made changes to how items render in the GUI.\
By default they are no longer allowed to go beyond their 16x16 grid, but added an option called `oversized_in_gui` to ItemModels to return this behaviour.\
This works best when using ItemModels ([itemmodels-vs.-custommodeldata.md](../../general-usage/faq/itemmodels-vs.-custommodeldata.md "mention")).\
In Nexo you can use this for your items by following the below example;

```yaml
my_oversized_item:
  material: PAPER
  Pack:
    oversized_in_gui: true
    model: my_oversized_model
  Components:
    item_model: nexo:my_oversized_item
```

{% hint style="info" %}
In Nexo 1.17+ there is `Pack.generation.force_oversized_in_gui` which can be used to change the default state of every item if you don't want to specify it for individual items
{% endhint %}

Here we do not use CustomModelData as that would apply to all items using PAPER.\
If you are not sure what an ItemModel is, think of it as the **base model** of an item.\
By default all items using the material PAPER will use **minecraft:paper.**\
By specifying our own ItemModel here, we are changing the base-model of our item, preventing any conflicts or issues, and Nexo can properly mark the config

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

***

{% hint style="info" %}
All the methods below support a `BLANK_texture` or `BLANK_textures` as well as models if all you have is a PNG\
For example for a 2D bow with different pulling-stages.
{% endhint %}

### Dyeable Items

```yaml
myitem:
  Pack:
    model: example
    dyeable_model: example_dyeable
    #texture: example
    #dyeable_texture: example_dyeable
```

### Blocking Model (Shields)

```yaml
myitem:
  Pack:
    model: example_shield
    blocking_model: example_shield_blocking
    #texture: example_shield
    #blocking_texture: example_shield_blocking
```

### Pulling Models (Bows / Crossbow)

```yaml
myitem:
  Pack:
    model: default/combat_bow
    pulling_models:
      - default/combat_bow_pulling_0
      - default/combat_bow_pulling_1
      - default/combat_bow_pulling_2
```

### Charged Model (Crossbow)

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

### Cast Model (Fishing Rods)

```yml
myitem:
  Pack:
    model: default/fishing_rod
    cast_model: default/fishing_rod_cast
    #texture: default/fishing_rod
    #cast_texture: default/fishing_rod_cast
```

### Damaged Model (Based on durability)

```yml
myitem:
  Pack:
    model: default/diamond_sword
    damaged_models:
      - default/diamond_sword_damaged1
      - default/diamond_sword_damaged2
      - default/diamond_sword_damaged3
```

### Composite Models

```yaml
myitem:
  Pack:
    model: default/diamond_sword
    composite_models:
      - default/background
      - default/item
      - default/overlay
```
