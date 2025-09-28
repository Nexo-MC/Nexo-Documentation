---
hidden: true
---

# 📜 Main Changelog

### **\[General]**

* Change CustomSound handling
  * `sound.yml` -> `sounds.yml`
  * Allow for all optional-properties specified on the [wiki](https://minecraft.wiki/w/Sounds.json#File_structure)
  * Refactor to allow for custom namespaces
* Multi-font Glyphs

### **\[ResourcePack]**

* Entirely new pack-structure to improve importing external packs
  * A detailed explanation can be found here
* ResourcePack is now sent before player loads in the server (Configuration Phase)
* Automatic ModelEngine-pack Import
* New PackServer options
  * POLYMATH - same as in 1.x
  * SELFHOST - SelfHost/Localhost the pack on your server itself
* Improve pack-merging and conflict handling
* Future Default Assets are now included in a external pack instead of in the Jar itself
* Built-in Pack-Obfuscator

### **\[Furniture]**

* Packet-based Furniture & Furniture Hitboxes
  * Aims to fix tons of issues with existing furniture leaving behind hitboxes & not updating properly
* Support for multiple interaction-hitboxes
* Seat-mechanic is no longer bound to barrierHitbox
  * Meaning you can define as many seats as you want at whatever position you want
* Toggleable-light mechanic for lamps and other such furniture
* Allow furniture placed on slabs, carpets and other non full blocks

### **\[Custom Blocks]**

* NoteBlock & StringBlock mechanics moved under new common `CustomBlock-Mechanic`
* NoteBlock-mechanic custom\_variation limit 749 -> 1149
* NoteBlock-mechanic can now be used in beacons
* NoteBlock-mechanic can now be used without disabling vanilla noteblock functionality
  * Disabled by default in mechanics.yml
* Remade Custom-Block Breaking System
  * Closer to vanilla logic with tool-speed modifiers
  * Fixes bunch of minor bugs with breaking & sound from 1.X
* StringBlocks can now be placed ontop of water similar to Lilypads with `placeable_on_water`

### **\[Custom Armor]**

* SHADER CustomArmor is no longer supported as TRIMS work on all supported versions
  * If you still for some reason want to use SHADER method, you can use it by manually handling ResourcePackFiles
  * Follow the README here for [FancyPants](https://github.com/Ancientkingg/fancyPants) or the more optimized [LessFancyPants](https://github.com/Godlander/lessfancypants)

### **\[Removed]**

* Dropped support for 1.20.3 & below
* Block-Mechanic (Mushroom Blocks), BigMining-, Hat-, Aura-, Skinnable-, BottledExp-, Durability-, Efficiency-, Repair-, Consumable-, ConsumablePotionEffects-, Food-, MusicDisc-, BedrockBreak-, Watering- & Farmblock-Mechanic have been removed
* BossShopPro compatibility

### **\[Developer API]**

The API has naturally had tons of breaking changes and new additions. A detailed changelog can be found here
