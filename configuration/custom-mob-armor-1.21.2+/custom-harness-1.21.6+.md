# 🪢 Custom Harness (1.21.6+)

With the new Happy Ghast entity, there is a new type of Equipment, the Harness.\
Nexo allows you to easily register custom harnesses like [custom-saddles-1.21.5+.md](custom-saddles-1.21.5+.md "mention").

To do so simply follow the general pattern for all NexoEquipment. Below is an example;

```
forest_harness:
  type: PAPER
  itemname: "Forest Harness"
  Pack:
    parent_model: item/generated
    texture: nexo:items/nexo_armor/forest_harness_icon
    CustomArmor:
      harness: nexo:items/nexo_armor/forest_harness
  Components:
    equippable:
      allowed_entity_types: [ HAPPY_GHAST ]
      slot: BODY
```

{% hint style="info" %}
If you are unsure how to reference a TextureFile in a NexoItem config; [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq.md#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}

Here `Pack.CustomArmor.harness` points to where we put the texture for the harness itself, with `Pack.texture` the icon.\
We also have to set the `allowed_entity_types` in our EquippableComponent for Nexo to properly handle the remaining properties
