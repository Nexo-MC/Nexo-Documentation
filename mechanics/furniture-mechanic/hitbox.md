# 🎯 Hitbox

Furnitures can have two types of hitboxes, with collision & without collision\
Collision hitboxes are normal barrier-blocks, whilst non-solid ones are interaction-entities.\
Interaction-entities have no collision, but can be any width and height, unlike barriers which are normal 1x1x1 blocks.Below are examples of how to use both.\
\
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

\
**Interaction-Entity Hitboxes** takes an **offset, width and height**

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
