# ☄️ Oraxen → Nexo

This article explains how to migrate your Oraxen config to Nexo.\
The process will be mostly automatic, but first follow the steps below.\


{% stepper %}
{% step %}
**Put Nexo JAR in your server's `plugins` folder**
{% endstep %}

{% step %}
#### Copy the contents of `plugins/Oraxen` into `plugins/Nexo/converter/Oraxen`

The `plugins/Nexo/converter/Oraxen` folder does not exist by default, so create the required folders yourself.\
Also make sure to keep the folder `plugins/Oraxen`, as this will be used later for the conversion process.\
On server reload, Nexo will migrate the data from the `plugins/Nexo/converter/Oraxen` folder and delete it after.\
This step may be repeated for as many Oraxen packs as you would like to add, even at a future date.
{% endstep %}

{% step %}
**Ensure you remove Oraxen JAR from your plugins folder**

It is also recommended to go into your `Server/WORLD/datapacks` and remove any leftover packs from Oraxen
{% endstep %}

{% step %}
**Ensure you make a backup of your worlds**

Whilst migration should be flawless, it is still recommended to make a backup of your world-folders before swapping to Nexo\
There might be small oversights leading to minor loss of furniture/custom blocks
{% endstep %}

{% step %}
**Start your server**
{% endstep %}
{% endstepper %}

### ResourcePack

There are small changes in how ResourcePacks work between Oraxen and Nexo.\
The main change is that Nexo no longer has shortcut folders for `pack/models` etc.\
This has always caused lots of confusion, so Nexo follows the normal structure\
`pack/models` -> `pack/assets/minecraft/models` etc\
Nexo also allows for far easier importing of external resourcepacks.\
Simply add any ResourcePack .zip or ResourcePack-folder (MyPack/assets/...) to `pack/external_packs` and it will be included in the final pack.

### Items

Nexo will also automatically convert existing items from Oraxen -> Nexo when a player joins.\
These will also be scanned and converted where there has been changes.\
Most notably in how NoteBlock, StringBlock and Furniture-Mechanics are defined

### Furniture

Placed OraxenFurniture will also be automatically converted to Nexo-Furniture when they load.\
There might be some issues with furniture that were Item-Frame based due to Nexo only supporting ItemDisplay Furniture.\
These can just be manually replaced or via a future update\
\
Main config-changes here are with how seats, lights & hitboxes (barrier & interaction) are defined.\
Nexo allows for multiple interaction-hitboxes, seats and lights.\
Suggest reading [Furniture Mechanic](../mechanics/furniture-mechanic/) for more info

### Custom Blocks

Custom blocks will also be converted. There is a difference in the custom-variation calculation between Oraxen & Nexo. Nexo will, when importing OraxenItems' correct this custom-variation.\
Example: `custom_variation: 1` -> `custom_variation: 51`\
There are also some minor changes in how these mechanics are defined.\
Examples can be found at [NoteBlock Mechanic](../mechanics/custom-block-mechanics/noteblock-mechanic/) & [StringBlock Mechanic](../mechanics/custom-block-mechanics/stringblock-mechanic.md)\
\
\
**If there are any issues in the conversion process, let me know!**
