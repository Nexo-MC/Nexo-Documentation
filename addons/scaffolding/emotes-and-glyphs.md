# 🙂 Emotes & Glyphs

Nexo glyphs and emotes convert automatically, so Bedrock players see them in chat, names and menus just like Java players do. Most of the time there is nothing to set up.

The one thing to know is that Bedrock sizes glyphs differently, which can make some icons look blurry. This page explains why, and how to fix it.

### Glyphs not working under Geyser-Velocity/Geyser-Standalone

If you use Geyser-Velocity or Geyser-Standalone, you need a properly configured [Floodgate](https://geysermc.org/wiki/floodgate/setup?platform=proxy-servers) setup. Floodgate must also be installed on all your backend servers, together with the Scaffolding plugin.

### Why some glyphs look blurry

On Java, the size a glyph shows at and the size of its image are two separate things.\
You can take a large, detailed image and tell Java to show it small, and it stays sharp.

Bedrock cannot keep these apart. The size a glyph is shown at also decides how sharp it looks:

* Bigger means larger and sharper.
* Smaller means smaller and blockier.

So on Bedrock, a detailed image meant to show as a small icon can look blurry, because shrinking it also makes it softer. When that happens, change the glyph's display size in `glyphs.yml`.

### Tweaking individual glyphs & fonts

In `plugins/Scaffolding/glyphs.yml` you can set the display size of a single glyph or of a whole font. The file is created with commented examples on first run, and most servers never need to touch it.

Set the size with whichever of these is easiest for you:

<table><thead><tr><th width="139.3333740234375">Option</th><th>What it does</th></tr></thead><tbody><tr><td><strong>scale</strong></td><td>Resizes the glyph by a factor. <code>2.0</code> makes it twice as big (larger and sharper), <code>0.5</code> makes it half as big.</td></tr><tr><td><strong>height</strong></td><td>Sets an exact display height in pixels. This overrides <code>scale</code>.</td></tr><tr><td><strong>supersample</strong></td><td>Uses the glyph's full-resolution image instead of its small Java size. This is the sharpest option, but the glyph also shows larger. Good for big logos or menu icons.</td></tr></tbody></table>

The file has two sections: `fonts:` (keyed by font name) and `glyphs:` (keyed by glyph id). If both set something for the same glyph, the setting under `glyphs:` wins.

{% code title="plugins/Scaffolding/glyphs.yml" %}
```yaml
fonts:
  emojis:discord_emojis:
    scale: 1.0
glyphs:
  pink_heart:
    height: 16
  some_big_logo:
    supersample: true
```
{% endcode %}

#### Which option to pick

* **An icon looks blurry:** it is shown too small for its detail. Raise `scale`, set a larger `height`, or turn on `supersample`.
* **An icon is too big:** lower `scale` or set a smaller `height`. It will also get a little softer as it shrinks.
* **A whole emote font looks wrong:** set one `scale` under `fonts:` for that font instead of changing each glyph.

{% hint style="success" %}
After editing `glyphs.yml`, run `/scf reload -f` and have your Bedrock players rejoin.
{% endhint %}
