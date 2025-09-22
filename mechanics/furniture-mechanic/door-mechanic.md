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
---

# 🚪 Door Mechanic

Nexo lets you make a furniture that will act as a door.\
You can also specify a few extra options for additional behaviour:

**toggle\_hitbox\_on\_open** - Changes the hitbox from barriers to interactions when opened\
**open\_sound -** The sound to play when opening the door\
**close\_sound -** The sound to play when closing the door\
**open\_properties - T**he same as [Furniture Properties](./#furniture-properties), but only applied in open-state\
**is\_sliding -** If the door is sliding type or normal type\
**automatic\_close\_delay -** A duration of time before the door will close when opened (1t, 2s, 3m, etc...)\
**delay\_hitbox\_toggle -** If the swap to non-solid hitbox should be delayed until door is fully opened

There is also a new **delay-property** which defines the "time to open" for the door.\
If left unspecified, the door immediatly changes state

There is also two types of doors, normal and sliding. A sliding door opens by applying the open\_properties transformations, whilst a normal door applies a rotation

**Config Examples:**

{% columns fullWidth="true" %}
{% column width="50%" %}
{% code fullWidth="false" %}
```yaml
large_wooden_door:
  itemname: Large Wooden Door
  Pack:
    model: nexo:item/nexo_furniture/large_wooden_door
  Mechanics:
    furniture:
      limited_placing:
        floor: true
      hitbox:
        barriers: 0..1,0..2,0
      block_sounds:
        place_sound: block.wood.place
        break_sound: block.wood.break
      properties:
        translation: 0,1,0
        delay: 4
      door:
        open_sound: block.wooden_door.open
        close_sound: block.wooden_door.close
        toggle_hitbox_on_open: true
        open_properties:
          translation: -0.85,1,0
```
{% endcode %}
{% endcolumn %}

{% column width="50%" %}
{% code fullWidth="true" %}
```yaml
large_wooden_sliding_door:
  itemname: Large Wooden Sliding Door
  Pack:
    model: nexo:item/nexo_furniture/large_wooden_door
  Mechanics:
    furniture:
      limited_placing:
        floor: true
      hitbox:
        barriers: 0..1,0..2,0
      block_sounds:
        place_sound: block.wood.place
        break_sound: block.wood.break
      properties:
        translation: 0,1,0
        delay: 4
      door:
        is_sliding: true
        open_sound: block.wooden_door.open
        close_sound: block.wooden_door.close
        toggle_hitbox_on_open: true
        open_properties:
          translation: -1.5,1,0
```
{% endcode %}
{% endcolumn %}
{% endcolumns %}

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTAoAxayP9PrBtX9UQ5wa%2Fuploads%2Fs8AfcHvnoLucixCBnQlR%2F2025-08-19%2015-57-54.mp4?alt=media&token=cc47ff3d-876b-46a0-8c02-ec72d214423f" %}
