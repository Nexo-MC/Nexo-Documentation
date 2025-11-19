# 📦 ItemsAdder → Nexo

This article explains how to migrate your ItemsAdder config to Nexo.\
The process will require a few manual steps due to the way ItemsAdder works.\
Nexo will convert all data where possible.

{% hint style="danger" %}
This is a converter for ItemsAdder v4.\
ItemsAdder v3.x has not been tested yet and might convert with some issues\
Recommended to use the ItemsAdder internal updating process before converting to Nexo.
{% endhint %}

{% stepper %}
{% step %}
**Put Nexo JAR in your server's `plugins` folder**
{% endstep %}

{% step %}
#### Copy the contents of `plugins/ItemsAdder` into `plugins/Nexo/converter/ItemsAdder`

The `plugins/Nexo/converter/ItemsAdder` folder does not exist by default, so create the required folders yourself.\
Also make sure to keep the folder `plugins/ItemsAdder`, as this will be used later  for the conversion process.\
On server reload, Nexo will convert the content from the `plugins/Nexo/converter/ItemsAdder` folder and delete it after.\
Any future packs you might get can then be put in here and it will all be converted again
{% endstep %}

{% step %}
**Take a backup**

It is recommended to make a backup of your server's world folders before swapping to Nexo, as there might be small oversights leading to minor loss of furniture/custom blocks.\
{% endstep %}

{% step %}
**Remove ItemsAdder & LoneLibs JAR-files**

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

Nexo wont be able to migrate it 100% as there will be some things that is not doable across plugins.\
The biggest issue most will face is that furniture placed in your world that is not using Display Entities, will not be automatically converted.\
Nexo will try and convert configs to its format and should mean new furniture placed will look the same.
