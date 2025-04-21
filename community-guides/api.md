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
    compileOnly("com.nexomc:nexo:1.1.0")
}
```

## Add Nexo-support to your plugin

### Repository & Dependency Info

You can find the repository and dependency notice here.

{% hint style="info" %}
All methods and better explanations of their functionality and parameters can be found in the actual Classes.\
Simply open them in your IDE to get a full list of them.
{% endhint %}

## Examples of use

Nexo is built around an ItemBuilder class that allows you to create items easily.\
When the plugin starts it parses the configurations to generate builders for each type of items.\
Each builder can be used to generate itemstacks.

### NexoItems class:

#### Get an ItemBuilder from a Nexo-ItemID

```java
NexoItems.itemFromId(itemID);
```

#### Get the Nexo-ItemID from an ItemStack

You can use to check if an ItemStack is an NexoItem (it will return null if the Nexo-ItemID doesn't exist)

```java
NexoItems.idFromItem(itemstack);
```

### Custom Blocks & Furniture

#### Place a NexoBlock

Place a NexoBlock at a given location

```java
NexoBlocks.place(itemID, location)
```

Place an NexoFurniture at a given location, optionally setting a player for rotation purposes

```java
NexoFurniture.place(itemID, location, @Nullable player)
```

### Mechanics:

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

### Custom PackServer

If you want a PackServer type that Nexo does not provide, you can make an addon that registers one. Make a class that extends `NexoPackServer` and override the methods you need.\
To register this with Nexo, you simply call `PackServerRegistry.register(type, packServer)`&#x20;

```kotlin
class MyPackServer : NexoPackServer {
    override fun uploadPack(): CompletableFuture<Void>
    override fun sendPack(player: Player)
    override fun start()
    override fun stop()
    override fun packUrl()
    override fun packInfo(): ResourcePackInfo?
}
```
