# 💡 Light Mechanic

Using the Light-Mechanic you can configure your furniture to emits light.\
It takes an **offset** from the base-furniture and a **light-level** between 0 & 15\
Light can also be made toggleable by adding `toggleable: true`, meaning right-clicking the furniture will toggle the light on/off.\
Using `toggled_model` you can provide a NexoItem to display when the furniture-light is toggled on\
Likewise, `toggled_item_model` lets you provide an ItemModel directly without a NexoItem to display when toggled on. Note; this is for 1.21.2+ servers only

```yaml
myitem:
  Mechanics:
    furniture:
      lights:
        #toggleable: false                    # Default is false
        #on_sneak: false                      # Default is false
        #toggled_model: some_nexo_item        # The NexoItem to show when light is on
        #toggled_item_model: namespace:model  # The ItemModel to use when light is on
        #toggled_custom_model_data: lamp_on   # CustomModelData to add when light is on
        light: 0,0,0 15    # x,y,z lightLevel
        #lights:
        #  - 0,0,0 15
        #  - 0,1,0 14
```

## Light Positions

Each entry is written as `x,y,z lightLevel`, where the offset follows the rotation of the furniture.\
Leaving out the level defaults it to 15.\
An axis can also be a range, like `0..2,0,0 14`, to fill a row of lights at once.\
A plain level, like `- 12`, places that level at the furniture itself, and `origin` places level 15 there.

```yaml
myitem:
  Mechanics:
    furniture:
      lights:
        lights:
          - 12             # Level 12 at 0,0,0
          - 0..2,1,0 14    # Level 14 at 0,1,0, 1,1,0 & 2,1,0
```

{% hint style="warning" %}
A single light that is only a number, like `light: 15`, is ignored.\
Write it as a list entry or quote it, like `light: "15"`
{% endhint %}

## Toggling

With `toggleable: true` the furniture starts lit, and right-clicking it turns the light off and on again.

`on_sneak` decides which click toggles the light.\
By default only a click without sneaking toggles it, and with `on_sneak: true` only a sneaking click does.\
Combined with the `on_sneak` of [Furniture States](furniture-states.md#on-sneak), a lamp can toggle its light on a normal click and cycle its states on a sneaking click.

```yaml
      lights:
        light: 0,1,0 15
        toggleable: true
        on_sneak: true
```

### Toggled CustomModelData

`toggled_custom_model_data` adds a CustomModelData value to the furniture while the light is on.\
It is added after any existing value, so it also works together with a `CUSTOM_MODEL_DATA` [state](furniture-states.md#custom_model_data).\
The type of the value is detected automatically, meaning it can be a string, number, true/false or a color.

```yaml
      lights:
        light: 0,1,0 15
        toggleable: true
        toggled_custom_model_data: lamp_on
```

## Light Data Injection

By default Nexo shows furniture light with client-side light blocks, which cannot be placed where a [Barrier Hitbox](hitbox/barrier-hitbox.md) is.\
Nexo will skip any light that overlaps a barrier and log an error for it.

`Experimental.light_data_injection` in `settings.yml` instead writes the light into the chunk light data sent to players.\
This lets lights sit inside barrier hitboxes, see [Plugin Settings](../../configuration/plugin-settings.md#light-data-injection) for its limitations.

<div><figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Table Lamp included in Nexo Default Items (off)</p></figcaption></figure> <figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Table Lamp included in Nexo Default Items (on)</p></figcaption></figure></div>
