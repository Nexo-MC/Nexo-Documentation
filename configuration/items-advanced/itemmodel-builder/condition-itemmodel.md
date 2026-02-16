---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Condition ItemModel

A **Condition ItemModel**, is a true/false statement to determine what to show the client.\
Vanilla makes use of this in Bows to show a different one when its being used/pulled and not.\
\
There are other ways to use this as it has several properties it can use for this condition.\
Recommend to check the [Minecraft Wiki](https://minecraft.wiki/w/Items_model_definition#condition) for an always up-to-date list.

Below is an example for showing a different Model if an item is broken vs when not;

```yaml
custom_sword:
  ItemModel:
    type: condition
    property: broken
    on_true:
      type: model
      model: namespace:custom_sword_broken
    on_false:
      type: model
      model: namespace:custom_sword
```

{% hint style="info" %}
You can also chain these to use different ItemModel-types inside the true/false ItemModels here for very complex items
{% endhint %}
