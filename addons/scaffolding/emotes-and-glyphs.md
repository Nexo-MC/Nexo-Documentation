# 🙂 Emotes & Glyphs

Nexo glyphs and emotes convert automatically, so they show up in chat, names and menus for Bedrock players just like on Java. In most cases there is nothing to configure.

The one thing worth knowing is that Bedrock sizes glyphs differently, which can make some icons look blurry. This page explains why and how to fix it.

### Glyphs not working under Geyser-Velocity/Geyser-Standalone

When using Geyser-Velocity or Geyser-Standalone, it is required to have a properly configured [Floodgate](https://geysermc.org/wiki/floodgate/setup?platform=proxy-servers) setup. It is also required on all your backend servers together with the Scaffolding plugin,

### Why some glyphs look blurry

On Java, the size a glyph shows at and the size of its image file are two separate things.\
You can take a large, detailed image and tell Java to display it small, and it stays sharp.

Bedrock cannot separate the two. It shows a glyph at whatever size its image is displayed, and that display size is also what decides how sharp it looks:

* Bigger means larger and sharper.
* Smaller means smaller and blockier.

So on Bedrock a detailed image that is meant to show as a small icon can end up looking blurry, because shrinking it also softens it. When that happens, you adjust the glyph's display size in `glyphs.yml`.

### Tweaking individual glyphs & fonts

`plugins/Scaffolding/glyphs.yml` lets you set the display size of a glyph, either for a single glyph or for a whole font. The file is created for you with commented examples on first run, and most servers never need to touch it.

You set the size using whichever of these is easiest:

<table><thead><tr><th width="139.3333740234375">Option</th><th>What it does</th></tr></thead><tbody><tr><td><strong>scale</strong></td><td>Resize the glyph by a factor. <code>2.0</code> makes it twice as big (larger and sharper), <code>0.5</code> makes it half.</td></tr><tr><td><strong>height</strong></td><td>Set an exact display height in pixels. This overrides <code>scale</code>.</td></tr><tr><td><strong>supersample</strong></td><td>Use the glyph's full-resolution image instead of its small Java size. This is the sharpest option, but it also makes the glyph render larger. Good for big logos or menu icons.</td></tr></tbody></table>

There are two sections in the file: `fonts:` (keyed by font name) and `glyphs:` (keyed by glyph id). A setting under `glyphs:` takes priority over a setting under `fonts:` for the same glyph.

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

* **An icon looks blurry:** it is rendering too small for its detail. Raise `scale`, set a larger `height`, or turn on `supersample`.
* **An icon is too big:** lower `scale` or set a smaller `height`. Keep in mind it will also get a little softer as it shrinks.
* **A whole emote font is off:** set a single `scale` under `fonts:` for that font instead of editing each glyph.

{% hint style="success" %}
Saving `glyphs.yml` reconverts on its own, so your changes apply on the next pack build without any extra command.
{% endhint %}
