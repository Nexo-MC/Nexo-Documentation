---
layout:
  width: default
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
---

# 🖼️ Custom Paintings

{% hint style="info" %}
Nexo only generates the Datapack for 1.21.5+ servers. You can still use Custom Paintings on 1.21.1-1.21.4, but you will need to make the datapack manually.
{% endhint %}

As of 1.21 you can now make custom paintings via datapacks. Nexo streamlines this process by automating the generation of this datapack based on a `Nexo/paintings.yml` file.

Here is an example of adding a custom painting:

```yaml
paintings:
  nexo:custom_painting:
    author: boy0000
    title: <red>Custom Painting
    asset_id: nexo:custom_painting  # This is the path to the PNG, namespace:path
    width: 1     # The width of your painting, in number of blocks it takes up
    height: 1    # The height of your painting, in number of blocks it takes up
    random_place: true # Will place at random from the vanilla painting items
  nexo:animated_painting:
    author: boy0000
    title: <red>Animated Custom Painting
    asset_id: nexo:animated_painting
    width: 1
    height: 1
```

Then you simply put the Texture of your painting inside Nexo's ResourcePack where your asset\_id points to.\
All Painting-Textures are in `assets/NAMESPACE/textures/painting/PATH`\
The config-format is as with everything else `NAMESPACE:PATH`

For our above example it means we must put the texture inside `assets/nexo/textures/painting/custom_painting.png`

{% hint style="info" %}
Make sure to fully restart your server after adding a new Painting, as they are only registered on startup.
{% endhint %}

### Animated Paintings

You can also make animated paintings using an MCMETA-file.\
The width & height properties are the pixel-size of each frame in your PNG.\
Below is a basic example, [Minecraft Wiki](https://minecraft.wiki/w/Resource_pack#Texture_animation) has a more in-depth explanation.\\

{% code title="animated_painting.png.mcmeta" %}
```json
{
  "animation": {
    "width": 256,
    "height": 256,
    "frametime": 1
    
  }
}
```
{% endcode %}

This file needs to be named the same as your texture + .mcmeta\
For our above example it means we must put the texture inside `assets/nexo/textures/painting/animated_painting.png.mcmeta`

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTAoAxayP9PrBtX9UQ5wa%2Fuploads%2FNQBDM0CDYHw3xLDuMFvA%2F2025-07-19%2021-41-23.mp4?alt=media&token=84affb23-a6a7-491e-8053-d3bc14efc2f5" %}
Static Painting & Animated Painting using MCMeta
{% endembed %}

### NexoItem

When your Custom Painting has been registered, you can make a custom NexoItem which will place the given painting. Below is a basic example

```yaml
custom_painting:
  itemname: Custom Painting
  material: PAINTING
  Components:
    painting_variant: nexo:custom_painting
animated_painting:
  itemname: Animated Painting
  material: PAINTING
  Components:
    painting_variant: nexo:animated_painting
```
