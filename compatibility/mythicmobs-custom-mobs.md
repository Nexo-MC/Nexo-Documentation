---
description: >-
  MythicMobs allows you to create custom mobs and bosses with advanced skills
  and attributes
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966831974004174858/unknown.png
coverY: 0
---

# MythicMobs - custom mobs

{% hint style="info" %}
If the plugin does not work with MythicMobs, use version 5.7.0+.
{% endhint %}

## How to use a nexo item for the drops?

### Usage

`nexo [nexo-itemid] [amount to drop(number or region)] [chance to drop(0-1)]`

### Example

`nexo my_item 3-4 0.75`\
This means that it has **75** percent chance to drop **3 to 4 custom\_material** items.

## How to equip your mob with a nexo item?

### Usage

`nexo [slot] [nexo-itemid]`

#### Slots

* 0, mainhand, weapon
* 1, boots, shoes
* 2, leggings, pants
* 3, chestpiece, chestplate, body
* 4, helmet, helm
* 5, shield

_5 is OffHand, but you can't put **offhand**, because MythicMobs's Author didn't put the alias._

### Example

`nexo mainhand my_item`\
It means that you put a **custom\_sword** item in **MainHand**.\
`nexo 3 my_item`\
It means that you put a **custom\_chestplate** item in **ChestPlate** slot (as an armor)
