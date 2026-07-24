# 🪨 Scaffolding

Scaffolding is a Nexo addon that brings your server's custom content to **Bedrock players** who connect through [Geyser](https://geysermc.org/).

Nexo generates a Java ResourcePack for your custom items, blocks, furniture, armor, glyphs & more. Normally Bedrock-players cannot see any of this without a complex conversion of the Java-setup. Scaffolding handles all this for you automatically. It converts your entire Nexo-setup to a Bedrock compatible one, consisting of Geyser-mappings and MCPack files. It is also automatically deployed to Geyser and always kept up-to-date with your changes in Nexo.

<p align="center">MCModels  |  <a href="https://nexomc.com">NexoMC</a>  |  Voxel.shop</p>

{% hint style="warning" %}
**Early Access**

Scaffolding is in **early access**. It has had thorough testing and covers the large majority of Nexo content, but it is not guaranteed bug-free yet. If something looks wrong on Bedrock, report it in our Discord with a screenshot and the item, block or furniture involved. Quick bug reports are what push it toward a stable release.
{% endhint %}

<details>

<summary>Requirements (click to expand)</summary>

<table><thead><tr><th width="229.666748046875">Plugin</th><th width="126.6666259765625">Needed</th><th>Notes</th></tr></thead><tbody><tr><td><a href="https://nexomc.com">Nexo</a> <strong>1.26+</strong></td><td>Required</td><td>Scaffolding is a Nexo addon and reads the pack Nexo builds.</td></tr><tr><td><a href="https://geysermc.org/">Geyser</a> <code>2.11.0-SNAPSHOT</code> +</td><td>Required</td><td>Older Geyser builds lack the mapping and extension features Scaffolding relies on.</td></tr><tr><td><a href="https://geysermc.org/">Floodgate</a></td><td>Optional</td><td>Detects Bedrock players so their outgoing text is remapped to the Bedrock-safe glyph codepoints.</td></tr><tr><td><strong>ScaffoldingExtension</strong></td><td>Optional</td><td>Ships with Scaffolding. Required for <strong>NexoFurniture and/or ModelEngine</strong>.</td></tr></tbody></table>

Your server also needs outbound internet access.\
Scaffolding uploads the pack to a hosted converter service and unpacks the result, so the game server never does the heavy conversion itself.

</details>

### Setup

Where you run Geyser decides how Scaffolding deploys, so pick your setup below.

{% tabs %}
{% tab title="Paper (Geyser-Spigot)" %}
Nexo, Scaffolding and Geyser all run on one Paper server.

1. Drop `Scaffolding.jar` into `plugins/`, alongside Nexo and Geyser-Spigot.
2. Start the server. Scaffolding auto-detects Geyser and deploys the pack into its `packs/` and `custom_mappings/`.
3. **Restart once** so Geyser loads the new mappings.

That is it, nothing to configure in the common case.
{% endtab %}

{% tab title="Velocity (Geyser-Velocity)" %}
Here Geyser runs on the Velocity proxy, while Nexo and Scaffolding run on the backend Paper server.\
Scaffolding can't reach the proxy's Geyser folder, so it leaves the files in `plugins/Scaffolding/output/` to copy across.

1. Install Nexo and Scaffolding on the **backend Paper server**, and Geyser on the **Velocity proxy**.
2. Start the backend so Scaffolding converts once. The output lands in `plugins/Scaffolding/output/`.
3. Copy that output into the proxy's `Geyser-Velocity/` folders (below), then **restart the proxy** and reconnect.

| From `plugins/Scaffolding/output/` | To the proxy's `Geyser-Velocity/` folder    |
| ---------------------------------- | ------------------------------------------- |
| `*.mcpack`                         | `packs/`                                    |
| `geyser_mappings/*.json`           | `custom_mappings/`                          |
| `furniture_mappings/*.yml`         | `extensions/scaffoldingextension/mappings/` |
| `meg/models.json`                  | `extensions/scaffoldingextension/meg/`      |

{% hint style="success" %}
If the proxy and backend share a filesystem, symlink the two folders so the copy is automatic.\
Scaffolding only deploys on its own when Geyser is a plugin on the same server.
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Why the restart?**

Geyser loads custom mappings only at startup, and Bedrock re-downloads packs only on reconnect.\
So after changing your Nexo content, restart and have Bedrock players reconnect.\
Scaffolding logs when a restart is needed and stays quiet otherwise.
{% endhint %}

### Supported

