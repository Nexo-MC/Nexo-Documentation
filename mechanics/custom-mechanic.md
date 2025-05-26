---
description: >-
  This mechanism allows you to realize an extremely customizable mechanism
  without programming
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825489098489856/unknown.png
coverY: 0
---

# Custom Mechanic

## How does it work?

This mechanic is for items only and does not work with blocks/furniture.\
For that check the [clickAction mechanic](clickaction-mechanic.md). The mechanics let you create subsections composed of 3 parts:

* **Event**: when is this mechanic triggered? e.g. when you right-click on a block
* **Conditions**: a set of conditions that must be satisfied. e.g. having a permission
* **Actions**: a set of actions to perform. e.g. send a command or a message

{% hint style="info" %}
An optional settings called one\_usage allows you to imitate the use of an item at 1.
{% endhint %}

## A comprehensive example

```yaml
myitem:
  Mechanics:
    custom:
      test:
        one_usage: false
        event: "CLICK:right:all"
        conditions:
          - '#player.hasPermission("example.permission")'
        actions:
          - "[console] give <player> cooked_beef 1"
```

In this example, the subsection `test` defines a custom mechanic triggered when someone right click (on a block or in the air).\
If this player has the permission `example.permission`, the console will perform the give command and replace \<player> by the player name.\
The item won't be consumed (one\_usage: false).

## Available events

### CLICK:click\_type:target\_type[^1], DROP[^2], PICKUP[^3], BREAK[^4], EQUIP[^5], UNEQUIP[^6], INV\_CLICK[^7], DEATH[^8]

## Available conditions

### HAS\_PERMISSION:the.permission

**the.permission**: `The permission required by the player using the item`

## Available actions

### Command-Action

This action lets you run a command either from console or as the player

```yaml
myitem:
  Mechanics:
    custom:
      mycustom:
        event: "CLICK:right:all"
        actions:
          - "[console] minecraft:give <player> minecraft:paper 2"
```

### Message-Action

This action lets you send a Message to the player with a customizable message

```yaml
myitem:
  Mechanics:
    custom:
      mycustom:
        event: "CLICK:right:all"
        actions:
          - "[message] <red>some message <gradient:red:blue>with MiniMessage support"
```

### ActionBar-Action

This action lets you send an ActionBar to the player with a customizable message

```yaml
myitem:
  Mechanics:
    custom:
      mycustom:
        event: "CLICK:right:all"
        actions:
          - "[actionbar] <red>some message <gradient:red:blue>with MiniMessage support"
```

### Sound-Action

This action lets you play a sound at a location or at a target with customizable values

**source -** The source of the sound ([List of sources](https://jd.advntr.dev/api/4.21.0/net/kyori/adventure/sound/Sound.Source.html))\
**volume** - The volume to play the sound with\
**pitch** - The pitch to play the sound with\
**self** - If the sound sound be played at the Player and not at a location

Followed by the sound-key to play

```yaml
myitem:
  Mechanics:
    custom:
      mycustom:
        event: "CLICK:right:all"
        actions:
          - "{source=AMBIENT volume=0.1 pitch=1} [sound] namespace:soundkey"
```

[^1]: Called when you click with the item.

    **mouse\_click\_type**: `[ right, left, all ]`\
    **target\_type**: `[ block, air, all ]`

[^2]: Called when you drop the item.

[^3]: Called when you pick up the item.

[^4]: Called when a player breaks an item.

[^5]: Called when a player equips an item.

[^6]: Called when a player unequips an item.

[^7]: Called when a player clicks an item in an inventory.

[^8]: Called when a player dies and would normally drop the given item.
