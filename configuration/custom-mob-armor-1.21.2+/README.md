# 🐴 Custom Mob Armor (1.21.2+)

Nexo allows you to automate the generation of several types of mob-armor.\
Mainly Wolf-Armor, Horse-Armor & Llama-Armor. These follow the same pattern as [components.md](../custom-armors/components.md "mention") Player Armor, with the ItemID- & Armor-pattern Texture being `armorname_wolf_armor`_,_ `armorname_horse_armor` & `armorname_llama_armor` .

```yaml
forest_wolf_armor:
  itemname: "Forest Wolf Armor"
  material: WOLF_ARMOR
  Pack:
    texture: nexo:item/nexo_armor/forest_wolf_armor_icon
    CustomArmor:
      wolf_armor: nexo:item/nexo_armor/forest_wolf_armor
forest_llama_armor:
  itemname: "Forest Llama Carpet"
  material: PAPER
  Pack:
    texture: nexo:item/nexo_armor/forest_llama_armor_icon
    CustomArmor:
      llama_armor: nexo:item/nexo_armor/forest_llama_armor
forest_horse_armor:
  itemname: "Forest Horse Armor"
  material: DIAMOND_HORSE_ARMOR
  Pack:
    texture: nexo:item/nexo_armor/forest_horse_armor_icon
    CustomArmor:
      horse_armor: nexo:item/nexo_armor/forest_horse_armor
forest_nautilus_armor:
  itemname: "Forest Nautilus Armor"
  material: DIAMOND_NAUTILUS_ARMOR
  Pack:
    texture: nexo:item/nexo_armor/forest_nautilus_armor_icon
    CustomArmor:
      horse_armor: nexo:item/nexo_armor/forest_nautilus_armor
```

{% hint style="info" %}
If you are unsure how to reference a TextureFile in a NexoItem config; [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}
