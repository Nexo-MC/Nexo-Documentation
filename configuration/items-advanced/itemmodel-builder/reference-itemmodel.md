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

# Reference ItemModel

A **Reference,** _or Model,_ **ItemModel** is the simplest form of ItemModel.\
All it does is reference the path to a Model[^1] file to use.

If we want to use this in an example here;

{% code title="NexoItem Example with pre-made Model file" %}
```yaml
myitem:
  ItemModel:
    type: model
    model: namespace:mymodel #References assest/namespace/models/mymodel.json
```
{% endcode %}

{% code title="NexoItem Example for a 2D NexoItem with just a Texture provided" %}
```yaml
myitem:
  Pack:
    texture: namespace:mytexture #References assest/namespace/textures/mytexture.png
  ItemModel:
    type: model
    model: myitem # When only a texture is provided, Nexo generates the Model for <itemid>
```
{% endcode %}

{% hint style="warning" %}
Should be noted that this example is not needed if you just want a basic Item like shown above.\
When using `prefer_item_models` ( [itemmodels-vs.-custommodeldata.md](../../../general-usage/faq/itemmodels-vs.-custommodeldata.md "mention") ), this is done automatically.\
If normally relying on CustomModelData, you can also just set the ItemModel-Component<br>

```
myitem:
  Pack:
    texture: namespace:mytexture
  Components:
    item_model: namespace:myitem
```
{% endhint %}

[^1]: Models are what control the visual aspects of Items & Blocks. These files are found in `assets/<namespace>/models/...`
