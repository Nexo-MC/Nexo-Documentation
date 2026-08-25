# 🫥 Furniture Culling

Nexo can hide furniture that a player cannot actually see.\
When a furniture-entity is fully behind solid blocks, Nexo sends that player a metadata-packet setting the entities view-range to 0, making the client stop rendering it.\
Once it comes back into view, the original view-range is sent back.

This is entirely client-side and per-player. The entity is never removed or respawned, so hitboxes, seats, storage and everything else keeps working exactly as before, even while the furniture is hidden.

{% hint style="info" %}
This is Nexo's own occlusion-culling, which is separate from the vanilla display-entity culling described in [#client-side-culling](furniture-culling.md#client-side-culling "mention").\
Both can be used together.
{% endhint %}

## Global settings

Culling is configured in `mechanics.yml` under `furniture.culling`

```yaml
furniture:
  culling:
    enabled: true
    interval: 1t
    force_culling: true
    distance: 0..64
    padding_width: 0.0
    padding_height: 0.0
    ignore_width: 0.0
    ignore_height: 0.0
```

**enabled -** Whether the culling-task runs at all. If false, no furniture is ever culled by Nexo.

**interval -** How often the culling-task runs. Accepts duration-formats like `1t`, `5s` or `1m`.\
An interval below 1 tick disables the task entirely.

**force\_culling -** The fallback used for any furniture that does not set `cullable` itself. See [#per-furniture-properties](furniture-culling.md#per-furniture-properties "mention").

**distance -** Range, in blocks, where culling applies. Furniture closer than the lower bound or further than the upper bound is always shown.\
The upper bound mostly exists to avoid raytracing furniture the client barely renders anyway.

**padding\_width / padding\_height -** Added to the calculated width and height of the furniture before the occlusion-check.\
Increasing these makes culling more conservative, as a bigger box is harder to fully block, which helps if furniture pops out of view slightly too early.

**ignore\_width / ignore\_height -** Furniture whose calculated width or height is below these values is never culled.\
Useful for skipping tiny decorations where the culling-check costs more than the render it saves.

## Per-Furniture Properties

The properties that alter culling behaviour are set in the furnitures `properties`-section, or globally in `mechanics.yml` under `furniture.default_properties`.\
As with all [furniture-properties](./#furniture-properties), the `default_properties` are applied first and the furnitures own `properties` take priority.

```yaml
myitem:
  Mechanics:
    furniture:
      properties:
        cullable: NOT_SET
        display_width: 0
        display_height: 0
```

### cullable

Decides whether this specific furniture is allowed to be culled. It has three states

`TRUE` - This furniture is always culled, even if `force_culling` is false\
`FALSE` - This furniture is never culled, even if `force_culling` is true\
`NOT_SET` - Falls back to the `force_culling` setting in `mechanics.yml`

You can also write it as a plain boolean, where `true` and `false` map to the states above.

Set it to `FALSE` for furniture where a mis-cull would be very noticeable, like huge builds that stick through walls, and `TRUE` for dense decoration you always want culled regardless of the global default.

### display\_width & display\_height

These define the size of the box Nexo checks occlusion against.\
If either is 0, or left unspecified, Nexo calculates that dimension from the furnitures [hitbox](hitbox/) instead, combining all interaction-, shulker-, ghast- and barrier-hitboxes into one box rotated to match the furnitures current yaw.

Since these are the same properties the client uses for its own culling, setting them will affect both. In most cases you can leave them at 0 and let the hitbox decide.

{% hint style="warning" %}
Furniture with no hitbox-dimensions and no `display_width`/`display_height` cannot be culled, as there is nothing to check occlusion against.
{% endhint %}

### view\_range

Not a culling-property as such, but the value Nexo restores when a furniture becomes visible again.\
If unspecified it defaults to `1.0`.

## How the check works

Every `interval`, for each player and each furniture they currently track, Nexo runs through the following, stopping at the first step that shows the furniture

1. Furniture that is invalid or in another world is skipped entirely
2. `cullable` is resolved against `force_culling`. Not cullable means shown
3. The width and height are resolved from `display_width`/`display_height`, or the hitbox, then `padding_width`/`padding_height` is added. This result is cached per furniture and only recalculated when it rotates
4. If both dimensions end up as 0, it is shown
5. If the width or height is below `ignore_width`/`ignore_height`, it is shown
6. If the distance from the players eye is outside `distance`, it is shown
7. The previous verdict is reused unless the player-eye or the furniture moved more than ~0.35 blocks, or the verdict is older than a second
8. Otherwise 7 rays are cast from the players eye towards the furniture-box, one at the center, four at the mid-height corners, one at the top and one at the bottom. The furniture is only hidden if **all** of them are blocked

Rays pass through non-occluding blocks like glass, leaves and barriers, up to 5 times per ray, so furniture behind a window will not be culled.

{% hint style="info" %}
The filtering runs off the main-thread and only the few furniture whose view actually changed get raytraced on the owning region-thread, so a still player standing in a room full of furniture costs close to nothing.
{% endhint %}

## Client-Side Culling

Display-entities also have properties that the client itself uses to decide whether to render them.\
By default Nexo only relies on distance-based culling here, not whether the entity is on-screen. If you place a lot of furniture in a small area, tweaking these can help.

`display_width` - Width of the entity, outside which the client culls it. Default is 0\
`display_height` - Height of the entity, outside which the client culls it. Default is 0\
`view_range` - Maximum view-range of the entity. When the distance is more than _`view_range`_ `×` [_`entityDistanceScaling`_](https://minecraft.wiki/w/Options.txt#Java_Edition) `× 64`, the entity is not rendered. Defaults to 1.0

Setting `display_width` and `display_height` to 0 disables the clients own culling for that furniture, which is why furniture will never disappear when you look away from it by default.
