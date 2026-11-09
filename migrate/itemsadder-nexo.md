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
**Copy the contents of `plugins/ItemsAdder` into `plugins/Nexo/converter/ItemsAdder`**

The `plugins/Nexo/converter/ItemsAdder` folder does not exist by default, so create the required folders yourself.\
Also make sure to keep the folder `plugins/ItemsAdder`, as this will be used later for the conversion process.\
On server reload, Nexo will empty the data from the `plugins/Nexo/converter/ItemsAdder` folder into a valid Nexo config and remove the folder.\
If any item or recipe fails to convert, the folder is kept so you can fix the issue and try again.\
This step may be repeated for as many ItemsAdder packs as you would like to add, even at a future date.
{% endstep %}

{% step %}
**Take a backup**

It is recommended to make a backup of your server's world folders before swapping to Nexo, as there might be small oversights leading to minor loss of furniture/custom blocks.\\
{% endstep %}

{% step %}
**Remove ItemsAdder and LoneLibs .jar files**

Make sure to only delete the jar files - keep the folder `plugins/ItemsAdder`.\\
{% endstep %}

{% step %}
**Start your server**
{% endstep %}

{% step %}
**Check console for conversion issues. And finally, test that the migration has worked by testing items, glyphs, and anything else that may be on your server!**
{% endstep %}
{% endstepper %}

<mark style="color:red;">ResourcePack</mark> content from ItemsAdder is all bundled into `Nexo/pack/external_packs/ItemsAdder/assets/namespace/...`\
<mark style="color:green;">Items</mark> are moved into `Nexo/items/itemsadder/namespace/...`\
<mark style="color:yellow;">Glyphs/Font</mark> Images are moved in `Nexo/glyphs/itemsadder/namespace/...`\
<mark style="color:blue;">Recipes</mark> are moved into `Nexo/recipes/...` and <mark style="color:purple;">Sounds</mark> into `Nexo/sounds.yml`

### What is converted

Alongside items, glyphs and the ResourcePack, Nexo converts the following from ItemsAdder:

* **Recipes -** crafting table, cooking (furnace, blast furnace, smoker & campfire), anvil repair, smithing, brewing & stonecutter recipes. A `permission_suffix` becomes the permission `ia.user.recipe.<suffix>`
* **Sounds -** the `sounds` section, and the sounds of blocks and furniture
* **Furniture -** lights, placement offsets & `placeable_on`
* **Blocks -** `blast_resistance` & `no_explosion`
* **Elytras -** the wings texture & broken texture
* **Glyphs -** `symbol`, `suggest_in_command`, `show_in_gui` & shadow color

Anything Nexo cannot convert is logged in console, so check it after converting.

### Converter Options

`plugins/Nexo/converter.yml` has a few options for the ItemsAdder converter.

```yaml
itemsadderConverter:
  convertItems: true
  convertResourcePack: true
  convertFurnitureOnLoad: true
  prependNamespaceToIds: false
  changedItemIds: {}
```

ItemsAdder items are identified by `namespace:id`, while NexoItems only have an id.\
By default Nexo keeps the id as is, and only when several namespaces use the same id are the later ones prefixed with their namespace, like `my_namespace_ruby`.\
With `prependNamespaceToIds: true` every id is prefixed with its namespace.

Nexo keeps track of every id it renamed in `changedItemIds`, so furniture placed with ItemsAdder can be matched to the new id.

### <mark style="color:yellow;">Known issues</mark>

Nexo won't be able to migrate everything, as some features are not compatible across both plugins.\
For example, non-Display Entity furniture placed in your world before conversion will NOT be automatically converted.\\
