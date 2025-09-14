---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# ItemModels vs. CustomModelData

### What is an ItemModel?

In 1.21.4, Mojang added a feature to specify the ItemModel of an item.\
In short an ItemModel is the **base model** of an item, which decides when to show what.\
\
ResourcePacks can be split into a few different types of files:\
ItemModels - Tells the client when to show what for an item\
Models - All the visual data of an item, cubes, uv-mappings etc\
Textures - The textures used by Models and other files

An ItemModel in short just says "when X condition is satisfied, show this Model to the player"\
By default an item using PAPER as its material will use the vanilla ItemModel **minecraft:paper**\
When an item uses CustomModelData it then adds a custom entry into this vanilla ItemModel that says;\
"When an item with this ItemModel has the CustomModelData X, show this Model".

This is the ways custom items have been done ever since it was introduced, as there was no better way.\
It works fine in most cases but can cause some issues and conflicts when merging a lot of files together.

Now we can change the base ItemModel itself, and not rely on overriding the vanilla one.\
For servers which only support 1.21.4+ clients, this is the ideal way to handle it.\
It will cause no conflicts, open up for more customizability and stability, and is the intended way to do custom models.

### How do iI start using custom ItemModels?

Nexo makes the process of swapping away from CustomModelData to ItemModels very easy.\
1\. Ensure you take a backup of your `Nexo/items` - folder\
2\. Go into `Nexo/settings.yml` and set `Pack.generation.prefer_item_models: true`\
3\. Go into your server and run the command `/nexo reset_custom_model_data`\
4\. Run the command `/nexo reload`&#x20;

And that is it, your NexoItems should now all be swapped to their own custom ItemModel\


```yaml
myitem:
  Pack:
    model: mymodel
  Components:
    item_model: nexo:mymodel
```

This ItemModel can be used on any item with any material in any plugin (that supports ItemModels) and will never conflict

### When should I not use a custom ItemModel?

The only real time you should not use a custom ItemModel over CustomModelData is if your server tries to support clients older than 1.21.4. There is also some downsides when you have plugins which are still to allow such new features, and rely exclusively on CustomModelData for its features

