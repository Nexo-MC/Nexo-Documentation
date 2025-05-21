# 🎵 Sounds

Nexo allows you to register custom sounds that can be used in `/playsound`or other plugins\
The most basic of sounds can be configured like below by editing \`plugins/Nexo/sounds.yml\`

```yaml
sounds:
  - id: block.custom.mysound   # id: namespace:id
    sound: nexo:mysound.ogg    # References assets/nexo/sounds/mysound.ogg
    #sounds:                   # Optional, list of sounds where a random will be selected
    #  - mysound.ogg
    #  - mysound2.ogg
```

There are also some more properties you can tweak if needed, but for majority of cases, the above default will be enough. A detailed explanation of each property can be found [here](https://minecraft.wiki/w/Sounds.json)

```yaml
#https://minecraft.wiki/w/Sounds.json
sounds:
  - id: nexo:music.something
    sound: nexo:music/something.ogg
    sounds:                                  # Alternative if you have more than 1 sound-file
      - nexo:music/something.ogg
      - nexo:music/something2.ogg
    stream: true                             # Optional, defaults to false
    preload: true                            # Optional, defaults to false
    volume: 1f                               # Optional, defaults to 1f
    pitch: 1f                                # Optional, defaults to 1f
    weight: 1                                # Optional, defaults to 1
    attenuation_distance: 13                 # Optional, defaults to 16
    jukebox_playable:                        # Optional, Used for registering a custom music-disc sound
      comparator_output: 15                  # Optional, defaults to 15, must be in 1..15
      range: X                               # Optional, If omitted, the sound will have a variable range.
      length_in_seconds: 2.5
      description: Description
```

There is also `jukebox_playable`which is used to register sounds used in custom music discs\
Nexo will generate the necessary datapack for this, which you can then reference in [JukeboxPlayable-Component](items-advanced.md#components) of your item



#### Replacing sounds

If you wanna replace sounds already in minecraft, you can do so by doing

```yaml
sounds:
  - id: block.glass.place # removes vanilla sound
    sounds: []
    replace: true
  - id: block.glass.break # replaces vanilla sound with custom sound
    sound: nexo:customglasssound
    replace: true
```
