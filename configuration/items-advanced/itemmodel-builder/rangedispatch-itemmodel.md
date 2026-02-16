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

# RangeDispatch ItemModel

A **RangeDispatch ItemModel**, is a set of conditions based on a numerical property on the Item, that decided when to show what Model.\
This is what normally is used for CustomModelData as shown in [.](./ "mention")-example.\
\
There are other ways to use this as it has several properties it can use for this condition.\
Recommend to check the [Minecraft Wiki](https://minecraft.wiki/w/Items_model_definition#range_dispatch) for an always up-to-date list.

Below is an example for showing a different Model based on the amount of the item it is.

```yaml
custom_diamond:
  ItemModel:
    type: range_dispatch
    property: count
    entries:
      - threshold: 1
        model:
          type: model
          #References assest/namespace/models/single_custom_diamond.json
          model: namespace:single_custom_diamond  
      - threshold: 2
        model:
          type: model
          model: namespace:double_custom_diamond
      # Since the next threshold is 10, it means the client will use the previous one
      # until it reaches the next threshold, which here is 10
      - threshold: 10
        model:
          type: model
          model: namespace:big_custom_diamond
    # A Fallback ItemModel in case none of the entries match
    fallback:
      type: model
      model: namespace:custom_diamond
```

{% hint style="info" %}
You can also chain these to use different ItemModel-types inside each threshold-entry here for very complex items
{% endhint %}
