# 🔳 Interaction Hitbox

**Interaction-Entity Hitboxes** takes an **offset, width and height** & have no collision\
You can view the hitboxes by toggling on Hitboxes in-game with F3+B

```yaml
myitem:
  Mechanics:
    furniture:
      hitbox:
        interactions:
        # - offset width,height
          - 0,0,0 1,1
          - 1,0,0 1,2.0
          - -1,0,0 1,2.2
```
