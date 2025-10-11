---
icon: window-frame
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
---

# ChorusBlock Mechanic

{% hint style="info" %}
CHORUSBLOCK-type allows for up-to **63** custom blocks.\
One per `custom_variation`
{% endhint %}

### Creating your first block

#### Parent-Model

The Nexo-item root configuration is the same as for any item (you can use any material like a diamond for example) and set an itemname, etc.\
It is recommended to not use a block for your material, sticking to such materials as PAPER\
For the pack section you can use your own model or texture for your block.\
If all you have is a texture, you can specify a parent\_model and Nexo will generate the needed files for you. A Normal 1x1x1 block uses "block/cube\_all"

```yaml
my_block:
  itemname: "My block"
  material: PAPER
  Pack:
    parent_model: "block/cube_all"
    texture: my_block_texture.png
```

### CustomBlock Mechanic configuration

To use this mechanic you need to tell to Nexo which model to use (to use the generated one, just put the name id of your item).\
You then need to use custom\_variation which is not already used by another block.\
Valid custom\_variation is 1..63

```yaml
my_block:
  Mechanics:
    custom_block:
      type: CHORUSBLOCK
      custom_variation: 2
      model: my_block
      drop:
        silktouch: false
        minimal_type: STONE
        loots:
          - nexo_item: my_block
            probability: 1.0
```
