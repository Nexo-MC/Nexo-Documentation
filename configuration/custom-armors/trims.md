# Trims Based (1.20+)

TRIMS is a legacy method for servers on **1.20-1.21.1**, where the COMPONENT method isn't available yet. With TRIMS, Nexo handles most of the work for you, but there are two important constraints:

* Every piece must use a **`CHAINMAIL_*`** base item (`CHAINMAIL_HELMET`, `CHAINMAIL_CHESTPLATE`, etc.).
* Nexo generates a **datapack** from your configured armor sets, so the server needs a full restart whenever you add or remove a set.

Make sure `armor_type` is set to `TRIMS` in `Nexo/settings.yml` (see the [overview](README.md#choosing-the-method)).

{% hint style="danger" %}
**First-time setup / after switching to `TRIMS`** - because the datapack only loads on startup, you need three steps:

1. **Start** your server so the datapack is generated.
2. **Stop** your server.
3. **Start** it again so the freshly generated datapack is loaded.

Skipping the second start is the most common reason trims armor "doesn't work" right after switching.
{% endhint %}

## Naming convention (read this first)

As with the COMPONENT method, Nexo links your items and textures together **by name**. Pick one `armorname` (e.g. `ruby`) and reuse it everywhere.

For an armor set named **`ruby`**:

| Piece      | Item ID (config key) | Base material          |
| ---------- | -------------------- | ---------------------- |
| Helmet     | `ruby_helmet`        | `CHAINMAIL_HELMET`     |
| Chestplate | `ruby_chestplate`    | `CHAINMAIL_CHESTPLATE` |
| Leggings   | `ruby_leggings`      | `CHAINMAIL_LEGGINGS`   |
| Boots      | `ruby_boots`         | `CHAINMAIL_BOOTS`      |

You only need **two** texture files for the whole set - the worn-armor layers:

| File                        | Covers                       |
| --------------------------- | ---------------------------- |
| `ruby_armor_layer_1.png`    | Helmet, chestplate and boots |
| `ruby_armor_layer_2.png`    | Leggings                     |

{% hint style="warning" %}
The split is fixed by Minecraft: `layer_1` draws the helmet, chestplate and boots, while `layer_2` draws the leggings.
{% endhint %}

{% hint style="info" %}
If you are unsure how to reference a texture file in a NexoItem config, see [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention").
{% endhint %}

## Configuring an armor piece

```yaml
ruby_helmet:
  displayname: "<gradient:#FA7CBB:#F14658>Ruby Helmet"
  material: CHAINMAIL_HELMET
  Pack:
    parent_model: "item/generated"
    # Pack.texture is the icon shown in the inventory / when held.
    texture: default/armors/ruby_helmet
    # Optional: only needed if your layer files do NOT follow the
    # `armorname_armor_layer_X.png` naming. If omitted, Nexo searches
    # for ruby_armor_layer_1.png and ruby_armor_layer_2.png itself.
    #CustomArmor:
    #  layer1: default/armors/ruby_armor_layer_1.png
    #  layer2: default/armors/ruby_armor_layer_2.png
```

Repeat this for `ruby_chestplate`, `ruby_leggings` and `ruby_boots` with their matching `CHAINMAIL_*` material.

## The trim pattern

For the worn armor to render, each piece needs a `trim_pattern`. **Nexo assigns this automatically** based on the item ID, so you usually don't need to set it.

The trim pattern always follows the pattern `nexo:armorname`. To set it manually:

```yaml
ruby_helmet:
  trim_pattern: nexo:ruby
```
