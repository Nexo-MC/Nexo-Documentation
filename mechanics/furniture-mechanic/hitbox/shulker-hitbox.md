# 📤 Shulker Hitbox

**Shulker-Entity Hitboxes** takes an **offset, scale, length** and **direction**\
**Offset** only supports full blocks, as shulkers are forcefully put at a full block. Meaning you cannot offset it by 0.5 blocks\
**Scale** is a single integer and determines the scale of the furniture. You cannot scale only the height, like with Interaction-Entity Hitboxes\
**Length** determines the extra length of the hitbox, and can be between 1..2\
**Direction** determines the way the hitbox faces, if not specified, defaults to UP

```yaml
myitem:
  Mechanics:
    furniture:
      hitbox:
        shulker: 0,0,0 1.0 1.0  #offset scale length direction visible
        #shulkers:
        #  - 0,0,0 1.0 1.0
        #  - 1,0,0 1.2 1.5 EAST
        #  - -1,0,0 0.8 2.0 UP
```

{% hint style="info" %}
If you struggle with finding the accurate hitbox-size you want for shulker-hitboxes, you can make them temporarily visible. To do this simply add `true` after the length or direction argument
{% endhint %}
