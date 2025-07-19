# 👻 Ghast Hitbox

**Ghast-Entity Hitboxes** are a feature for 1.21.6+ and allows for a scalable collision entity hitbox.\
It takes an **offset, scale & a rotation** property, with an optional debug true/false visible statement.\
Scale is 0.25 by default unless specified otherwise, to make it a 1-block sized hitbox.\
Rotation is 0 by default unless specified otherwise

{% hint style="warning" %}
This is only available for 1.21.6+ servers
{% endhint %}

```yaml
myitem:
  Mechanics:
    furniture:
      hitbox:
        ghasts:
        # - offset scale rotation visible
          - 0,0,0 0.25
          - 0,1,0 0.25 45
          - 0,2,0 0.25 true
```
