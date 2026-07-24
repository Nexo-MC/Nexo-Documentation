# 🖥️ Custom GUIs & HUDs

On Java, custom GUIs comes down to two things, and Scaffolding reproduces both on Bedrock:

1. **Custom GUIs** are a glyph (a unicode character defined in a font file) placed in the **title** of a custom inventory.
2. **HUD overrides** are replaced vanilla HUD textures, such as the hearts, hotbar or armor bar.

Scaffolding reads these straight from the pack's fonts and textures, so it is not tied to any one plugin's glyph setup. Conversion is automatic in the common case.

{% hint style="warning" %}
**Alignment is approximate**

Bedrock and Java lay their screens out differently, and Bedrock gives far less control over placement. The automatic conversion gets most screens close, but it is **not guaranteed pixel-perfect**, and some GUIs can show **larger inconsistencies**. Simple, chest-based screens convert best; dense or heavily custom layouts are the most likely to need a manual nudge.
{% endhint %}

### Custom GUI backgrounds

A custom inventory background on Java is a tall glyph placed in the container's title. Bedrock has no title glyph, so Scaffolding takes that glyph's texture and draws it onto the Bedrock screen instead, shown only while that container is open.

This is **automatic** for any glyph tall enough to be a background:

* The texture is placed on the matching Bedrock screen, sized and positioned to line up with the slot grid.
* It shows only while that container is open, matched by the container title.
* `guiAutoBackgrounds` in `config.yml` toggles the whole feature (on by default).

### Sizing a glyph

Bedrock renders a glyph at its baked pixel size, so size and sharpness move together — a bigger bake is larger _and_ sharper, a smaller bake is smaller _and_ blockier. Override that bake per font or per glyph in `plugins/Scaffolding/glyphs.yml`. Most setups never touch this file.

Two sections, both keyed by id: `fonts:` (by font key) and `glyphs:` (by glyph id). A `glyphs:` entry wins over a `fonts:` entry for the same glyph. Every field is optional.

<table><thead><tr><th width="136.99993896484375">Field</th><th>Purpose</th></tr></thead><tbody><tr><td><code>scale</code></td><td>Multiply the glyph's Java height. <code>2.0</code> = twice as tall, and sharper.</td></tr><tr><td><code>height</code></td><td>Pin an explicit baked height in px. Overrides <code>scale</code>.</td></tr><tr><td><code>supersample</code></td><td>Bake from the full-resolution source texture instead of the Java height. Sharpest, but renders larger — good for big or UI glyphs.</td></tr></tbody></table>

#### Vanilla GUI overrides

If your pack reskins a **vanilla container screen** (by replacing its texture), Scaffolding reproduces that on the matching Bedrock screen too. This is controlled by `convertVanillaOverrides` in `config.yml` (on by default; turn it off if you do not reskin vanilla content and want a smaller pack).

**Supported screens, if present in your pack:**

* Chest, double-chest and ender chest
* Shulker box
* Furnace, blast furnace and smoker
* Crafting table
* Player inventory
* Enchanting table
* Anvil
* Brewing stand
* Villager trading

{% hint style="danger" %}
**Hopper, dropper and dispenser are not supported**

These Bedrock screens are hard-coded and cannot be customized via a resourcepack at the moment, so they cannot be altered. They are noted in the conversion log and left as vanilla for Bedrock players.
{% endhint %}

### Vanilla HUD overrides

Retextures of the vanilla HUD are converted to their Bedrock equivalents. Bedrock scales each texture to fit its on-screen element, so the source resolution does not matter.

**Converted HUD elements include:**

* Hotbar and the selected-slot box
* Hearts (health, absorption, frozen, vehicle/mount)
* Hunger, Armor, air & experience bars
* Mob-effect status backgrounds
* Locator bar

A few Java-only HUD states have **no Bedrock counterpart** and are left out (and noted in the log): poisoned/withered/hardcore hearts, the crosshair and attack indicators, the jump/ride bar, per-effect status icons and offhand slots.

{% hint style="warning" %}
**Custom HUD plugins are not supported yet**

This only covers retextures of the **vanilla** HUD.\
Custom HUDs added by plugins such as **MythicHUD** are **not supported at the moment**.
{% endhint %}
