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

{% hint style="info" %}
Pack blocking requires the proxy to already know a backend server's ResourcePack details. This information is sent over a plugin message channel, which can only be opened once at least one player is present on that server. This means the very first player to join a given backend server will always receive the pack normally, as the proxy has no way to block it yet. Every player after that will benefit from duplicate blocking, provided all backend servers share the same Nexo setup and therefore produce the same pack. Note that obfuscation is not a concern here: NexoProxy compares the unobfuscated pack hash, so identical packs are correctly recognised as duplicates even when their obfuscated hashes differ.
{% endhint %}
