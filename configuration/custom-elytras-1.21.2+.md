---
cover: ../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png
coverY: 0
---

# 🪽 Custom Elytras

Custom textured elytras use the same `CustomArmor`-section as [Custom Player Armors](custom-armors.md), with the wings defined through the `elytra` layer.

```yaml
forest_elytra:
  itemname: "Forest Elytra"
  material: ELYTRA
  Pack:
    texture: nexo:item/nexo_armor/forest_elytra_icon
  CustomArmor:
    id: forest_elytra
    elytra: nexo:item/nexo_armor/forest_elytra
```

{% hint style="warning" %}
An elytra needs its own `id`.\
If it shares one with an armor-set, the wings would also render on the chestplate of that set
{% endhint %}

Nexo fills in the Equippable-Component for you, with `slot: CHEST` and `asset_id: nexo:forest_elytra`.\
When not using `ELYTRA` as the material, also add the `glider` component so the item can actually fly.

{% hint style="info" %}
If you are unsure how to reference a TextureFile in a NexoItem config; [#how-do-i-reference-a-resourcepack-file-in-a-config](../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Forest Elytra included with Nexo</p></figcaption></figure>
