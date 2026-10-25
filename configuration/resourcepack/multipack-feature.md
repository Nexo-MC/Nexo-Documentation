---
icon: folders
layout:
  width: wide
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# MultiPack Feature

The Multipack feature allows for sending additional ResourcePacks to players with the base-pack.\
Each pack is defined as a **template**, which can be required, optional, or enabled by default.\
Players can toggle optional templates on/off, and Nexo re-sends the appropriate packs automatically.

## How it works

* Templates are standalone resource packs stored in `plugins/Nexo/pack/template_packs/` (or at a custom path).
* On startup/reload, each template is read, built, and hosted alongside the main pack.
* When a player joins, they receive the main Nexo pack plus any template packs that are enabled for them (required ones + their personal selections).
* Templates can declare conflicts with each other, meaning enabling one automatically disables the conflicting template(s).

***

## Configuration

All multipack configuration lives in `plugins/Nexo/multipack.yml`.\
Templates are defined under the `templates:` key, and the optional GUI menu under `menu:`.

```yaml
templates:
  my_template:
    required: false       # Always sent to all players, cannot be toggled
    default: true         # Enabled by default for new players
    conflicts_with:       # Disables these templates when this one is enabled
      - other_template
    path: ""              # Optional: custom path to the pack folder or zip
                          # Defaults to plugins/Nexo/pack/template_packs/<id>
  other_template:
    required: false
    default: false
    conflicts_with: my_template  # Can also be a single string

menu:
  # See the GUI / Menu section below
```

### Template options

<table><thead><tr><th width="148">Option</th><th width="117">Type</th><th width="108">Default</th><th>Description</th></tr></thead><tbody><tr><td><code>required</code></td><td>boolean</td><td><code>false</code></td><td>Always sent to every player; cannot be toggled off</td></tr><tr><td><code>default</code></td><td>boolean</td><td><code>false</code></td><td>Enabled by default for players who have never toggled it</td></tr><tr><td><code>conflicts_with</code></td><td>string or list</td><td><code>[]</code></td><td>IDs of templates to disable when this one is enabled</td></tr><tr><td><code>path</code></td><td>string</td><td><code>""</code></td><td>Path to the pack. Accepts absolute paths, paths relative to <code>template_packs/</code>, or paths relative to the Nexo data folder. Defaults to <code>template_packs/&#x3C;id></code></td></tr><tr><td><code>empty</code></td><td>boolean</td><td><code>false</code></td><td>The template has no pack and sends nothing. Useful as a "none" option in a cycle, or as a setting read through <code>%nexo_multipack_&#x3C;id>%</code></td></tr></tbody></table>

## Pack folder structure

