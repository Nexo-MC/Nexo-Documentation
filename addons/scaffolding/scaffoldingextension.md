# ScaffoldingExtension

**Furniture** and **ModelEngine** models are not drawn by the resource pack alone. Geyser does not render either on Bedrock by default, so Scaffolding ships a companion Geyser extension, the **ScaffoldingExtension**, that recreates them.

It is a Geyser-Extension (not as a plugin) and is built against the Geyser `2.11.0` API.\
Install it by dropping `ScaffoldingExtension.jar` into Geyser's `extensions/` folder and restarting. Scaffolding generates the mapping files it reads and deploys them automatically: directly into Geyser's folders when Geyser runs on the same server, and over the sync transport when Geyser sits on a **proxy or runs standalone** (see Setup).

{% hint style="warning" %}
Without the ScaffoldingExtension, items, blocks, armor and glyphs still convert and show, but **furniture and ModelEngine models will not render** for Bedrock players.
{% endhint %}

### NexoFurniture

NexoFurniture is placed as an **ItemDisplay-entity** that carries the furniture's **ItemModel**.\
Geyser does not render display entities on Bedrock, so without the extension furniture is invisible to Bedrock players. With the extension installed, Scaffolding converts the furniture's model like any other, and the extension makes the display entity appear:

* It renders in the world at the correct **position, rotation and scale**.
* Transform interpolation is kept, so furniture that animates its transform moves smoothly.
* Each model's display transform is written to a mapping file (`furniture_mappings/*.yml`) that the extension re-applies.
* Dyeable furniture is the one gap: Bedrock cannot get tint from the item

### ModelEngine

[ModelEngine](https://www.mythiccraft.io/) gives mobs custom models and animations.\
On Bedrock these are recreated by the extension, working together with the plugin:

* **Plugin side** tracks each active MEG model whose blueprint was converted, and mirrors its state to Bedrock viewers over a plugin-message channel: spawn and despawn on range, position and look, current animation, bone visibility, scale, hurt-tint and the model's hitbox.
* **Extension side** spawns one model entity per tracked model, rendered as its custom Bedrock entity, and applies that streamed state. ModelEngine hides the base mob from clients, so the position is streamed rather than followed.

A single mob can carry several models, each tracked independently.

**Remaps and skins:** a model remapped onto another blueprint's look (`remapmodel` in MythicMobs, the `remap` animation script, or a plugin swapping bone models, as Scenes does for NPC skins) shows the new look on Bedrock too.

* Every skin blueprint must be loaded in ModelEngine when the pack converts. Scaffolding bakes each skin into the model it can be put on, since Bedrock cannot swap models at runtime.
* After adding new skin blueprints, restart Geyser once the pack has reconverted.
* Only blueprints that share most of the model's rig (same bone names in the same rest pose) are linked. Single-bone cosmetics pulled from unrelated models with `changepart` are not covered.
* Each linked skin adds its geometry and textures to the model, so the pack grows with every skin a model can take.

**Riding MEG mounts:** Bedrock sends no jump or sneak input while riding, so camera pitch stands in. Look up to jump or ascend, look straight down to sneak or descend, and start sneaking to dismount

Rotations are the one rough edge: models generally render correctly, but a few can show wrong rotations in rare cases (see [.](./ "mention"))

### Resource pack options

With `splitPacks` on, the animated models ship as their own pack in two versions: full and light. Bedrock players pick one, or no animation at all, from a form the extension shows when they first join. Answers are saved per player, and a changed answer applies on their next join, since Bedrock only receives packs while connecting.

The form is set up in `packs.yml` in the extension's folder (`extensions/scaffoldingextension/` in Geyser). Scaffolding creates it for you and keeps it up to date until you edit it. Edits apply with `/<commandRoot> reload`.

| Setting          | Purpose                                                                                                                                   |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `showOnJoin`     | Show the form to players who have not answered yet, right after they join.                                                                |
| `rememberAnswer` | Save answers in `playerPacks.yml` so a player is only asked once. Off keeps them until Geyser restarts and asks everyone on every join.   |
| `title`          | Title of the form.                                                                                                                        |
| `rejoinMessage`  | Sent after a player changes an answer.                                                                                                    |
| `noPacksMessage` | Sent by the packs command when the player has no optional pack to choose.                                                                 |
| `questions`      | One form per question, with a button per option in the order listed.                                                                      |

Each question has a `text`, an optional `note` under it, a `default` option for new players, and its `options`. An option has a `button` label and the `pack` it gives, or no `pack` for "none of them". The packs of one question exclude each other, and options whose pack the player does not receive are left out. `{command}` in any text becomes the command that reopens the form.

```yaml
questions:
  # Renaming the id asks everyone again
  animation:
    text: "Do you want animated models & textures? Might cause issues on lower-end hardware."
    note: "Crashing or lagging? Use {command} to pick the light version or turn animation off."
    default: animated
    options:
      animated:
        button: "Animated"
        pack: "Scaffolding Animated"
      light:
        button: "Animated (light)"
        pack: "Scaffolding Animated Simple"
      static:
        button: "Static"
```

{% hint style="info" %}
`pack` is the pack's original Scaffolding name. Keep it as is, even when `packName` in the plugin's config renames the pack. The older `optionalPacks:` layout of `packs.yml` is still read.
{% endhint %}

{% hint style="warning" %}
Update the Scaffolding plugin and the ScaffoldingExtension together. An outdated extension shows no form and gives Bedrock players both animated packs at once.
{% endhint %}

### Commands

Every extension command starts with `commandRoot` from the extension's `config.yml` (default `scaffoldingextension`). `/<commandRoot>` alone lists them.

<table><thead><tr><th width="302.333251953125">Command</th><th width="250">Permission</th><th>What it does</th></tr></thead><tbody><tr><td><code>/&#x3C;commandRoot> reload</code></td><td><code>scaffolding.commands.reload</code></td><td>Reload the config, mappings and <code>packs.yml</code> (<code>rl</code> also works).</td></tr><tr><td><code>/&#x3C;commandRoot> packs</code></td><td><code>scaffolding.commands.packs</code></td><td>Reopen the resource pack options form. The name and description come from <code>packsCommand</code>.</td></tr></tbody></table>

`scaffolding.commands.packs` is granted to everyone by default on Spigot, Paper, Geyser-Standalone and NeoForge. On **Velocity, BungeeCord and Fabric**, grant it with your permissions plugin.

For example, to get `/bedrock packs`, set this in the extension's `config.yml` and restart (changes to these settings only apply after a restart):

```yaml
commandRoot: "bedrock"
packsCommand:
  name: "packs"
  description: "Choose which optional resource packs you receive"
```

Pick a root no other plugin or extension uses.
