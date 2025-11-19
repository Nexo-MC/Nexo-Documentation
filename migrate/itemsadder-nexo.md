# 📦 ItemsAdder → Nexo

This article explains how to migrate your ItemsAdder config to Nexo.\
The process will be mostly automatic, but first follow the steps below.

{% hint style="danger" %}
This page covers migrating to Nexo from ItemsAdder v4.\
If you are on ItemsAdder v3.x, you must update ItemsAdder before migrating to Nexo.
{% endhint %}

{% stepper %}
{% step %}
**Put Nexo JAR in your server's `plugins` folder**
{% endstep %}

{% step %}
#### Copy the contents of `plugins/ItemsAdder` into `plugins/Nexo/converter/ItemsAdder`

The `plugins/Nexo/converter/ItemsAdder` folder does not exist by default, so create the required folders yourself.\
Also make sure to keep the folder `plugins/ItemsAdder`, as this will be used later for the conversion process.\
On server reload, Nexo will empty the data from the `plugins/Nexo/converter/ItemsAdder` folder into a valid Nexo config and remove the folder.\
This step may be repeated for as many ItemsAdder packs as you would like to add, even at a future date.
{% endstep %}

{% step %}
**Take a backup**

It is recommended to make a backup of your server's world folders before swapping to Nexo, as there might be small oversights leading to minor loss of furniture/custom blocks.\
{% endstep %}

{% step %}
**Remove ItemsAdder and LoneLibs .jar files**

Make sure to only delete the jar files - keep the folder `plugins/ItemsAdder`.\
{% endstep %}

{% step %}
**Start your server**
{% endstep %}

{% step %}
**Check console for conversion issues. And finally, test that the migration has worked by testing items, glyphs, and anything else that may be on your server!**
{% endstep %}
{% endstepper %}

<mark style="color:red;">ResourcePack</mark> content from ItemsAdder is all bundled into `Nexo/pack/external_packs/ItemsAdder/namespace/...`\
<mark style="color:green;">Items</mark> are moved into `Nexo/items/itemsadder/...`\
<mark style="color:yellow;">Glyphs/Font</mark> Images are moved in `Nexo/glyphs/itemsadder/namespace/...`

### <mark style="color:yellow;">Known issues</mark>

Nexo won't be able to migrate everything, as some features are not compatible across both plugins.\
For example, non-Display Entity furniture placed in your world before conversion will NOT be automatically converted.\
