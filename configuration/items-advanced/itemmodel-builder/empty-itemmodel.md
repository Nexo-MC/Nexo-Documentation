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

# Empty ItemModel

An **Empty ItemModel** just renders nothing.

Main use for this type is for conditional checks in other types, to render something or nothing.\
Below is an example which renders nothing in the GUI until you start using the item, but renders it normal in every other context

```yaml
custom_sword:
  ItemModel:
    type: select
    property: display_context
    cases:
      - when: "gui"
        model:
          type: condition
          property: using_item
          on_true:
            type: model
            model: namespace:custom_sword
          on_false:
            type: empty
    # A Fallback ItemModel so we dont need to define all the other display-contexts manually
    fallback:
      type: model
      model: namespace:custom_sword
```

{% hint style="info" %}
You can also chain these to use different ItemModel-types inside each threshold-entry here for very complex items
{% endhint %}
