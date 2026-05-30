---
cover: ../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png
coverY: 0
---

# 🪽 Custom Elytras (1.21.2+)

Custom elytras are a sub-feature of [COMPONENT-based custom armor](components.md), letting you give the elytra a custom texture. The setup is the same as a normal armor piece, with two small differences:

* The item ID follows the scheme **`armorname_elytra`** (e.g. `forest_elytra`).
* The `equippable.asset_id` is suffixed with **`_elytra`** (e.g. `nexo:forest_elytra`).

Unlike armor pieces, an elytra uses a **single** wing texture rather than the two armor layers.

```yaml
forest_elytra:
  itemname: "Forest Elytra"
  material: ELYTRA
  Pack:
    # The icon shown in the inventory / when held.
    texture: nexo:item/nexo_armor/forest_elytra_icon
  Components:
    equippable:
      slot: CHEST
      asset_id: nexo:forest_elytra
```

{% hint style="info" %}
If you are unsure how to reference a texture file in a NexoItem config, see [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention").
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>The Forest Elytra included with Nexo</p></figcaption></figure>
