# 🖥️ Custom GUIs & HUDs

On Java, custom GUIs and HUDs come down to two things, and Scaffolding recreates both on Bedrock:

1. **Custom GUIs** are a glyph (a unicode character defined in a font file) placed in the **title** of a custom inventory.
2. **HUD overrides** are replaced vanilla HUD textures, such as the hearts, hotbar or armor bar.

Scaffolding reads these directly from the pack's fonts and textures, so it does not depend on any one plugin's glyph setup. In most cases conversion is automatic.

{% hint style="warning" %}
**Alignment is approximate**

Bedrock and Java lay out their screens differently, and Bedrock gives you much less control over where things go. The automatic conversion gets most screens close, but it is **not guaranteed to be pixel-perfect**, and some GUIs can be **noticeably off**. Simple chest-based screens convert best. Dense or heavily customized layouts are the most likely to need a manual fix.

You can fix anything the automatic placement gets wrong by hand, see [#tweaking-a-gui-manually](custom-guis-and-huds.md#tweaking-a-gui-manually "mention").
{% endhint %}

### Custom GUI backgrounds

On Java, a custom inventory background is a tall glyph placed in the container's title. Bedrock cannot show glyphs in the title this way, so Scaffolding takes that glyph's texture and draws it onto the Bedrock screen instead, only while that container is open.

This happens **automatically** for every glyph Nexo uses as a background in a GUI title:

* The texture is placed on the matching Bedrock screen, sized and positioned to line up with the slot grid.
* It only shows while that container is open, matched by the container title.
* Bedrock cannot shift title text, so any `<shift:N>` in front of the glyph in the Java title is added to the overlay's position instead.
* `autoBackgrounds` in `gui.yml` turns the whole feature on or off (on by default, see below).

Only glyphs that are actually used in a Nexo GUI title become overlays, so a random tall glyph somewhere else in your pack does not turn into a stray background. Anything Nexo does not put in a title, such as a GUI from another plugin, has to be added by hand.

### Tweaking a GUI manually

You can override anything the automatic conversion decides, per GUI, in `plugins/Scaffolding/gui.yml`. Most setups never need this. Use it when a background sits a few pixels off or shows at the wrong size, or when you want a glyph that was not picked up automatically.

If the file does not exist, Scaffolding writes it for you on the first conversion. It starts with:

* your **auto-detected backgrounds**, commented out, ready to uncomment and change
* every other **tall glyph** as a commented candidate you can turn on

Once the file exists, Scaffolding never rewrites it, so your edits are safe. Delete it if you want a fresh copy with new suggestions.

{% hint style="success" %}
**GUI Visualizer**

Instead of guessing numbers, you can work out the alignment visually with the tool at [https://nexomc.com/tools/gui-visualizer](https://nexomc.com/tools/gui-visualizer).
{% endhint %}

{% hint style="info" %}
After editing `gui.yml`, run `/scf reload -f` and have your Bedrock players reconnect. Bedrock only downloads the pack again when it reconnects.
{% endhint %}

#### Settings

There are two top-level keys, and both are optional:

<table><thead><tr><th width="260">Setting</th><th width="120">Default</th><th>Purpose</th></tr></thead><tbody><tr><td><code>autoBackgrounds</code></td><td><code>true</code></td><td>Detect GUI backgrounds from your Nexo inventory titles. <code>false</code> shows only the entries in this file.</td></tr><tr><td><code>minHeight</code></td><td><code>32</code></td><td>Smallest glyph height in pixels to list as a commented example when the file is created. Does not affect conversion.</td></tr></tbody></table>

#### Entries

Each entry uses its glyph id as the key and overrides the automatic overlay for that glyph. Only `glyph` is required. Any field you leave out uses the automatic value.

<table><thead><tr><th width="260">Field</th><th width="120">Default</th><th>Purpose</th></tr></thead><tbody><tr><td><code>glyph</code></td><td>required</td><td>The Nexo glyph to draw. Its texture and unicode come from Nexo, so the id is enough.</td></tr><tr><td><code>match_literal</code></td><td>the glyph</td><td>The Java title with Nexo tags, such as <code>"&#x3C;glyph:my_gui>"</code>. The art only shows while the open container's title contains it.</td></tr><tr><td><code>match_title</code></td><td>-</td><td>Like <code>match_literal</code>, but plain text for titles without Nexo tags.</td></tr><tr><td><code>shift</code></td><td><code>0</code></td><td>Horizontal nudge in pixels, like the <code>&#x3C;shift:N></code> before the glyph on Java. Positive moves right.</td></tr><tr><td><code>size</code></td><td>auto</td><td><code>"W,H"</code>. <code>"162px,54px"</code> is a fixed size in UI pixels, <code>"100,100"</code> or <code>"100%,100%"</code> a percentage of the panel. Pixels line up better with Bedrock's 18px slots.</td></tr><tr><td><code>offset</code></td><td>auto</td><td><code>"x,y"</code> pixel offset from the anchor. Positive x moves right, positive y moves down.</td></tr><tr><td><code>anchor</code></td><td><code>center</code></td><td>Where the image attaches. <code>center</code> for window art, <code>top_left</code> or another JSON-UI anchor for HUD pieces.</td></tr><tr><td><code>layer</code></td><td><code>13</code></td><td>Draw order. <code>13</code> is above slot backgrounds and below item icons.</td></tr><tr><td><code>screen</code></td><td><code>container</code></td><td>Which Bedrock screen the art is added to, see the table below.</td></tr></tbody></table>

{% hint style="warning" %}
An entry with no match, or with a `match_literal` that cannot be resolved (for example a glyph id with a typo), is **always visible** on that screen. Scaffolding logs a warning when this happens.
{% endhint %}

```yaml
autoBackgrounds: true
minHeight: 32

# Nudge an auto-detected background 4px up
my_menu:
  glyph: my_menu
  match_literal: "<glyph:my_menu>"
  screen: container
  offset: "0,-4"

# A glyph that is not in any GUI title, pinned to the furnace screen at a fixed size
forge_overlay:
  glyph: forge_overlay
  match_literal: "<glyph:forge_overlay>"
  screen: furnace
  size: "176px,166px"
```

#### Screens

<table><thead><tr><th width="260"><code>screen</code></th><th>Where it draws</th></tr></thead><tbody><tr><td><code>container</code> / <code>chest</code></td><td>Chest and double chest. This is the default for custom inventories.</td></tr><tr><td><code>shulker_box</code></td><td>Shulker box.</td></tr><tr><td><code>inventory</code></td><td>The whole survival inventory screen.</td></tr><tr><td><code>player_inventory</code></td><td>Only the top half of the inventory window.</td></tr><tr><td><code>crafting_table</code></td><td>Crafting table window.</td></tr><tr><td><code>furnace</code>, <code>blast_furnace</code>, <code>smoker</code></td><td>The 176x166 window of each smelting screen.</td></tr><tr><td><code>enchanting</code></td><td>Enchanting table.</td></tr><tr><td><code>anvil</code></td><td>Anvil.</td></tr><tr><td><code>smithing_table</code></td><td>Smithing table.</td></tr><tr><td><code>grindstone</code></td><td>Grindstone.</td></tr><tr><td><code>brewing_stand</code></td><td>Brewing stand.</td></tr><tr><td><code>villager</code></td><td>The right panel of the trading screen.</td></tr><tr><td><code>hud</code></td><td>The in-game HUD, drawn on top of everything.</td></tr></tbody></table>

#### Commands

<table><thead><tr><th width="260">Command</th><th>What it does</th></tr></thead><tbody><tr><td><code>/scf gui list</code></td><td>Lists the active overlays, auto-detected and from <code>gui.yml</code>, with their screen and title match.</td></tr><tr><td><code>/scf gui import &#x3C;glyph> [screen]</code></td><td>Adds a glyph to the end of <code>gui.yml</code> and reconverts, with size and offset auto-detected.</td></tr></tbody></table>

#### Advanced: injection points

Bedrock sometimes renames its own screens and controls between game versions. If an update breaks a screen, you can point an entry at the new location yourself, without waiting for a Scaffolding update.

<table><thead><tr><th width="200">Field</th><th>Purpose</th></tr></thead><tbody><tr><td><code>ui_file</code></td><td>The Bedrock JSON-UI file to patch, for example <code>ui/chest_screen.json</code>.</td></tr><tr><td><code>namespace</code></td><td>The JSON-UI namespace of that file, for example <code>chest</code>.</td></tr><tr><td><code>root</code></td><td>A single control to add the overlay to.</td></tr><tr><td><code>roots</code></td><td>A list of controls, for screens with more than one panel (small/large chest).</td></tr><tr><td><code>array</code></td><td>The name of the control's child array. This is <code>controls</code> on every vanilla screen.</td></tr><tr><td><code>layer_bias</code></td><td>Layer offset for the root's own depth, so <code>layer</code> means the same everywhere.</td></tr></tbody></table>

{% hint style="info" %}
If `gui.yml` is malformed, the whole file is ignored. If a single entry is wrong, only that entry is skipped. Both cases log a warning in the console, and conversion carries on either way, so a typo can never break your pack.
{% endhint %}

### Sizing a glyph

Bedrock draws a glyph at the pixel size it was baked at, so size and sharpness go together. A bigger bake is larger _and_ sharper, and a smaller bake is smaller _and_ blockier. You can change the bake per font or per glyph in `plugins/Scaffolding/glyphs.yml`. Most setups never touch this file.

The file has two sections, both keyed by id: `fonts:` (by font key) and `glyphs:` (by glyph id). If both have an entry for the same glyph, the `glyphs:` entry wins. Every field is optional.

<table><thead><tr><th width="136.99993896484375">Field</th><th>Purpose</th></tr></thead><tbody><tr><td><code>scale</code></td><td>Multiplies the glyph's Java height. <code>2.0</code> makes it twice as tall, and sharper.</td></tr><tr><td><code>height</code></td><td>Sets an exact baked height in px. Overrides <code>scale</code>.</td></tr><tr><td><code>supersample</code></td><td>Bakes from the full-resolution source texture instead of the Java height. This is the sharpest option, but the glyph also shows larger. Good for big or UI glyphs.</td></tr></tbody></table>

### Vanilla GUI overrides

If your pack reskins a **vanilla container screen** by replacing its texture, Scaffolding recreates that reskin on the matching Bedrock screen too. `vanillaBackground.convertOverrides` in `config.yml` controls this. It is on by default. Turn it off if you do not reskin vanilla content and want a smaller pack.

`vanillaBackground.hideBackground` (also on by default) hides Bedrock's own window background behind those reskins, so no vanilla art shows through under yours. Turn it off to keep the gray panel behind your art.

**Supported screens, if your pack has them:**

* Chest, double chest and ender chest
* Shulker box
* Furnace, blast furnace and smoker
* Crafting table
* Player inventory
* Enchanting table
* Anvil
* Brewing stand
* Villager trading
* Hopper, dropper, dispenser and crafter

### Vanilla HUD overrides

Retextures of the vanilla HUD are converted to their Bedrock versions. Bedrock stretches each texture to fit its spot on the screen, so the resolution of your texture does not matter.

**Converted HUD elements include:**

* Hotbar and the selected-slot box
* Hearts (health, absorption, frozen, vehicle/mount)
* Hunger, armor, air and experience bars
* Mob effect status backgrounds
* Locator bar

Some HUD parts only exist on Java and have **nothing to match on Bedrock**, so they are skipped and noted in the log: poisoned, withered and hardcore hearts, the crosshair and attack indicators, the jump/ride bar, the icons for each status effect, and offhand slots.

{% hint style="info" %}
This page covers retextures of the **vanilla** HUD.\
HUDs from **MythicHUD** and **BetterHud** are converted separately, see the third-party plugins on the [Scaffolding](./) page.
{% endhint %}
