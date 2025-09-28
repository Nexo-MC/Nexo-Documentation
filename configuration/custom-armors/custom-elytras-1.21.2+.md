---
cover: ../../.gitbook/assets/image (1) (1) (1) (1) (1).png
coverY: 0
---

# 🪽 Custom Elytras (1.21.2+)

This is a sub-feature of using COMPONENT based CustomArmor, letting you make custom textured elytras.\
The pattern for adding it is exactly the same as explained in [CustomArmor](components.md)-section, with some slight differences. The Equippable-Component model-property is suffixed with \_elytra, and the itemid follows the scheme `armorname_elytra`&#x20;

Here is a config example:

```yaml
forest_elytra:
  itemname: "Forest Elytra"
  material: ELYTRA
  Pack:
    texture: nexo:item/nexo_armor/forest_elytra_icon
  Components:
    equippable:
      slot: CHEST
      asset_id: nexo:forest_elytra
```

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Forest Elytra included with Nexo</p></figcaption></figure>
