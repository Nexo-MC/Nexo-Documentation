---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966823919917080626/unknown.png
coverY: 0
---

# ⛑️ Custom Player Armors

Nexo allows for creating fully custom Armor-sets for Players, using EquipmentModels.&#x20;

{% hint style="info" %}
As of Nexo 1.28, the TRIMS method has been removed.\
If you are using an older Nexo release, you can find the old page [here](trims.md)
{% endhint %}

## How to configure your armor?

{% hint style="info" %}
Make sure that the ItemID of your NexoItem follows the pattern `armorname_armortype`.\
For the rest of the above set it would be `forest_chestplate`, `forest_leggings` and `forest_boots`.

Make sure your armor-layer files follow the format of **armorname**\_armor\_layer\_1/2.png.\
In the example below, we would need a **forest**\_armor\_layer\_1.png & **forest**\_armor\_layer\_2.png

\
If you are unsure how to reference a TextureFile in a NexoItem config;\
[#how-do-i-reference-a-resourcepack-file-in-a-config](../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}

```yaml
forest_helmet:
  material: PAPER    # Can be any material, armor-item or anything else
  Pack:
    # Optional, if not specified, Nexo searches for any texture
    # with the filename armorname_armor_layer_X.png
    #CustomArmor:
    #  layer1: nexo:item/nexo_armors/forest_armor_layer_1
    #  layer2: nexo:item/nexo_armors/forest_armor_layer_2
    texture: nexo:item/nexo_armors/forest_helmet
```

An Equippable-Component is also necessary for the armor to display correctly.\
Nexo will automatically assign it if it has not been manually specified.\
You can optionally manually assign the component if you want to.\
The value should be `nexo:armorname`, so in our example;

```yaml
forest_helmet:
  Components:
    equippable:
      slot: HEAD
      asset_id: nexo:forest
```

{% hint style="warning" %}
If using a 3D model for your helmet, do not specify Components.equippable.asset\_id
{% endhint %}

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>Forest Armor Sets Nexo comes with (Player, Wolf, Horse &#x26; Llama)</p></figcaption></figure>
