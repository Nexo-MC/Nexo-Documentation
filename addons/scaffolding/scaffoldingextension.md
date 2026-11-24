# ScaffoldingExtension

The resource pack alone cannot show **furniture** or **ModelEngine** models. Geyser does not render either of them on Bedrock, so Scaffolding comes with a Geyser extension, the **ScaffoldingExtension**, that recreates them.

It is a Geyser extension, not a plugin, and is built against the Geyser `2.11.0` API.\
To install it, put `ScaffoldingExtension.jar` in Geyser's `extensions/` folder and restart. Scaffolding creates the mapping files the extension reads and delivers them for you. If Geyser runs on the same server, they go straight into Geyser's folders. If Geyser runs on a **proxy or standalone**, they are sent over the sync transport (see Setup).

{% hint style="warning" %}
Without the ScaffoldingExtension, items, blocks, armor and glyphs still convert and show, but **furniture and ModelEngine models will not render** for Bedrock players.
{% endhint %}

### Pack updates without a reload

The extension does not leave the Scaffolding pack in Geyser's `packs/` folder. It sends the pack to each Bedrock player itself while they connect, so every player always gets the newest pack:

* After a conversion, Bedrock players get the new pack **the next time they join**. You do not need `geyser reload`, and nobody gets disconnected.
* If a conversion changes the **mappings** (you added or removed items or blocks), Geyser still needs a restart to load them. Until you restart, players keep getting the pack that matches the mappings Geyser has loaded, so nothing looks broken in the meantime.
* This works the same whether Geyser runs on the same server, on a proxy or standalone.

When you first install the extension, it moves any Scaffolding pack it finds in Geyser's `packs/` folder into its own `packs/` folder and serves it from there. Leave that folder alone. Old pack versions are cleaned up automatically.

{% hint style="info" %}
You can safely turn off or remove the extension. Scaffolding notices, goes back to putting the pack in Geyser's `packs/` folder, and asks for a `geyser reload` again.
{% endhint %}

### Players loading large packs

Phones can take a while to load a large pack. With `forward-player-ping: true` in Geyser's config, these players could time out before they got in. The extension keeps them connected while their pack loads, for up to `packLoadKeepAlive` (default `5m`) in the extension's `config.yml`. Set it to `0s` to turn this off.

### NexoFurniture

NexoFurniture is placed as an **ItemDisplay entity** that carries the furniture's **ItemModel**.\
Geyser does not render display entities on Bedrock, so without the extension Bedrock players cannot see furniture at all. With the extension installed, Scaffolding converts the furniture's model like any other model, and the extension makes the display entity show up:

* It renders in the world at the correct **position, rotation and scale**.
* Transform interpolation is kept, so furniture that animates its transform moves smoothly.
* Each model's display transform is saved to a mapping file (`furniture_mappings/*.yml`), and the extension applies it again on Bedrock.

### ModelEngine

