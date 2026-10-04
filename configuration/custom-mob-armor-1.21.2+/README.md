# 🐴 Custom Mob Armor

Mob armor uses the same `CustomArmor`-section as [Custom Player Armors](../custom-armors.md).\
Supported layers are `wolf_armor`, `llama_armor`, `horse_armor` & `nautilus_armor` (1.21.11+).

```yaml
forest_wolf_armor:
  itemname: "Forest Wolf Armor"
  material: WOLF_ARMOR
  Pack:
    texture: nexo:item/nexo_armor/forest_wolf_armor_icon
  CustomArmor:
    id: forest_wolf_armor
    wolf_armor: nexo:item/nexo_armor/forest_wolf_armor
forest_llama_armor:
  itemname: "Forest Llama Carpet"
  material: PAPER
  Pack:
    texture: nexo:item/nexo_armor/forest_llama_armor_icon
  CustomArmor:
    id: forest_llama_armor
    llama_armor: nexo:item/nexo_armor/forest_llama_armor
forest_horse_armor:
  itemname: "Forest Horse Armor"
  material: DIAMOND_HORSE_ARMOR
  Pack:
    texture: nexo:item/nexo_armor/forest_horse_armor_icon
  CustomArmor:
    id: forest_horse_armor
    horse_armor: nexo:item/nexo_armor/forest_horse_armor
forest_nautilus_armor:
  itemname: "Forest Nautilus Armor"
  material: DIAMOND_NAUTILUS_ARMOR
  Pack:
    texture: nexo:item/nexo_armor/forest_nautilus_armor_icon
  CustomArmor:
    id: forest_nautilus_armor
    nautilus_armor: nexo:item/nexo_armor/forest_nautilus_armor
```

Nexo fills in the Equippable-Component from the layer, so even a `PAPER` item works.\
In the example above, `forest_llama_armor` gets `slot: BODY` and `allowed_entity_types: [LLAMA, TRADER_LLAMA]`.

{% hint style="info" %}
If you are unsure how to reference a TextureFile in a NexoItem config; [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}
