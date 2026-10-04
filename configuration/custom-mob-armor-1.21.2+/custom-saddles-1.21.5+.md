# 🐖 Custom Saddles (1.21.5+)

Custom saddles use the same `CustomArmor`-section as [Custom Player Armors](../custom-armors.md).\
The supported layers are `camel_saddle`, `donkey_saddle`, `horse_saddle`, `mule_saddle`, `pig_saddle`, `skeleton_horse_saddle`, `strider_saddle` & `zombie_horse_saddle`.\
On 1.21.11+ there is also `nautilus_saddle` & `camel_husk_saddle`.

One item can define several saddle-layers, letting the same saddle fit multiple mobs.

```yaml
forest_saddle:
  itemname: Forest Saddle
  material: SADDLE
  Pack:
    texture: nexo:items/forest_armor/forest_saddle_icon
  CustomArmor:
    id: forest_saddle
    pig_saddle: nexo:items/forest_armor/forest_pig_saddle
    horse_saddle: nexo:items/forest_armor/forest_horse_saddle
```

Nexo fills in the Equippable-Component with `slot: SADDLE` and `allowed_entity_types` set to the mobs of the defined layers, `[PIG, HORSE]` in the example above.\
Set `allowed_entity_types` yourself if you want something else.

{% hint style="info" %}
If you are unsure how to reference a TextureFile in a NexoItem config; [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}