[ModelEngine](https://www.mythiccraft.io/) gives mobs custom models and animations.\
On Bedrock, the Scaffolding plugin and the extension work together to recreate them:

* **The plugin** keeps track of every active ModelEngine model whose blueprint was converted. It sends Bedrock players everything they need to see that model over a plugin-message channel: when it should appear and disappear as players come into and leave range, where it is and where it looks, which animation is playing, which bones are visible, its scale, the red hurt tint and its hitbox.
* **The extension** spawns each of these models for Bedrock players as its own custom Bedrock entity, and keeps it updated with what the plugin sends. ModelEngine hides the real mob from players, so the extension cannot follow that mob. It places the model where the plugin tells it to instead.

One mob can carry several models, and each one is tracked on its own.

**Remaps and skins:** when a model is remapped to look like another blueprint, Bedrock players see the new look too. This covers `remapmodel` in MythicMobs, the `remap` animation script, and plugins that swap bone models, as Scenes does for NPC skins.

* Every skin blueprint must be loaded in ModelEngine when the pack converts. Bedrock cannot swap models while the game runs, so Scaffolding bakes each skin into every model it can be put on.
* After you add new skin blueprints, restart Geyser once the pack has reconverted.
* Scaffolding only links blueprints that share most of the model's rig (the same bone names in the same rest pose). Single-bone cosmetics taken from unrelated models with `changepart` are not covered.
* Each linked skin adds its geometry and textures to the model, so the pack gets bigger with every skin a model can take.

**Riding MEG mounts:** Bedrock does not pass jump or sneak on to a ModelEngine mount, so the camera angle is used instead. Players look up to jump or fly up, and look straight down to go down. Sneaking still gets them off the mount.

Rotations are the one known weak spot. Most models render correctly, but in rare cases a few show wrong rotations (see [.](./ "mention"))

### Resource pack options

With `pack.split` on, the animated models are sent as a separate pack in two versions: full and light. Bedrock players pick one of them, or no animation at all, from a form the extension shows the first time they join. Each player's answer is saved. If a player changes their answer, it applies the next time they join, because Bedrock only receives packs while connecting.

You set up the form in `packs.yml` in the extension's folder (`extensions/scaffoldingextension/` in Geyser). Scaffolding creates this file for you and keeps it up to date until you edit it. Run `/<commandRoot> reload` to apply your edits.

<table><thead><tr><th width="200">Setting</th><th>Purpose</th></tr></thead><tbody><tr><td><code>showOnJoin</code></td><td>Show the form right after joining to players who have not answered yet.</td></tr><tr><td><code>rememberAnswer</code></td><td>Save answers in <code>playerPacks.yml</code> so each player is asked once. Off asks everyone on every join, so a player whose device struggles can pick again.</td></tr><tr><td><code>title</code></td><td>The title of the form.</td></tr><tr><td><code>rejoinMessage</code></td><td>The message sent after a player changes an answer.</td></tr><tr><td><code>noPacksMessage</code></td><td>Sent by the packs command when the player has no optional pack to pick.</td></tr><tr><td><code>questions</code></td><td>One form per question, with one button per option, in the order you list them.</td></tr></tbody></table>

Each question has a `text`, an optional `note` shown under it, a `default` option for new players, and its `options`. Each option has a `button` label and the `pack` it gives. Leave out `pack` for a "none of them" option. A player can only get one pack per question, and options for packs the player does not receive are hidden. Anywhere in the text, `{command}` is replaced with the command that reopens the form.

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
`pack` is the pack's original Scaffolding name. Keep it as it is, even if `pack.name` in the plugin's config renames the pack. The older `optionalPacks:` layout of `packs.yml` still works.
{% endhint %}

{% hint style="warning" %}
Always update the Scaffolding plugin and the ScaffoldingExtension together. An outdated extension shows no form and gives Bedrock players both animated packs at once.\
Scaffolding warns in the console when the two versions do not match, and tells you which one to update.
{% endhint %}

### Commands

Every extension command starts with `commandRoot` from the extension's `config.yml` (default `scaffoldingextension`). Run `/<commandRoot>` on its own to list them.

<table><thead><tr><th width="302.333251953125">Command</th><th width="250">Permission</th><th>What it does</th></tr></thead><tbody><tr><td><code>/&#x3C;commandRoot> reload</code></td><td><code>scaffolding.commands.reload</code></td><td>Reloads the config, mappings and <code>packs.yml</code> (<code>rl</code> also works).</td></tr><tr><td><code>/&#x3C;commandRoot> packs</code></td><td><code>scaffolding.commands.packs</code></td><td>Reopens the resource pack options form. Its name and description come from <code>packsCommand</code>.</td></tr></tbody></table>

When Geyser runs on your Paper or Folia server, or as Geyser-Standalone, everyone has `scaffolding.commands.packs` by default. When Geyser runs on **Velocity or BungeeCord**, give it to players with your permissions plugin.

For example, to get `/bedrock packs`, set this in the extension's `config.yml` and restart. Changes to these settings only apply after a restart.

```yaml
commandRoot: "bedrock"
packsCommand:
  name: "packs"
  description: "Choose which optional resource packs you receive"
```

Pick a root that no other plugin or extension uses.