<table><thead><tr><th width="180.6666259765625">Feature</th><th width="112.3333740234375">Status</th><th>Notes</th></tr></thead><tbody><tr><td>Items (2D and 3D)</td><td>✅ Works</td><td>3D models become held Bedrock models with an auto-rendered inventory icon; 2D items become sprites.</td></tr><tr><td>Bows, crossbows and tridents</td><td>✅ Works</td><td>Their draw and throw animations are rebuilt natively on Bedrock.</td></tr><tr><td>Custom blocks</td><td>✅ Works</td><td>All Nexo CustomBlocks (note-block, string, chorus, etc.) become real Bedrock custom blocks, with their sounds. Carpentry blocks likely work too, but are not fully tested yet.</td></tr><tr><td>Player armor</td><td>✅ Works</td><td>Custom armor with an equipment texture renders as worn armor.</td></tr><tr><td>Glyphs and emotes</td><td>✅ Works *</td><td>Rebuilt as Bedrock glyph sheets, so they show in chat, names and UI. Tune their Bedrock size per glyph or font ( <a data-mention href="emotes-and-glyphs.md">emotes-and-glyphs.md</a> )</td></tr><tr><td>Custom sounds</td><td>✅ Works</td><td>Remapped so Bedrock players hear them</td></tr><tr><td>Custom GUIs</td><td>✅ Works</td><td>A title glyph that draws a custom inventory background is reproduced automatically(<a data-mention href="./#custom-gui-and-hud">#custom-gui-and-hud</a>)</td></tr><tr><td>Vanilla GUI &#x26; HUD Overrides</td><td>✅ Works</td><td>Replaced vanilla GUIs &#x26; HUD-elements  are supported</td></tr><tr><td>NexoFurniture</td><td>✅ With extension</td><td>Requires <a data-mention href="./#scaffoldingextension">#scaffoldingextension</a></td></tr><tr><td>ModelEngine</td><td>✅ With extension</td><td>Requires <a data-mention href="./#scaffoldingextension">#scaffoldingextension</a></td></tr></tbody></table>

{% hint style="info" %}
**\* Glyphs on Bedrock**

Bedrock renders a glyph at its baked pixel size, so **scale and sharpness are tied together.**\
This is different from **Java,** where a glyph's size is set independently from its texture resolution.\
A larger texture meant to render as a small icon can therefore look **blurry** on Bedrock.\
See Emotes & Glyphs on Bedrock for how to tune this per glyph or font in `glyphs.yml`.
{% endhint %}

{% hint style="info" %}
Bedrock picks an item's look once from its data; it can't react to live gameplay states like Java.\
So **live-state model swaps,** like dyeing an item or renaming it, are not going to transfer over.
{% endhint %}

### Not yet supported

Scaffolding aims for parity, but a few Nexo features do not convert yet or have known rough edges on Bedrock:

<table><thead><tr><th width="173">Feature</th><th width="129.0001220703125">Status</th><th>Notes</th></tr></thead><tbody><tr><td>Dyeable models and furniture</td><td>⚠️ Not yet</td><td>Bedrock cannot read a color from the item stack, so dyed or tinted models and furniture show their texture as-is. This may become possible once Geyser merges <a href="https://github.com/GeyserMC/Geyser/pull/6392">PR #6392</a>, which adds Bedrock dyeable-component support to the custom item API.</td></tr><tr><td>Custom Elytras</td><td>⚠️ Partial</td><td>The wings render as worn armor, but Bedrock players <strong>cannot fly (glide) with them</strong>.</td></tr><tr><td>ModelEngine rotations</td><td>⚠️ Rare issue</td><td>Models generally render correctly via the extension, but a few can show wrong rotations in rare scenarios.</td></tr><tr><td>Custom mob armor</td><td>❌ Not converted</td><td>Custom armor worn by mobs (horse, wolf, etc.) does not render on Bedrock.</td></tr><tr><td>Custom paintings</td><td>❌ Not converted</td><td>Custom paintings show as vanilla for Bedrock players.</td></tr><tr><td>Hopper / dropper / dispenser reskins</td><td>❌ Not converted</td><td>These Bedrock screens are hardcoded and cannot be customized via a resource pack at the moment, so a reskin cannot reach them (see Custom GUI &#x26; HUD).</td></tr><tr><td>Custom HUD plugins (MythicHUD)</td><td>❌ Not yet</td><td>Custom HUDs added by plugins such as MythicHUD are not supported at the moment. Only vanilla HUD retextures convert.</td></tr></tbody></table>

### Custom GUI & HUD

On Java a custom screen is one of two things: a glyph placed in a custom inventory's title (a GUI background), or a replaced vanilla HUD texture. Scaffolding reproduces both on Bedrock, along with reskins of vanilla container screens.

{% hint style="warning" %}
**Automatic alignment is approximate**

Bedrock and Java lay their screens out differently, so the automatic placement is **not guaranteed pixel-perfect** and some GUIs can show larger inconsistencies.\
See Custom GUI & HUD for per-screen support, the HUD elements covered, and how to nudge or override a background.
{% endhint %}

### ScaffoldingExtension

**Furniture** and **ModelEngine** models are not drawn by the resource pack alone, so Scaffolding ships a companion Geyser extension that recreates them on Bedrock. Drop `ScaffoldingExtension.jar` into Geyser's `extensions/` folder and restart.

{% hint style="warning" %}
Without the ScaffoldingExtension, items, blocks, armor and glyphs still convert and show, but **furniture and ModelEngine models will not render** for Bedrock players.
{% endhint %}

See [#scaffoldingextension](./#scaffoldingextension "mention") for install detail, how furniture and ModelEngine are handled.

### Configuration

Defaults work for almost everyone, and config fount at  `plugins/Scaffolding/config.yml` .

<table><thead><tr><th width="198.333251953125">Setting</th><th width="97">Default</th><th>Purpose</th></tr></thead><tbody><tr><td><code>autoConvert</code></td><td><code>true</code></td><td>Convert and deploy automatically whenever Nexo rebuilds its pack.</td></tr><tr><td><code>iconSize</code></td><td><code>x64</code></td><td>Resolution of the rendered inventory icons. One of <code>x16</code>, <code>x32</code>, <code>x64</code> or <code>x128</code>.</td></tr><tr><td><code>compression</code></td><td><code>BALANCED</code></td><td>Texture encode tradeoff: <code>FAST</code> (biggest pack), <code>BALANCED</code>, or <code>MAX</code> (smallest, slowest).</td></tr><tr><td><code>cacheSize</code></td><td><code>10</code></td><td>How many past conversions to keep on disk so flipping settings is served from cache. <code>0</code> disables.</td></tr><tr><td><code>supportAnimatedItems</code></td><td><code>false</code></td><td>Split the pack into sub-packs plus an optional animated overlay players can opt out of, so a change re-sends only the affected part.</td></tr><tr><td><p><code>vanillaBackground.</code></p><p><code>convertOverrides</code></p></td><td><code>true</code></td><td>Also convert reskins of vanilla items and containers with no Nexo config. Turn off if you do not reskin vanilla content and want a smaller pack.</td></tr><tr><td><p><code>vanillaBackground.</code></p><p><code>hideBackground</code></p></td><td><code>true</code></td><td>Hide Bedrock's own window background behind converted vanilla GUI reskins, so nothing vanilla peeks out. Turn off to keep the gray panel drawn behind the art.</td></tr><tr><td><code>invertedCubeHalo</code></td><td><code>true</code></td><td>Render inside-out halo/glow shells the way Java shows them. Off removes the halo.</td></tr><tr><td><code>weaponUsePoses</code></td><td><code>false</code></td><td>Give custom shields and bows the vanilla in-use pose (block, bow draw). May drift on very different client versions.</td></tr><tr><td><code>converter.channel</code></td><td><code>STABLE</code></td><td>Which hosted converter to use: <code>STABLE</code> (production) or <code>DEV</code> (test builds). Ignored when a URL is set.</td></tr><tr><td><code>converter.timeout</code></td><td><code>10m</code></td><td>How long to wait for a conversion before giving up. Accepts <code>30s</code>, <code>10m</code>, <code>1h</code>.</td></tr></tbody></table>

### Commands

The base command is `/scaffolding` (aliases `/scaffold`, `/scf`).

<table><thead><tr><th width="302.333251953125">Command</th><th>What it does</th></tr></thead><tbody><tr><td><code>/scf help</code></td><td>List the available commands.</td></tr><tr><td><code>/scf reload &#x3C;-f></code></td><td>Reconvert the current Nexo pack and redeploy to Geyser (<code>rl</code> also works). Add <code>-f</code> to force new conversion, even when setup is the same</td></tr><tr><td><code>/scf status</code></td><td>Show the converter service, the last output pack, and check the service is reachable.</td></tr><tr><td><code>/scf gui list</code></td><td>List the GUI overlays configured in <code>gui.yml</code>.</td></tr><tr><td><code>/scf gui import &#x3C;glyph> [screen]</code></td><td>Add a glyph to <code>gui.yml</code> as an overlay and reconvert (screen defaults to <code>container</code>).</td></tr><tr><td><code>/scf cache list</code> / <code>clear</code></td><td>Inspect or clear the on-disk conversion cache.</td></tr></tbody></table>
