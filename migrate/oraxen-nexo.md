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
On server reload, Nexo will empty the data from the `plugins/Nexo/converter/Oraxen` folder into a valid Nexo config and remove the folder.\
This step may be repeated for as many Oraxen packs as you would like to add, even at a future date.
{% endstep %}

{% step %}
**Take a backup**

It is recommended to make a backup of your server's world folders before swapping to Nexo, as there might be small oversights leading to minor loss of furniture/custom blocks.\
{% endstep %}

{% step %}
**Remove Oraxen .jar file**

Make sure to only delete the jar files - keep the folder `plugins/Oraxen`.\
{% endstep %}

{% step %}
**Start your server**
{% endstep %}

{% step %}
**Check console for conversion issues. And finally, test that the migration has worked by testing items, glyphs, and anything else that may be on your server!**
{% endstep %}
{% endstepper %}

### Resource Packs

There are small changes in how ResourcePacks work between Oraxen and Nexo.\
The main change is that Nexo does not have shortcut folders for `pack/models` etc.\
Instead, Nexo follows the file structure used in vanilla Minecraft resource packs.\
For example, instead of using `pack/models`, Nexo uses `pack/assets/minecraft/models` (etc.)\
This system allows for the easier importing of vanilla Minecraft resource packs.\
You may add any resource pack .zip or ResourcePack-folder (MyPack/assets/...) to `pack/external_packs` and it will be included in the final pack.

### Items

When a player joins, any Oraxen items in their inventory will be converted to Nexo items.\
These will also be scanned and converted where there have been changes to the config, most notably in how NoteBlock, StringBlock and Furniture-Mechanics are defined.

### Furniture

Placed Oraxen furniture will be automatically converted to Nexo furniture when they load.\
There might be some issues with item frame furniture due to Nexo only supporting ItemDisplay furniture.\
These can be manually replaced, although an automatic conversion feature may be added in a future Nexo update.\
\
Main config changes here are with how seats, lights, and [hitboxes](../mechanics/furniture-mechanic/hitbox) are defined.\
Nexo allows for multiple interaction hitboxes, seats, and lights. Read [Furniture Mechanic](../mechanics/furniture-mechanic/) for more info.

### Custom Blocks

Custom blocks will be converted to Nexo, however there is a difference in the custom-variation calculation between Oraxen and Nexo. When importing OraxenItems, Nexo will correct this custom-variation.\
Example: `custom_variation: 1` -> `custom_variation: 51`\
There are also some minor changes in how these mechanics are defined.\
Examples can be found at [NoteBlock Mechanic](../mechanics/custom-block-mechanics/noteblock-mechanic/) and [StringBlock Mechanic](../mechanics/custom-block-mechanics/stringblock-mechanic.md).\
\
\
**If there are any issues in the conversion process, let the developers know!**
