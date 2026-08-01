# 🧭 Furniture Placements

Nexo lets a single furniture-item behave differently depending on what surface it is placed on.\
A lantern that stands on the ground, hangs from the ceiling and sticks out of a wall, all from one NexoItem.

This is done with the `placements`-section, which has three optional subsections:\
**floor -** Used when placed on top of a block\
**wall -** Used when placed on the side of a block\
**roof -** Used when placed on the underside of a block

Each of these is a furniture-mechanic of its own, merged on top of the parent furniture.\
Anything you can put in the `furniture`-section can be put in a placement, and it will override the parent value.\
Properties you do not specify are simply inherited from the parent furniture.

```yaml
lantern:
  itemname: "<gray>Lantern"
  material: PAPER
  Pack:
    model: default/lantern
  Mechanics:
    furniture:
      block_sounds:
        place_sound: block.lantern.place
        break_sound: block.lantern.break
      hitbox:
        interaction: 0,0,0 0.5,0.5
      placements:
        floor:
          item_model: nexo:furniture/lantern_floor
        wall:
          item_model: nexo:furniture/lantern_wall
          properties:
            translation: 0,0.3,-0.3
        roof:
          item_model: nexo:furniture/lantern_hanging
          properties:
            translation: 0,-0.4,0
```

The chosen placement is stored on the furniture when placed, so breaking, interacting and drops all use the same variant it was placed as.

{% hint style="info" %}
If you only define some of the placements, the ones you leave out fall back to the parent furniture.\
A placement cannot define its own `placements`-section, as that would recurse infinitely.
{% endhint %}

## Placements vs Limited Placing

The two work together and do different things.\
[Limited placing](./#limited-placing) decides **if** a furniture may be placed on a surface.\
Placements decide **what** the furniture looks and acts like once placed there.

Meaning, if you want a furniture that only exists as a wall- and roof-variant, combine the two:

```yaml
lantern:
  Mechanics:
    furniture:
      limited_placing:
        floor: false
        wall: true
        roof: true
      placements:
        wall:
          item_model: nexo:furniture/lantern_wall
        roof:
          item_model: nexo:furniture/lantern_hanging
```
