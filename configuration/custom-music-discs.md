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

# 💿 Custom Music Discs

Nexo streamlines the process of adding custom music discs to your server.\
You will need one valid OGG file, for your sound & a NexoItem referencing it.

### Registering your sound

To begin you will need to register your sound. This is essentially what [sounds.md](sounds.md "mention")explains.\
All Sound-OGG files go into the **sounds-folder** in the ResourcePack.\
If unsure how ResourcePacks work & how to structure files, read through [resourcepack.md](resourcepack.md "mention") & [#how-do-i-reference-a-resourcepack-file-in-a-config](../general-usage/faq/#how-do-i-reference-a-resourcepack-file-in-a-config "mention")

In short, navigate to `plugins/Nexo/sounds.yml` and add a basic entry for your sound

```yaml
sounds:
  - id: namespace:my.sound    # This is a key which will be used in the NexoItem
    file: namespace:my/sound  # This references your OGG file and where you put it
    stream: true              # Optional, defaults to false. Enable for long sounds
    jukebox_playable:
      comparator_output: 15   # Optional, defaults to 15, must be in 1..15
      range: X                # Optional, If omitted, the sound will have a variable range.
      duration: 2.5s
      description: Description
```

Now make sure you put the OGG file in the right spot. Above we have referenced `namespace:my/sound` -> `assets/namespace/sounds/my/sound.ogg`  inside `plugins/Nexo/pack/`

### Making the Custom Music Disc NexoItem

Now that the sound is all done we just need to make a very basic NexoItem that references the ID of our sound above. There is a slight difference in how the Jukebox Playable-Component is written depending on your server-version. [components.md](items-advanced/components.md "mention") will show you the one for your server.

For setting a custom texture/model on your NexoItem, you can define it under the Pack section.

```yaml
my_music_disc:
  itemname: My Music Disc
  material: PAPER
  Pack:
    texture: namespace:discs/my_music_disc
  Components:
    jukebox_playable:
      song_key: namespace:my.sound
```
