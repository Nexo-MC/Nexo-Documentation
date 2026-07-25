# 🖥️ Custom GUIs & HUDs

On Java, custom GUIs comes down to two things, and Scaffolding reproduces both on Bedrock:

1. **Custom GUIs** are a glyph (a unicode character defined in a font file) placed in the **title** of a custom inventory.
2. **HUD overrides** are replaced vanilla HUD textures, such as the hearts, hotbar or armor bar.

Scaffolding reads these straight from the pack's fonts and textures, so it is not tied to any one plugin's glyph setup. Conversion is automatic in the common case.

{% hint style="warning" %}
**Alignment is approximate**

Bedrock and Java lay their screens out differently, and Bedrock gives far less control over placement. The automatic conversion gets most screens close, but it is **not guaranteed pixel-perfect**, and some GUIs can show **larger inconsistencies**. Simple, chest-based screens convert best; dense or heavily custom layouts are the most likely to need a manual nudge.

Anything the automatic placement gets wrong can be corrected by hand, see [#tweaking-a-gui-manually](custom-guis-and-huds.md#tweaking-a-gui-manually "mention").
{% endhint %}

### Custom GUI backgrounds

A custom inventory background on Java is a tall glyph placed in the container's title. Bedrock has no title glyph, so Scaffolding takes that glyph's texture and draws it onto the Bedrock screen instead, shown only while that container is open.

This is **automatic** for every glyph Nexo uses as a background in a GUI title:

* The texture is placed on the matching Bedrock screen, sized and positioned to line up with the slot grid.
* It shows only while that container is open, matched by the container title.
* Any `<shift:N>` in front of the glyph in the Java title is folded into the overlay's placement, since Bedrock cannot shift title text itself.
* `autoBackgrounds` in `gui.yml` toggles the whole feature (on by default, see below).

Only glyphs actually used in a Nexo GUI title are turned into overlays, so a random tall glyph elsewhere in your pack does not become a stray background. Anything Nexo does not put in a title, a GUI from another plugin for instance, has to be added by hand.

### Tweaking a GUI manually

Everything the automatic conversion decides can be overridden per GUI in `plugins/Scaffolding/gui.yml`. Most setups never need this; reach for it when a background sits a few pixels off, renders at the wrong size, or when you want a glyph that was not picked up automatically.

Scaffolding writes the file for you on the first conversion if it does not exist, seeded with:

* your **auto-detected backgrounds**, commented out, ready to uncomment and override
* every other **tall glyph** as a commented candidate you can enable

Once the file exists it is never rewritten, so your edits are safe. Delete it if you want a fresh, re-seeded copy.

{% hint style="success" %}
**GUI Visualizer**

A visual tool for working out the alignment, instead of guessing at numbers, is available at [https://nexomc.com/tools/gui-visualizer](https://nexomc.com/tools/gui-visualizer).
{% endhint %}

{% hint style="info" %}
After editing `gui.yml`, run `/scf reload -f` and have your Bedrock players reconnect. Bedrock only re-downloads the pack on reconnect.
{% endhint %}

#### Settings

Two top-level keys, both optional:

| Setting            | Default | Purpose                                                                                                                              |
| ------------------ | ------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `autoBackgrounds`  | `true`  | Detect GUI backgrounds from your Nexo inventory titles. Set to `false` to show only the entries you list in this file.                  |
| `minHeight`        | `32`    | Minimum glyph height, in pixels, for a glyph to be listed as a commented candidate when the file is generated. Does not affect conversion. |

#### Entries

Each entry is keyed by its glyph id and overrides the automatic overlay for that glyph. Only `glyph` is required, every other field falls back to the automatic value.

| Field           | Default            | Purpose                                                                                                                                                                       |
| --------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `glyph`         | required           | The Nexo glyph whose texture is drawn. Its texture and unicode are resolved from Nexo, so the id is all you need.                                                                |
| `match_literal` | the glyph          | Java title, written with Nexo tags such as `"<glyph:my_gui>"`. The overlay shows only while the open container's title contains it.                                              |
| `match_title`   | -                  | Same as above but a raw literal string, with no tag resolution. Use it when the title carries no Nexo tag.                                                                       |
| `shift`         | `0`                | Horizontal nudge in pixels, mirroring the `<shift:N>` in front of the glyph on Java. Positive moves right.                                                                       |
| `size`          | auto               | `"W,H"`. `"162px,54px"` is fixed UI pixels, `"100,100"` or `"100%,100%"` is a percentage of the parent panel. Prefer pixels: they align to Bedrock's 18px slot grid without drift. |
| `offset`        | auto               | `"x,y"` pixel offset from the anchor. Positive x moves right, positive y moves down.                                                                                            |
| `anchor`        | `center`           | Where the image attaches to the screen. `center` for window art, `top_left` and the other JSON-UI anchors for HUD pieces.                                                        |
| `layer`         | `13`               | Draw order. `13` sits above the slot backgrounds and below the item icons; raise it to draw over items, lower it to hide behind them.                                            |
| `screen`        | `container`        | Which Bedrock screen the art is injected into, see the table below.                                                                                                             |

{% hint style="warning" %}
An entry with no match, or with a `match_literal` that cannot be resolved (a typo'd glyph id, for example), is **always visible** on that screen. Scaffolding logs a warning when this happens.
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

| `screen`                             | Where it draws                                                    |
| ------------------------------------ | ----------------------------------------------------------------- |
| `container` / `chest`                | Chest and double chest, the default for custom inventories.       |
| `shulker_box`                        | Shulker box.                                                      |
| `inventory`                          | The whole survival inventory screen.                              |
| `player_inventory`                   | The inventory window's top half only.                             |
| `crafting_table`                     | Crafting table window.                                            |
| `furnace`, `blast_furnace`, `smoker` | The 176x166 window of each smelting screen.                       |
| `enchanting`                         | Enchanting table.                                                 |
| `anvil`                              | Anvil.                                                            |
| `smithing_table`                     | Smithing table.                                                   |
| `grindstone`                         | Grindstone.                                                       |
| `brewing_stand`                      | Brewing stand.                                                    |
| `villager`                           | The right panel of the trading screen.                            |
| `hud`                                | The in-game HUD, drawn on top of everything.                      |

#### Commands

| Command                          | What it does                                                                                                |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| `/scf gui list`                  | List the active overlays, auto-detected and from `gui.yml`, with the screen and title match each one uses.    |
| `/scf gui import <glyph> [screen]` | Append an entry for a glyph to `gui.yml` and reconvert. Size and offset are left to auto-detect.             |

#### Advanced: injection points

Bedrock's own screen and control names occasionally move between game versions. If an update breaks a screen, the injection point can be repointed per entry without waiting for a Scaffolding update.

| Field         | Purpose                                                                       |
| ------------- | ----------------------------------------------------------------------------- |
| `ui_file`     | Bedrock JSON-UI file to patch, for example `ui/chest_screen.json`.             |
| `namespace`   | JSON-UI namespace of that file, for example `chest`.                          |
| `root`        | A single control to insert the overlay into.                                  |
| `roots`       | A list of controls, for screens with more than one panel (small/large chest). |
| `array`       | Name of the child array on the control, `controls` on every vanilla screen.   |
| `layer_bias`  | Layer offset compensating the root's own depth, so `layer` means the same everywhere. |

{% hint style="info" %}
A malformed `gui.yml` is ignored entirely and a single bad entry is skipped, in both cases with a warning in the console. Conversion carries on either way, so a typo can never break your pack.
{% endhint %}

### Sizing a glyph

Bedrock renders a glyph at its baked pixel size, so size and sharpness move together — a bigger bake is larger _and_ sharper, a smaller bake is smaller _and_ blockier. Override that bake per font or per glyph in `plugins/Scaffolding/glyphs.yml`. Most setups never touch this file.

Two sections, both keyed by id: `fonts:` (by font key) and `glyphs:` (by glyph id). A `glyphs:` entry wins over a `fonts:` entry for the same glyph. Every field is optional.

<table><thead><tr><th width="136.99993896484375">Field</th><th>Purpose</th></tr></thead><tbody><tr><td><code>scale</code></td><td>Multiply the glyph's Java height. <code>2.0</code> = twice as tall, and sharper.</td></tr><tr><td><code>height</code></td><td>Pin an explicit baked height in px. Overrides <code>scale</code>.</td></tr><tr><td><code>supersample</code></td><td>Bake from the full-resolution source texture instead of the Java height. Sharpest, but renders larger — good for big or UI glyphs.</td></tr></tbody></table>

### Vanilla GUI overrides

If your pack reskins a **vanilla container screen** (by replacing its texture), Scaffolding reproduces that on the matching Bedrock screen too. This is controlled by `vanillaBackground.convertOverrides` in `config.yml` (on by default; turn it off if you do not reskin vanilla content and want a smaller pack).

`vanillaBackground.hideBackground` (also on by default) hides Bedrock's own window background behind those reskins, so nothing vanilla peeks out from under your art. Turn it off to keep the gray panel drawn behind it.

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
