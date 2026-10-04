# 🪢 Custom Harness (1.21.6+)

With the Happy Ghast came a new type of equipment, the Harness.\
Custom harnesses use the same `CustomArmor`-section as [Custom Player Armors](../custom-armors.md), through the `harness` layer.

```yaml
forest_harness:
  material: PAPER
  itemname: "Forest Harness"
  Pack:
    texture: nexo:items/nexo_armor/forest_harness_icon
  CustomArmor:
    id: forest_harness
    harness: nexo:items/nexo_armor/forest_harness
```

Nexo fills in the Equippable-Component with `slot: BODY` and `allowed_entity_types: [HAPPY_GHAST]`.

{% hint style="info" %}
If you are unsure how to reference a TextureFile in a NexoItem config; [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}
