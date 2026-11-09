# 💡 Custom Block Light

Any type of custom block can emit light, like a lamp or a glowing ore.\
A custom block takes a single **light-level** between 0 & 15, which it shows on the open sides around it.

```yaml
my_lamp:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      light: 15
```

The longer form takes the same level in a `light` section, which also lets you make it toggleable.

```yaml
my_lamp:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      light:
        level: 15
        toggleable: true    # Default is false
```

{% hint style="info" %}
The light is shown on the sides of the block that are air or water, and not inside a furniture hitbox.\
A block surrounded by other blocks on all sides therefore gives off no light
{% endhint %}

{% hint style="warning" %}
`lights` with an `s` is the [furniture light](../furniture-mechanic/light-mechanic.md) format.\
Custom blocks only read `light`, and Nexo will warn you if it finds `lights` on a custom block
{% endhint %}

## Toggling

With `toggleable: true` the block starts lit, and right-clicking it with the main hand without sneaking turns the light off and on again.\
Like other interactable blocks, players need to sneak to place blocks against it.\
Whether the light is on is saved on the placed block, so it stays the same through restarts.

### Toggled Block

`toggled_block` swaps the block to another look while its light is off.\
It can name another custom block, which must be the same `type` as the lamp itself.

```yaml
my_lamp:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      light:
        level: 15
        toggleable: true
        toggled_block: my_lamp_off
```

It can also be a section, which defines the toggled block inline without needing an item of its own.\
This registers a block called `<itemid>_toggled`, `my_lamp_toggled` in the example below.\
It copies `breakable`, `hardness`, `block_sounds`, `blast_resistant`, `blast_resistance`, `immovable`, `storage`, `clickActions` & `blocklocker` from the lamp, and anything set in the section overrides those.

```yaml
my_lamp:
  Mechanics:
    custom_block:
      type: NOTEBLOCK
      model: my_lamp
      light:
        level: 15
        toggleable: true
        toggled_block:
          model: my_lamp_off
          #custom_variation: 40    # Assigned and saved automatically if unspecified
```

A player breaking the lamp while its light is off still gets the lamp's own drops.\
In explosions it uses the drops of the toggled block instead, and an inline `toggled_block` does not copy the lamp's `drop`.

{% hint style="warning" %}
`toggled_block` is ignored on [Directional Blocks](noteblock-mechanic/directional-mechanic.md), as swapping the block would lose which way it was placed.\
The light itself still toggles.\
A `light` inside the inline `toggled_block` is also ignored, the lamp's own light stays in charge
{% endhint %}

## Light Data Injection

By default Nexo shows the light with client-side light blocks next to the custom block.\
`Experimental.light_data_injection` in `settings.yml` instead writes the light into the chunk light data, with the block itself as the light source.\
See [Plugin Settings](../../configuration/plugin-settings.md#light-data-injection) for its limitations.