Place each template pack as a folder or zip inside `plugins/Nexo/pack/template_packs`.\
This follows the same logic as [#resourcepack-structure](./#resourcepack-structure "mention")

If the pack has no `pack.mcmeta`, Nexo generates one based on the server's version.

***

## GUI / Menu

Nexo includes a built-in inventory GUI for players to browse and toggle their template selections without needing commands. The menu is configured under the `menu:` key in `multipack.yml`.

### Opening the menu

```
/nexo multipack
/nexo multipack menu
/nexo multipack menu <targets>
```

* Permission: `nexo.command.multipack.menu`
* Permission for opening for others: `nexo.command.multipack.menu.other`

Changes made inside the GUI are **batched**, meaning packs are only re-sent once when the inventory is closed, not on every click.

### Menu configuration

```yaml
menu:
  title: "<gold>My Resourcepack Menu"   # Defaults to "<gold>Multipack"
  rows: 3          # 1-6, defaults to 6

  slots:
    my_slot:
      offset: 5,2      # Column (x: 1–9) and row (y: 1–<rows>) of the top-left cell
      size: 1,1        # How many cells wide/tall this slot occupies (defaults to 1,1)
      # Only the top-left cell shows the item, the other cells are invisible but still clickable
      all_slots_except_first_empty: false
      base_item:   # Fallback item shown when the action's state has no own item
        material: PAPER
        itemname: "<gray>My Pack"
      action:
        # See action types below
```

#### Slot options

<table><thead><tr><th width="220">Option</th><th width="100">Type</th><th width="100">Default</th><th>Description</th></tr></thead><tbody><tr><td><code>offset</code></td><td><code>x,y</code></td><td>—</td><td>Column (1-9) and row (1-rows) of the top-left cell of the slot. Required, cells outside the menu are skipped</td></tr><tr><td><code>size</code></td><td><code>x,y</code></td><td><code>1,1</code></td><td>Width and height in cells. Useful for decorative multi-cell slots</td></tr><tr><td><code>all_slots_except_first_empty</code></td><td>boolean</td><td><code>false</code></td><td>When <code>true</code>, only the top-left cell shows the item. The other cells stay clickable but show an invisible placeholder that copies the data components of the item currently shown</td></tr><tr><td><code>base_item</code></td><td>item section</td><td>—</td><td>Fallback item used when a state has no own item defined. Required unless every action state defines its own item</td></tr><tr><td><code>action</code></td><td>section</td><td>—</td><td>Defines what happens when the slot is clicked (see below)</td></tr></tbody></table>

***

### Action types

#### TOGGLE

Displays one of two items depending on whether the target template is currently enabled, and flips it on click.

```yaml
action:
  type: TOGGLE
  target: my_template   # Template ID to toggle

  enabled_item:         # Item shown when the template is ON
    material: LIME_DYE
    itemname: "<green>Music Pack <gray>| <green>Enabled"

  disabled_item:        # Item shown when the template is OFF
    material: GRAY_DYE
    itemname: "<red>Music Pack <gray>| <red>Disabled"
```

`enabled_item` and `disabled_item` are merged on top of `base_item` if one is defined, so shared properties (e.g. lore) can be put in `base_item` and only the differences in each state item.

Required templates cannot be toggled, clicking their slot does nothing.

#### CYCLING

Cycles through a list of templates on each click, enabling exactly one at a time. Useful for mutually-exclusive choices like 2D vs 3D tools.

**Simple form** — template IDs only, inherits `base_item` for the display:

```yaml
action:
  type: CYCLING
  targets:
    - 2d_tools
    - 3d_tools
```

**Rich form** | each entry can carry its own item, merged on top of `base_item`:

```yaml
action:
  type: CYCLING
  targets:
    - id: 2d_tools
      material: PAPER
      itemname: "<aqua>2D Tools"
    - id: 3d_tools
      material: IRON_SWORD
      itemname: "<gold>3D Tools"
```

On click, the currently-enabled entry is disabled and the next one in the list is enabled (wrapping around). All other entries in the cycle are set to `false`.\
Required templates in the list are skipped.

***

### Item definition

Items in `base_item`, `enabled_item`, `disabled_item`, and cycling entries support three formats:

**Nexo item** | references an existing Nexo item by ID.\
`itemname`, `customname` and `lore` can be set to override those of the item:

```yaml
base_item:
  nexo_item: my_item_id
  itemname: "<gray>My Pack"
  lore:
    - "<dark_gray>Click to toggle"
```

**Item model** | An ItemModelBuilder, refer to [#itemmodel-builder/README.md](../items/itemmodel-builder/README.md "mention") for details. Can be used to create simple custom items without needing to set up a full Nexo item.\
The item is always a `PAPER` with only this model, any other keys like `itemname` or `lore` are ignored.

```yaml
base_item:
  item_model:
    type: "composite"
    models:
      - type: model
        model: "item/diamond_sword"
      - type: model
        model: "item/diamond"
```

**Inline item** | a standard Nexo item section (material, itemname, lore, etc.):

```yaml
base_item:
  material: PAPER
  itemname: "<gray>My Pack"
  lore:
    - "<dark_gray>Click to toggle"
```

***

## Commands

MultiPack commands are under `/nexo multipack` and require the `nexo.command.multipack` permission.

### Open GUI

```
/nexo multipack
/nexo multipack menu
/nexo multipack menu <targets>
```

Opens the interactive template selection menu. If no `menu:` section is configured in `multipack.yml`, a warning is shown instead.

* Permission: `nexo.command.multipack.menu`
* Permission for targeting others: `nexo.command.multipack.menu.other`

### List templates

```
/nexo multipack list
```

Shows all configured templates and their current state (enabled/disabled) for the executing player.\
Required and default templates are labeled.

### Toggle a template

```
/nexo multipack toggle <template>
/nexo multipack toggle <template> <targets>
```

Toggles the given template on or off for the player (or targeted players).\
Re-applies packs immediately after toggling. Required templates cannot be toggled.

* Permission: `nexo.command.multipack.toggle`
* Permission for targeting others: `nexo.command.multipack.toggle.others`&#x20;

### Debug

```
/nexo multipack debug
/nexo multipack debug <targets>
```

Prints detailed debug info: loaded templates, raw PDC selections, resolved enabled set, and per-template state flags.

* Permission: `nexo.command.multipack.debug`
* Permission for targeting others: `nexo.command.multipack.debug.others`

***

## Examples

### Toggling on/off a larger Music/SoundFX Pack | 2D/3D Tools

A common use case is offering players a choice to enable an addon for custom music, or swapping between 2D & 3D Tools

**`multipack.yml`:**

```yaml
templates:
  custom_music:
    required: false
    default: false
    path: "custom_music"
  2d_tools:
    required: false
    default: true
    conflicts_with: 3d_tools
  3d_tools:
    required: false
    default: false
    conflicts_with: 2d_tools
```

Players can switch between them in-game:

```
/nexo multipack list
/nexo multipack toggle custom_music
/nexo multipack toggle 3d_tools
```

Enabling `3d_tools` automatically disables `2d_tools` due to the conflict, and packs are re-sent immediately.

***

### Full GUI example

A 3-row menu with a music toggle and a 2D/3D cycling slot:

```yaml
templates:
  custom_music:
    required: false
    default: false
  2d_tools:
    required: false
    default: true
    conflicts_with: 3d_tools
  3d_tools:
    required: false
    default: false
    conflicts_with: 2d_tools

menu:
  title: "<gold>Resource Pack Options"
  rows: 3

  slots:
    music_toggle:
      offset: 3,2
      base_item:
        material: NOTE_BLOCK
        lore:
          - "<dark_gray>Click to toggle"
      action:
        type: TOGGLE
        target: custom_music
        enabled_item:
          itemname: "<green>Music Pack <gray>| <green>Enabled"
        disabled_item:
          itemname: "<red>Music Pack <gray>| <red>Disabled"

    tool_style:
      offset: 7,2
      base_item:
        material: STICK
        lore:
          - "<dark_gray>Click to switch style"
      action:
        type: CYCLING
        targets:
          - id: 2d_tools
            itemname: "<aqua>Tools <gray>| <aqua>2D"
          - id: 3d_tools
            itemname: "<gold>Tools <gray>| <gold>3D"
```
