# 📦 ItemsAdder → Nexo

Compared to migrating from Oraxen, ItemsAdder requires a few more manual steps.\
Nexo automates all it can but due to weird choices in ItemsAdder, some things wont be possible\
Nexo will convert all items, glyphs/font-images & resourcepacks where possible

{% hint style="warning" %}
This is unlikely to be a flawless process so do make sure you take backups and try it on a test-server first
{% endhint %}

{% hint style="danger" %}
This is a converter for ItemsAdder v4\
ItemsAdder v3.x has not been tested yet and might convert with some issues\
Recommended to use ItemsAdder internal updating process before converting to Nexo
{% endhint %}

{% stepper %}
{% step %}
#### Put nexo-1.x.jar in your `Server/plugins folder`
{% endstep %}

{% step %}
#### Take a backup of all your worlds

Whilst migration should be flawless, it is still recommended to make a backup of your world-folders before swapping to Nexo\
There might be small oversights leading to minor loss of furniture/custom blocks
{% endstep %}

{% step %}
#### Remove ItemsAdder & LoneLibs JAR-files

Keep `plugins/ItemsAdder` as this is what Nexo will convert from.\
Also good to keep it as a backup in-case you need to migrate again in the future.
{% endstep %}

{% step %}
#### Start your server
{% endstep %}

{% step %}
#### Check console for conversion issues and test out items/glyphs
{% endstep %}
{% endstepper %}

<mark style="color:red;">ResourcePack</mark> content from ItemsAdder is all bundled into `Nexo/pack/external_packs/ItemsAdder/namespace/...`\
<mark style="color:green;">Items</mark> are moved into `Nexo/items/itemsadder/...`\
<mark style="color:yellow;">Glyphs/Font</mark> Images are moved in `Nexo/glyphs/itemsadder/namespace/...`

### <mark style="color:yellow;">Known issues</mark>

Nexo wont be able to migrate it 100% as there will be some things that is not doable across plugins.\
The biggest issue most will face is that furniture placed in your world that is not using Display Entities, will not be automatically converted.\
Nexo will try and convert configs to its format and should mean new furniture placed will look the same.
