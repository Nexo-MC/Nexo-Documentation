# ScaffoldingExtension

**Furniture** and **ModelEngine** models are not drawn by the resource pack alone. Geyser does not render either on Bedrock by default, so Scaffolding ships a companion Geyser extension, the **ScaffoldingExtension**, that recreates them.

It is a Geyser-Extension (not as a plugin) and is built against the Geyser `2.11.0` API.\
Install it by dropping `ScaffoldingExtension.jar` into Geyser's `extensions/` folder and restarting. Scaffolding generates the mapping files it reads and deploys them automatically when Geyser is on the same server. On Velocity, copy them into the proxy's `extensions/scaffoldingextension/` folder (see Setup).

{% hint style="warning" %}
Without the ScaffoldingExtension, items, blocks, armor and glyphs still convert and show, but **furniture and ModelEngine models will not render** for Bedrock players.
{% endhint %}

{% hint style="danger" %}
**Known issue on Geyser-Velocity** On a **Geyser-Velocity** setup the extension currently has known issues where **mobs (ModelEngine) and furniture may not render correctly**.\
A **Geyser-Spigot** setup (Geyser on the same Paper server) is **not affected**. \
If you rely on furniture or ModelEngine on Bedrock, prefer Geyser-Spigot for now.
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

* **Plugin side** tracks each active MEG model whose blueprint was converted, and mirrors its state to Bedrock viewers over a plugin-message channel: spawn and despawn on range, current animation, bone visibility, scale and hurt-tint. It never sends positions.
* **Extension side** spawns one model entity per tracked model, rendered as its custom Bedrock entity, and makes it follow the base mob. Because it follows the mob, only state has to be sent.

A single mob can carry several models, each tracked independently.

**Riding MEG mounts:** Bedrock sends no jump or sneak input while riding, so camera pitch stands in. Look up to jump or ascend, look straight down to sneak or descend, and start sneaking to dismount

Rotations are the one rough edge: models generally render correctly, but a few can show wrong rotations in rare cases (see [.](./ "mention"))
