# 🎯 Hitbox

Furnitures come with two core types, with and without collision-interactions.\
Collision hitboxes are normal barrier-blocks, whilst non-solid ones are interaction-entities.\
Interaction-entities have no collision, but can be any width and height, unlike barriers which are normal 1x1x1 blocks.Below are examples of how to use both.\
\
There are also two other types of hitboxes with collision but some other extra functionalities, Shulker- & Ghast-type hitboxes. Ghast Hitboxes are only available for 1.21.6+

<figure><img src="../../.gitbook/assets/2025-06-20_16-51.png" alt=""><figcaption><p>Showing off Barrier, Interaction, Shulker &#x26; Ghast Hitboxes</p></figcaption></figure>

### Barrier-Block Hitbox

**Barrier** hitboxes can be formatted at a given offset from the furniture.\
They also support integer-ranges to shorten repeating lines for larger hitboxes

```yaml
myitem:
  Mechanics:
    furniture:
      hitbox:
        barriers:
          - 0,0,0
          - 0,0,1
          - 0,0,2
          - 1,0,0..2
```

### **Interaction-Entity Hitbox**

**Interaction-Entity Hitboxes** takes an **offset, width and height** & have no collision

```yaml
myitem:
  Mechanics:
    furniture:
      hitbox:
        interactions:
          - 0,0,0 1,1
          - 1,0,0 1,2.0
          - -1,0,0 1,2.2
```

### Shulker-Entity Hitbox

**Shulker-Entity Hitboxes** takes an **offset, scale, length** and **direction**\
**Offset** only supports full blocks, as shulkers are forcefully put at a full block. Meaning you cannot offset it by 0.5 blocks\
**Scale** is a single integer and determines the scale of the furniture. You cannot scale only the height, like with Interaction-Entity Hitboxes\
**Length** determines the extra length of the hitbox, and can be between 1..2\
**Direction** determines the way the hitbox faces, if not specified, defaults to UP

{% hint style="warning" %}
This is only available for 1.20.5+ servers\
Should also be noted that the shulker-entity head will be visible on 1.21.1 & below\
It will be invisible for 1.21.2 and above as long as [https://bugs.mojang.com/browse/MC-278123](https://bugs.mojang.com/browse/MC-278123) is not fixed
{% endhint %}

```yaml
myitem:
  Mechanics:
    furniture:
      hitbox:
        shulkers:
          - 0,0,0 1.0 1.0
          - 1,0,0 1.2 1.5 EAST
          - -1,0,0 0.8 2.0 UP
```

{% hint style="info" %}
If you struggle with finding the accurate hitbox-size you want for shulker-hitboxes, you can make them temporarily visible. To do this simply add `true` after the length or direction argument
{% endhint %}

### Ghast-Entity Hitbox

**Ghast-Entity Hitboxes** are a feature for 1.21.6+ and allows for a scalable collision entity hitbox.\
It takes an **offset & a scale** property, with an optional debug true/false visible statement.\
Scale is 0.25 by default unless specified otherwise, to make it a 1-block sized hitbox.

{% hint style="warning" %}
This is only available for 1.21.6+ servers
{% endhint %}

```yaml
myitem:
  Mechanics:
    furniture:
      hitbox:
        ghasts:
          - 0,0,0 0.25
          - 0,1,0 0.25 true
```
