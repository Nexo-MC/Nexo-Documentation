# 🐖 Custom Saddles (1.21.5+)

When using COMPONENT type CustomArmor, Nexo allows you to easily create custom saddles for various mobs. The list of supported entities are: **camel, donkey, horse, mule, pig, skeleton\_horse, strider, zombie\_horse, nautilus & camel\_husk**

Similar to all other CustomArmor sections, the pattern is \`mobtype\_saddle\`.

```yaml
forest_saddle:
  itemname: Forest Saddle
  type: SADDLE
  Pack:
    texture: nexo:items/forest_armor/forest_saddle_icon
    CustomArmor:
      pig_saddle: nexo:items/forest_armor/forest_pig_saddle
      horse_saddle: nexo:items/forest_armor/forest_horse_saddle
  Components:
    equippable:
      slot: BODY
      allowed_enity_types: [ PIG, HORSE ]
```

{% hint style="info" %}
If you are unsure how to reference a TextureFile in a NexoItem config; [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}

Here `Pack.CustomArmor.x_saddle` points to where we put the texture for the harness itself, with `Pack.texture` the icon.\
We also have to set the `allowed_entity_types` in our EquippableComponent for Nexo to properly handle the remaining properties
