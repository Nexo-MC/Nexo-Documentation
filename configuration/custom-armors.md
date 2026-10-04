---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966823919917080626/unknown.png
coverY: 0
---

# ⛑️ Custom Player Armors

Nexo allows for creating fully custom Armor-sets for Players, using EquipmentModels.\
The same system also powers [Custom Elytras](custom-elytras-1.21.2+.md), [Custom Mob Armor](custom-mob-armor-1.21.2+/README.md), [Saddles](custom-mob-armor-1.21.2+/custom-saddles-1.21.5+.md) & [Harnesses](custom-mob-armor-1.21.2+/custom-harness-1.21.6+.md).

## How to configure your armor?

Every armor-piece gets a `CustomArmor`-section with an `id`.\
All items sharing the same `id` share one EquipmentModel, so the layer-textures only need to be defined once per set.

```yaml
forest_helmet:
  itemname: "Forest Helmet"
  material: CHAINMAIL_HELMET
  Pack:
    texture: nexo:item/nexo_armor/forest_helmet
  CustomArmor:
    id: forest
    layer1: nexo:item/nexo_armor/forest_armor_layer_1
    layer2: nexo:item/nexo_armor/forest_armor_layer_2
forest_chestplate:
  itemname: "Forest Chestplate"
  material: CHAINMAIL_CHESTPLATE
  Pack:
    texture: nexo:item/nexo_armor/forest_chestplate
  CustomArmor:
    id: forest
forest_leggings:
  itemname: "Forest Leggings"
  material: CHAINMAIL_LEGGINGS
  Pack:
    texture: nexo:item/nexo_armor/forest_leggings
  CustomArmor:
    id: forest
forest_boots:
  itemname: "Forest Boots"
  material: CHAINMAIL_BOOTS
  Pack:
    texture: nexo:item/nexo_armor/forest_boots
  CustomArmor:
    id: forest
```

`layer1` is the texture used for the helmet, chestplate & boots, `layer2` the one used for leggings.\
It does not matter which item of the set defines them.

{% hint style="info" %}
If you are unsure how to reference a TextureFile in a NexoItem config;\
[#how-do-i-reference-a-resourcepack-file-in-a-config](../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}

### The Equippable-Component

For the armor to render, the item needs an [Equippable-Component](items/components.md) pointing at the EquipmentModel.\
Nexo fills in anything you did not specify yourself and writes it back into your item-config:

* **`slot`** is taken from the material, so a `CHAINMAIL_HELMET` gets `HEAD`.\
  If the material is not wearable, like `PAPER`, the slot is taken from the layer instead.\
  Player-armor layers do not imply a slot, so a `PAPER` based armor-piece needs `slot` set manually
* **`asset_id`** is set to `nexo:<id>`, `nexo:forest` in the example above
* **`allowed_entity_types`** is set from the defined mob-layers, but only for the `BODY` & `SADDLE` slots

Anything else the Equippable-Component leaves out, like the equip-sound, is kept from the vanilla material.\
Values you do specify are never overridden.

```yaml
forest_helmet:
  material: PAPER
  CustomArmor:
    id: forest
  Components:
    equippable:
      slot: HEAD
      #asset_id: nexo:forest   # Added by Nexo if not specified
```

{% hint style="warning" %}
Do not point `asset_id` at a vanilla model like `minecraft:chainmail`.\
Nexo would not generate anything for it, and the item would render as normal chainmail
{% endhint %}

### 3D Helmets

A helmet using a 3D model does not need a `CustomArmor`-section.\
It only needs an Equippable-Component without an `asset_id`, so no armor-texture renders underneath the model.

```yaml
forest_helmet:
  itemname: "Forest Helmet"
  material: CHAINMAIL_HELMET
  Pack:
    model: nexo:item/nexo_armor/forest_helmet
  Components:
    equippable:
      slot: HEAD
```

Since the helmet is no longer part of the `forest` set, define `layer1` & `layer2` on another piece of the set instead.\
If the set uses [Armor Effects](../mechanics/all-mechanics.md#armor-effects) that require a full set, add `set: forest` to the helmet's `armor_effects`.

### Custom EquipmentModels

Nexo generates the EquipmentModel at `assets/nexo/equipment/<id>.json`.\
If your pack already contains a file at the `asset_id` path, Nexo leaves it untouched and uses yours instead.

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>Forest Armor Sets Nexo comes with (Player, Wolf, Horse &#x26; Llama)</p></figcaption></figure>
