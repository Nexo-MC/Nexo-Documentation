---
cover: ../../.gitbook/assets/image.png
coverY: 0
---

# 🤖 2D Player Heads

2D Player Heads are used by a lot of servers to display the players skin in a stylish way.\
As this is a very popular feature there are conflicts when several plugins use the Player-Head resourcepack files.

With the Pack here from [NexoAssets](https://mcmodels.net/products/14834/2d-player-heads) you can easily create 2D Player-Heads.\
It uses ItemModels, hence only supports **1.21.4+**, but wont conflict with any other ResourcePack

It comes with a premade Nexo-setup, making it easy to add, but all it contains is a ResourcePack added as a Nexo ExternalPack.\
**Example command for getting the items:**

{% code title="1x1 PlayerHead:" overflow="wrap" %}
```json
/minecraft:give player_head[item_model:"nexo:2d_player_head",profile={"name":"boy0000"}]
```
{% endcode %}

{% code title="2x2 PlayerHead" overflow="wrap" %}
```json
/minecraft:give player_head[item_model:"nexo:2d_player_head_large",profile={"name":"boy0000"}]
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>1x1 &#x26; 2x2 PlayerHeads for Boy0000 &#x26; Sixsoul (NexoAssets)</p></figcaption></figure>
