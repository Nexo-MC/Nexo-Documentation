# Component Based (1.21.2+)

COMPONENT is the recommended way to add custom armor on 1.21.2+ servers. It has **none** of the restrictions older methods had:

* The base item can be **any material** - `PAPER`, an armor item, anything.
* No datapack and no server restarts are required.
* It does not conflict with shaders or require extra client mods.

Before you start, make sure `armor_type` is set to `COMPONENT` in `Nexo/settings.yml` (see the [overview](README.md#choosing-the-method)).

## Naming convention (read this first)

This is where most setups go wrong. Nexo links your items and textures together **by name**, so the names have to follow an exact pattern. Pick one `armorname` (e.g. `forest`) and reuse it everywhere.

For an armor set named **`forest`**:

| Piece      | Item ID (config key) |
| ---------- | -------------------- |
| Helmet     | `forest_helmet`      |
| Chestplate | `forest_chestplate`  |
| Leggings   | `forest_leggings`    |
| Boots      | `forest_boots`       |

You only need **two** texture files for the whole set - the worn-armor layers:

| File                          | Covers                        |
| ----------------------------- | ----------------------------- |
| `forest_armor_layer_1.png`    | Helmet, chestplate and boots  |
| `forest_armor_layer_2.png`    | Leggings                      |

{% hint style="warning" %}
The two layer files are **not** optional and the split is fixed by Minecraft: `layer_1` draws the helmet, chestplate and boots, while `layer_2` draws the leggings. If your leggings look wrong, you've almost certainly put the leg texture in `layer_1`.
{% endhint %}

{% hint style="info" %}
If you are unsure how to reference a texture file in a NexoItem config, see [#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention").
{% endhint %}

## Configuring an armor piece

Each piece is a normal NexoItem. The only armor-specific part is the worn texture, which Nexo finds automatically as long as your files follow the naming convention above.

```yaml
forest_helmet:
  displayname: "<gradient:#3FA34D:#1E6E2D>Forest Helmet"
  material: PAPER    # Can be any material - armor item or otherwise
  Pack:
    # Pack.texture is the icon shown in the inventory / when held.
    texture: nexo:item/nexo_armors/forest_helmet
    # Optional: only needed if your layer files do NOT follow the
    # `armorname_armor_layer_X.png` naming. If omitted, Nexo searches
    # for forest_armor_layer_1.png and forest_armor_layer_2.png itself.
    #CustomArmor:
    #  layer1: nexo:item/nexo_armors/forest_armor_layer_1
    #  layer2: nexo:item/nexo_armors/forest_armor_layer_2
```

Repeat this for `forest_chestplate`, `forest_leggings` and `forest_boots`, changing the `material`/`displayname` as needed. They all share the same two layer files.

## The Equippable component

For the worn armor to render, the item needs an `equippable` component pointing at the set's asset. **Nexo assigns this automatically** based on the item ID, so in most cases you don't need to write it yourself.

The asset id always follows the pattern `nexo:armorname`. If you want to set it manually - for example to control the equip `slot` explicitly - it looks like this:

```yaml
forest_helmet:
  Components:
    equippable:
      slot: HEAD
      asset_id: nexo:forest
```

{% hint style="warning" %}
If your helmet uses a **3D model** (a custom model rather than a flat texture), do **not** set `Components.equippable.asset_id`. The asset id forces the flat armor-layer rendering and would hide your 3D model.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>The Forest armor sets Nexo ships with (Player, Wolf, Horse &#x26; Llama)</p></figcaption></figure>
