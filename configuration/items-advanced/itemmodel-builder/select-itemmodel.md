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

# Select ItemModel

A **Select ItemModel**, is a set of conditions based on a specific property on the Item, that decided when to show what Model.\
Vanilla makes use of this in Crossbows to show the firework & arrow when the bow is charged.\
\
There are other ways to use this as it has several properties it can use for this condition.\
Recommend to check the [Minecraft Wiki](https://minecraft.wiki/w/Items_model_definition#select) for an always up-to-date list.

Below is an example for showing a different Model if an item has been renamed by a player;

```yaml
custom_diamond:
  ItemModel:
    type: select
    property: component
    component: custom_name
    cases:
      - when: "Renamed Diamond"
        model:
          type: model
          #References assest/namespace/models/renamed_diamond.json
          model: namespace:renamed_diamond
      - when:  # When can also be a list of conditions here
          - "Diamond1"
          - "Diamond2"
        model:
          type: model
          model: namespace:multiple_diamonds
    # A Fallback ItemModel in case none of the cases match
    fallback:
      type: model
      model: namespace:custom_diamond
```

{% hint style="info" %}
You can also chain these to use different ItemModel-types inside each case here for very complex items
{% endhint %}
