---
icon: network-wired
---

# NexoProxy

NexoProxy is a [Velocity](https://papermc.io/software/velocity) plugin addon for Nexo that solves common ResourcePack and Glyph headaches caused by proxy networks.

## Features

### Blocking Duplicate ResourcePacks

When players switch between backend servers on your network, Velocity normally unloads and reloads the ResourcePack even if it is identical on both servers.\
NexoProxy detects this and **blocks the duplicate send**, so players experience no interruption.

It also handles obfuscated NexoPacks: if the underlying pack content is identical across two servers, the duplicate send is still blocked even when the obfuscated file hashes differ.

### Glyph Tags in Velocity Plugins

NexoProxy adds support for using Nexo's `<glyph:id>` tags inside other Velocity plugins such as [Velocitab](https://modrinth.com/plugin/velocitab) and [TAB](https://hangar.papermc.io/NEZNAMY/TAB), letting you display Nexo glyphs in tab lists, scoreboards, and other proxy-side UI without any extra configuration.

## Setup

1. Drop `NexoProxy.jar` into your Velocity `plugins/` folder.
2. Make sure Nexo is installed on your backend servers as normal.
3. No additional configuration is required — duplicate pack detection and glyph tag support are active automatically.

{% hint style="warning" %}
The very first time a player joins a backend server after NexoProxy is installed, duplicate blocking will not apply, the proxy is informed of the pack details only after the initial send. All subsequent joins and server switches will be handled correctly.
{% endhint %}
