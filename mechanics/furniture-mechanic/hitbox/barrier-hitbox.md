# 🚧 Barrier Hitbox

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
