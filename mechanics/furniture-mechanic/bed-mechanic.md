---
description: Feature added in Nexo 1.4
cover: ../../.gitbook/assets/huge_2025-04-23_14.33.14.png
coverY: 0
---

# 🛏️ Bed Mechanic

Furniture can also be used as beds. Bed-positions can be configured like below.\
This can be used for both replicating normal beds, or just a furniture to lie down on.\
It is configured with an offset and properties for if it should skip nights and reset phantoms.\
A normal bed has both these to true, but you can disable it for say a bench if you want to.

```yaml
myitem:
  Mechanics:
    furniture:
      beds:
        - 0,0,0 true true # x,y,z skip-night reset-phantoms
```

<figure><img src="../../.gitbook/assets/huge_2025-04-23_14.33.14.png" alt=""><figcaption><p>Double-Bed included in Nexo's Default Items</p></figcaption></figure>
