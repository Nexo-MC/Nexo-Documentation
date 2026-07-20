# 🔳 Interaction Hitbox

**Interaction-Entity Hitboxes** takes an **offset, width and height** & have no collision\
You can view the hitboxes by toggling on Hitboxes in-game with _F3+B_

```yaml
myitem:
  Mechanics:
    furniture:
      hitbox:
        interaction: 0,0,0 1,1  # offset width,height
        #interactions:
        #  - 0,0,0 1,1
        #  - 1,0,0 1,2.0
        #  - -1,0,0 1,2.2
```
