---
description: >-
  The different mechanics available by default and their configurations sorted
  by category
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825489098489856/unknown.png
coverY: 0
---

# Other Mechanics

## Miscellaneous

### Backpack

This allows you to turn any item into a backpack.

{% hint style="info" %}
This mechanic might cause duplication issues!\
If you find any please open a [bug-report](all-mechanics.md) and we will fix them as soon as possible!\\
{% endhint %}

```yml
backpack:
  itemname: backpack
  material: PAPER
  Components:
    max_stack_size: 1
  Mechanics:
    backpack:
      rows: 4
      title: "<red>Backpack"                  #Optional, Default: "Backpack"
      open_sound: "entity.shulker.open"       #Optional, Default: "entity.shulker.open"
      close_sound: "entity.shulker.close"     #Optional, Default: "entity.shulker.close"
      blacklist:                              #Optional, add which items are not allowed
        nexo_items:
          - item_id
          - item_id2
        materials:
          - DIAMOND
```

### Misc Mechanic

{% hint style="warning" %}
On 1.20.5+ use the new [FireResistant-Component](../configuration/items-advanced.md) instead of **burns\_in\_x**
{% endhint %}

This mechanic has a bunch of small changes you can make to your item.\
What they each do should be pretty self-explanatory.

```yaml
myitem:
  Mechanics:
    misc:
      breaks_from_cactus: true
      burns_in_fire: true
      burns_in_lava: true
      disable_vanilla_interactions: false
      can_strip_logs: false
      piglins_ignore_when_equipped: false
      compostable: false
      allow_in_vanilla_recipes: true
```

### Commands

This allows you to execute commands (as the console, a player or op player). If this option is not often the most elegant it has the merit of simplifying a lot of things. You can create a cooldown between usages, check if the player has a specific permission and use the item (understand decrease its amount by one when the command is performed).

```yaml
myitem:
  Mechanics:
    commands:
      cooldown: 5 # example cooldown in seconds. This is optional
      permission: "my.awesome.perm" # required permission. This is optional
      one_usage: true # should the amount decrease when used? Default: false
      console:
        # e.g. to kill the player
        - "kill %p%"
      player:
        # e.g. the player performs /spawn
        - "spawn"
      opped_player:
        # e.g. the player gives himself a diamond sword
        - "give diamond_sword 1"
```

### Armor Effects

This allows you to bind a Potion Effect to an armor (or a hat) so that when you equip it you'll get the effect.\
[Here](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/potion/PotionEffectType.html) is a list of all potion effect types available.

```yaml
myitem:
  Mechanics:
    armor_effects:
      night_vision: # the potion effect type
        duration: 10
        amplifier: 0
        ambient: true # Makes potion effect produce more, translucent, particles.
        particles: true # whether this effect has particles or not
        icon: true # whether this effect has an icon or not
```

You can also make an effect only apply if the entire set it equipped.

```yaml
myitem:
  Mechanics:
    armor_effects:
      night_vision:
        requires_full_set: true
        ...
```

### clickAction

This mechanic allows you to run various events when a player clicks a block or furniture. It is very customizable, so it also has a [dedicated tutorial page](clickaction-mechanic.md).

### ItemType

With this mechanic, you can change the item type detected by NexoBlocks. Make sure to use a type declared [inside the block mechanic](custom-block-mechanics/noteblock-mechanic/#global-configuration).

```yaml
myitem:
  Mechanics:
    itemtype:
      value: SUPER_MATERIAL # your itemType
```

### Soulbound

With this mechanic, you can avoid the players to lose their item when they die.

```yaml
myitem:
  Mechanics:
    soulbound:
      lose_chance: 0
```

### Custom mechanic

This mechanic allows you to customize events, conditions and actions.\
Since it is a quite rspecial mechanic, it has its [dedicated tutorial page](custom-mechanic.md).

## Combat

### Thor

Have you ever dreamed of being able to throw lightning bolts? This is for you.

```yaml
myitem:
 Mechanics:
   thor:
    lightning_bolts_amount: 5
    random_location_variation: 1.5
    delay: 20000 # in milliseconds (20000ms = 20s)
```

* **lightning\_bolts\_amount**: how many lightning bolts will be spawned?
* **random\_location\_variation**: the random variation range between bolts (in blocks)
* **delay**: delay between usage in milliseconds (1000ms = 1s)

### Lifesteal

Want to steal hearts to your opponents when you hit them?

```yaml
myitem:
  Mechanics:
    lifesteal:
      amount: 2 # the amount of 1/2 hearts that you'll steal to your opponents
```

### EnergyBlast

EnergyBlast is a very cool mechanic that creates a cone of particles to attack entities.

```yaml
myitem:
  Mechanics:
    energyblast:
      delay: 20000
      length: 5
      damage: 10.0
      particle:
        type: REDSTONE #Only REDSTONE particle can change size and color.
        size: 1
        color:
          red: 0
          green: 255
          blue: 255
```

### Witherskull

Send wither skulls when right clicking!

```yaml
myitem:
  Mechanics:
    witherskull:
      charged: false # a charged skull can break blocks
      delay: 3000 # in milliseconds (3000ms = 3s)
```

## Farming

### Harvesting

Harvesting allows you to recolt and replant automatically wheat in a certain radius.

```yaml
myitem:
  Mechanics:
    harvesting:
      cooldown: 10000 # 10 seconds between usages
      radius: 5 # blocks surrounding the clicked block
      height: 3 # high
```

### Smelting

Smelting allows you to instantly melt iron and gold ores when you mine them. This supports fortune and silktouch.

```yaml
myitem:
  Mechanics:
    smelting:
      enabled: true
      play_sound: true
```
