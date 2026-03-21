---
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

# 🛑 Anti-Cheat Plugins

Nexo might cause conflicts with Anti-Cheat plugins when standing on [furniture-mechanic](../mechanics/furniture-mechanic/ "mention").\
NexoFurniture uses ClientSide hitboxes, meaning these plugins will think the player is floating/flying.\
\
Nexo has built-in support for the most common ones, like Vulkan & [Spartan/Vaca&#x6E;**\***](#user-content-fn-1)[^1]**.**\
The settings for these can be found in `mechanics.yml` under `Furniture.anti_cheat`.\
For other plugins like _LPX_ & _Polar Anti-Cheat_, there is no built-in support for these.\
There is an unofficial third-party addon you can download which should fix this: [NexoPolarBridge](https://github.com/SLNE-Development/NexoPolarBridge)



[^1]: This is mainly for older versions before it became changed over and became a subscription AI slop plugin
