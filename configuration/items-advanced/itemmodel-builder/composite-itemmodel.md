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

# Composite ItemModel

A **Composite ItemModel**, is a list of ItemModels that should be layered over eachother.\
Recommend to check the [Minecraft Wiki](https://minecraft.wiki/w/Items_model_definition#composite) for an always up-to-date list.

Below is an example for showing an Item with a Model background

```yaml
custom_diamond:
  ItemModel:
    type: composite
    models:
      - type: model
        model: namespace:custom_diamond
      - type: model
        model: namespace:background
```

{% hint style="info" %}
You can also chain these to use different ItemModel-types inside each composite-entry here for very complex items
{% endhint %}
