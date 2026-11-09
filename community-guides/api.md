---
cover: >-
  https://www.techyon.es/media/news/full-stack-developer-cu%C3%81les-son-las-principales-competencias_1637600851_21.jpg
coverY: 0
---

# API

### Repository & Dependencies

```kotlin
repositories {
    maven("https://repo.nexomc.com/releases")
}

dependencies {
    compileOnly("com.nexomc:nexo:<version>") //Nexo 1.X -> 1.X.0
}
```

## JavaDocs

Nexo has JavaDocs published at [https://jd.nexomc.com](https://jd.nexomc.com/). These will be updated whenever changes to the API are made, which is not too often.

## Custom Items

Nexo has its own ItemBuilder class which handles building its custom items.\
The [NexoItems](https://jd.nexomc.com/latest/com/nexomc/nexo/api/NexoItems.html)-class contains most of the methods you would need to handle items.

```java
ItemBuilder itemBuilder = NexoItems.itemFromId(itemID);
ItemStack itemStack = itemBuilder.build();
String itemId = NexoItems.idFromItem(itemStack);
```

{% hint style="info" %}
Nexo loads items in an async task, thus getting them in your plugins onEnable will likely fail\
You can listen for the NexoItemsLoadedEvent to be sure the items are registered
{% endhint %}

#### Modifying how Nexo updates a NexoItem

Nexo will update any NexoItem on several actions to ensure its data is up-to-date.\
If your plugin should override any property on the Item which Nexo resets, follow the steps below.

You need to register an UpdateCallback which lets you run logic on any item Nexo updates.\
This should be registered during NexoItemsLoadedEvent as shown below;

{% tabs fullWidth="true" %}
{% tab title="Kotlin" %}
{% code fullWidth="true" %}
```kotlin
@EventHandler
fun NexoItemsLoadedEvent.onLoaded() {
    NexoItems.registerUpdateCallback(Key.key("namespace:key"), object : UpdateCallback {
        override fun preUpdate(itemStack: ItemStack): ItemStack? {
            // return null to skip updating
            return null
        }
        
        override fun postUpdate(itemId: String, itemStack: ItemStack, preUpdateItemStack: ItemStack): ItemStack {
            // Apply changes after Nexo finishes updating the item
            return itemStack
        }
    })
}
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
```java
@EventHandler
public void onItemsLoaded(NexoItemsLoadedEvent event) {
    NexoItems.registerUpdateCallback(
        Key.key("namespace", "key"), new UpdateCallback() {

            @Override
            public ItemStack preUpdate(ItemStack itemStack) {
                // return null to skip updating
                return null;
            }

            @Override
            public ItemStack postUpdate(String itemId, ItemStack itemStack, ItemStack preUpdateItemStack) {
                // Apply changes after Nexo finishes updating the item
                return itemStack;
            }
        }
    );
}

```
{% endtab %}
{% endtabs %}

#### External Items

Plugins can register their own items with Nexo through code, instead of through a config in the items-folder.\
The `ConfigurationSection` is parsed like any item-config, with its name as the item-id, and is parsed again on every reload.

Nexo fills in anything the section leaves out, like `custom_variation` or `custom_model_data`, by writing it onto the section.\
Your plugin has to save these values itself, as otherwise placed custom blocks get a new variation on the next start.\
The optional `onConfigUpdated` is called with the section whenever Nexo writes to it.

The optional `itemFactory` provides your plugin's own item when a player uses pick-block on its blocks and furniture.\
`NexoItems.createItem(itemID)` returns that item for external items, and a normally built NexoItem otherwise.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
NexoItems.registerExternalItem(plugin, section, { updated -> saveSection(updated) }) { buildMyItem() }
```
{% endtab %}

{% tab title="Java" %}
```java
NexoItems.registerExternalItem(plugin, section, updated -> saveSection(updated), () -> buildMyItem());
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
An id already used by an item-config is refused.\
The `itemFactory` can be called from the player's region thread on Folia
{% endhint %}

#### Component Projections

`ComponentProjections` lets you rewrite any text Nexo sends to a player, per player.\
Nexo caches the text of items per player, so call `ComponentProjections.invalidate()` whenever your projection would return something different for the same text.

```java
ComponentProjections.register("myplugin:projection", player -> true, (player, component) -> component);
ComponentProjections.invalidate();
```

## Custom Blocks

The [NexoBlocks](https://jd.nexomc.com/latest/com/nexomc/nexo/api/NexoBlocks.html)-class contains all the methods available for placing, removing and checking for custom blocks in Nexo.

```java
NexoBlocks.place(itemID, location)
```

### Furniture

The [NexoFurniture](https://jd.nexomc.com/latest/com/nexomc/nexo/api/NexoFurniture.html)-class contains all the methods available for placing, removing and checking for furniture in Nexo. In addition to this you can return the [FurnitureMechanic](https://jd.nexomc.com/latest/com/nexomc/nexo/mechanics/furniture/FurnitureMechanic.html) of the Furniture to get specific properties of it if needed.

```java
NexoFurniture.place(itemID, location, rotation, blockFace)
NexoFurniture.place(itemID, location, yaw, blockFace)
```

#### Text-Entity Overrides

By default every placed copy of a furniture shows the text configured in its [Text-Entities](../mechanics/furniture-mechanic/text-entities.md).\
A `FurnitureTextOverride` lets your plugin decide the text per placed furniture instead, like a sign showing its owner.\
Return `null` to keep the configured text.

Overrides are checked in order of plugin name, and the first one returning a text wins.\
Pass a set of item-ids to only override those furniture.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
NexoFurniture.registerTextOverride(plugin, { entity ->
    if (entity.index == 0) Component.text(ownerName(entity.baseEntity)) else null
}, setOf("my_sign"))
```
{% endtab %}

{% tab title="Java" %}
```java
NexoFurniture.registerTextOverride(plugin, entity ->
    entity.getIndex() == 0 ? Component.text(ownerName(entity.getBaseEntity())) : null,
    Set.of("my_sign"));
```
{% endtab %}
{% endtabs %}

The text is cached per placed furniture and shared by every player viewing it.\
Call `NexoFurniture.refreshTextEntities(baseEntity)` when the text should change.\
Overrides are removed automatically when your plugin disables, or manually with `NexoFurniture.unregisterTextOverrides(plugin)`.

{% hint style="info" %}
`textFor` runs on the furniture's region thread
{% endhint %}

## Packs merged outside Nexo

Some models Nexo generates are based on models in the pack.\
If your plugin merges models into the pack after Nexo has generated it, Nexo cannot see them, and these have to be generated on your final pack instead.

```java
NexoFurniture.generatePreviewModels(resourcePack); // Faded models for furniture placement-previews
NexoBlocks.generateOffsetModels(resourcePack);     // Shifted models for custom block variants with an offset
```

`resourcePack` is a [creative](https://github.com/unnamed/creative) `ResourcePack`.

## Custom Mechanics

Nexo allows you to add your own mechanics to the plugin, new ones or extending existing ones\
An example repository can be found [here](https://github.com/Nexo-MC/NexoExampleMechanic), with examples for both Java and Kotlin\
You can register your mechanic in your onEnable or wherever you want.\
This will register it when Nexo registers its own Mechanics, and parse them for items\
\
Mechanics consist of a Mechanic class with properties and methods.\
MechanicFactory consists of parsing method for global Mechanic properties & linking item -> mechanic\
\
**NexoMechanicsRegisteredEvent** - Called when Nexo loads/reloads Mechanics\
**NexoItemsLoadedEvent** - Called when Nexo finishes loading/reloading NexoItems

#### Toggling lights

**NexoBlockInteractEvent** and **NexoFurnitureInteractEvent** have a `canToggleLight` result, which decides if the interaction toggles a toggleable [block light](../mechanics/custom-block-mechanics/custom-block-light.md) or [furniture light](../mechanics/furniture-mechanic/light-mechanic.md).\
Set it to `DENY` to stop the light from toggling without cancelling the interaction.

## Custom PackServer

If you want a PackServer type that Nexo does not provide, you can make an addon that registers one. Make a class that extends `NexoPackServer` and override the methods you need.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
class MyPackServer : NexoPackServer {
    override fun uploadPack(): CompletableFuture<Void>
    override fun sendPack(player: Player)
    override fun start()
    override fun stop()
    override fun packUrl(): String
    override fun packInfo(): ResourcePackInfo?
}
```
{% endtab %}

{% tab title="Java" %}
```java
public class PackServer extends NexoPackServer {
    @Override
    public CompletableFuture<Void> uploadPack()
    
    @Override
    public void sendPack(Player player)
    
    @Override
    public void start()
    
    @Override
    public void stop()
    
    @Override
    public String packUrl()
    
    @Override
    @Nullable
    public ResourcePackInfo packInfo()
}
```
{% endtab %}
{% endtabs %}

To register this with Nexo, you simply call `PackServerRegistry.register(type, packServer)`
