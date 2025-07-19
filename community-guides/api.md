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
The [NexoItems](https://jd.nexomc.com/1.8/com/nexomc/nexo/api/NexoItems.html)-class contains most of the methods you would need to handle items.

```java
ItemBuilder itemBuilder = NexoItems.itemFromId(itemID);
ItemStack itemStack = itemBuilder.build();
String itemId = NexoItems.idFromItem(itemStack);
```

{% hint style="info" %}
Nexo loads items in an async task, thus getting them in your plugins onEnable will likely fail\
You can listen for the NexoItemsLoadedEvent to be sure the items are registered
{% endhint %}

## Custom Blocks

The [NexoBlocks](https://jd.nexomc.com/1.8/com/nexomc/nexo/api/NexoBlocks.html)-class contains all the methods available for placing, removing and checking for custom blocks in Nexo.

```java
NexoBlocks.place(itemID, location)
```

### Furniture

The [NexoFurniture](https://jd.nexomc.com/1.8/com/nexomc/nexo/api/NexoFurniture.html)-class contains all the methods available for placing, removing and checking for furniture in Nexo. In addition to this you can return the [FurnitureMechanic](https://jd.nexomc.com/1.8/com/nexomc/nexo/mechanics/furniture/FurnitureMechanic.html) of the Furniture to get specific properties of it if needed.

```java
NexoFurniture.place(itemID, location, @Nullable player)
```

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

To register this with Nexo, you simply call `PackServerRegistry.register(type, packServer)`&#x20;
