# ✨ Particle Mechanic

Using the Particle-Mechanic you can make furniture emit particles on a set interval.\
Campfire smoke above a fireplace, embers from a brazier, dripping water from a fountain and so on.

```yaml
campfire_table:
  material: PAPER
  Mechanics:
    furniture:
      lights:
        light: 0,0,0 15
        toggleable: true
      particles:
        - particle: CAMPFIRE_COSY_SMOKE
          offset: 0,1.2,0
          spread: 0.1,0,0.1
          count: 1
          speed: 0.02
          interval: 10
          light_state: true
        - particle: LAVA
          offset: 0,0.8,0
          interval: 2s
          distance: 16
          light_state: true
        - particle: DUST
          offset: 0.3,1,0
          color: 255,120,0
          size: 1.5
          interval: 5
```

A single particle can also be written as a `particle` section instead of the `particles` list.

## Properties

**particle -** The [Particle](https://jd.papermc.io/paper/org/bukkit/Particle.html) to emit. This is the only required property\
**offset -** `x,y,z` offset from the furniture. It follows the rotation of the furniture\
**spread -** `x,y,z` area the particles are randomly spread across. `delta` works as well\
**count -** How many particles to emit each time. Default is 1\
**speed -** Speed of the particles. Default is 0\
**interval -** How often the particles are emitted. A plain number is read as ticks, and it also accepts duration-formats like `5t`, `2s` or `1m`. Default is 20\
**distance -** How far away, in blocks, players can see the particles. Default is 32\
**force -** Shows the particles to players further away than their particle-setting normally allows. Default is false\
**states -** Only emit while the furniture is in one of these [states](furniture-states.md). Takes a single state or a list\
**light\_state -** Only emit while the furniture [light](light-mechanic.md) is on (`true`) or off (`false`). Leave it out to always emit.

## Particle Data

Some particles need extra data. Nexo reads it from the following properties, depending on the particle

| Particle                               | Properties                                        |
| -------------------------------------- | ------------------------------------------------- |
| `DUST`                                 | `color`, `size`                                   |
| `DUST_COLOR_TRANSITION`                | `color` (or `from_color`), `to_color`, `size`     |
| Colored particles, like `ENTITY_EFFECT` | `color`                                         |
| Block particles, like `BLOCK`          | `block`, a material or blockdata string           |
| `ITEM`                                 | `item`, a NexoItem id or a vanilla material       |
| `SCULK_CHARGE`                         | `roll`                                            |
| `SHRIEK`                               | `delay`                                           |
| Other float particles                  | `power`                                           |

Colors can be written as `255,120,0` or `#FF7800`.\
Particles that need data Nexo has no config for, like vibrations or trails, are not supported and will log an error.

## Particles in States

A state of type `FURNITURE` can define its own `particles`, which replace the base ones while the furniture is in that state.

```yaml
      states:
        lit:
          type: FURNITURE
          particles:
            - particle: FLAME
              offset: 0,1,0
              interval: 5
```

{% hint style="warning" %}
The client collides particles with barriers, so a particle starting inside the furniture's own barrier-hitbox will not move.\
Nexo warns about this on load. Raise the `offset` so the particle starts clear of the hitbox.
{% endhint %}
