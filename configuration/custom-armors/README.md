---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966823919917080626/unknown.png
coverY: 0
---

# ⛑️ Custom Player Armors

Like any other item, armor has a texture for when it is held or sitting in your inventory. Unlike most items, it _also_ needs a second texture that is drawn onto the player model when the armor is worn. This worn texture is what makes custom armor more involved than a normal item.

Nexo can generate both for you. There are two methods to choose from:

| Method        | Versions     | Base item        | Notes                                                                |
| ------------- | ------------ | ---------------- | ------------------------------------------------------------------- |
| **COMPONENT** | 1.21.2+      | Any material     | The recommended method. No restrictions, no datapack, no shaders.   |
| **TRIMS**     | 1.20–1.21.1  | `CHAINMAIL_*`    | For older servers only. Requires a generated datapack + restarts.   |

## Which method should I use?

* **Running 1.21.2 or newer?** Use [**COMPONENT**](components.md). There is no reason to use TRIMS or shader-based methods on these versions — COMPONENT has no downsides and is simpler to set up.
* **Running 1.21.1 and only allowing 1.20+ players?** [**TRIMS**](trims.md) is a good fit. It does not break when other shaders are present and needs no extra client mods, but it must use `CHAINMAIL` armor as the base item.

## Choosing the method

The method is set **once** for your whole server in `Nexo/settings.yml`:

```yaml
CustomArmor:
  # COMPONENT (1.21.2+) or TRIMS (1.20-1.21.1)
  armor_type: COMPONENT
```

{% hint style="warning" %}
This is a server-wide setting, not a per-item one. All custom armor on the server uses the method you pick here.
{% endhint %}

Once you've picked a method, head to the matching page:

* [Component Based (1.21.2+)](components.md)
* [Trims Based (1.20+)](trims.md)
* [Custom Elytras (1.21.2+)](custom-elytras-1.21.2+.md)
