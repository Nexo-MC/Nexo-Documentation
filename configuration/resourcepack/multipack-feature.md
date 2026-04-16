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

Templates are defined under `Pack.multipack_templates` in `settings.yml`:

```yaml
Pack:
  multipack_templates:
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
```

### Template options

<table><thead><tr><th width="148">Option</th><th width="117">Type</th><th width="108">Default</th><th>Description</th></tr></thead><tbody><tr><td><code>required</code></td><td>boolean</td><td><code>false</code></td><td>Always sent to every player; cannot be toggled off</td></tr><tr><td><code>default</code></td><td>boolean</td><td><code>false</code></td><td>Enabled by default for players who have never toggled it</td></tr><tr><td><code>conflicts_with</code></td><td>string or list</td><td><code>[]</code></td><td>IDs of templates to disable when this one is enabled</td></tr><tr><td><code>path</code></td><td>string</td><td><code>""</code></td><td>Path to the pack. Accepts absolute paths, paths relative to <code>template_packs/</code>, or paths relative to the Nexo data folder. Defaults to <code>template_packs/&#x3C;id></code></td></tr></tbody></table>

## Pack folder structure

Place each template pack as a folder or zip inside `plugins/Nexo/pack/template_packs`.\
This follows the same logic as [#resourcepack-structure](./#resourcepack-structure "mention")

If the pack has no `pack.mcmeta`, Nexo generates one based on the server's version.

***

## Commands

MultiPack commands are under `/nexo multipack` and require the `nexo.command.multipack` permission.

### List templates

```
/nexo multipack list
```

Shows all configured templates and their current state (enabled/disabled) for the executing player. Required and default templates are labeled.

### Toggle a template

```
/nexo multipack toggle <template>
/nexo multipack toggle <template> <targets>
```

Toggles the given template on or off for the player (or targeted players). Re-applies packs immediately after toggling. Required templates cannot be toggled.

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

**`settings.yml`:**

```yaml
Pack:
  multipack_templates:
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
