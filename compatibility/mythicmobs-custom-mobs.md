---
description: >-
  MythicMobs allows you to create custom mobs and bosses with advanced skills
  and attributes
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966831974004174858/unknown.png
coverY: 0
---

# MythicMobs - custom mobs

MythicMobs is a plugin for making highly customizable mobs and bosses.\
This page explains how you can make said mobs drop a NexoItem or equip them with a NexoItem

Below is an example config of how to define Equipment & Drops (also applies to DropTables)

```yaml
ExampleMob:
  Type: WITHER_SKELETON
  Equipment:
    - IRON_HELMET HEAD
    - nexo:forest_sword HAND
    - nexo:forest_shield OFFHAND
  Drops:
    - nexo forest_chestplate 1to2 1.0
    - #nexo itemid amount probability
```
