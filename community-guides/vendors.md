---
description: Guide for vendors and others wanting to make Third-Party packs for Nexo
---

# Vendors

Below is the recommended way to add content to Nexo in a "drag & drop" format\
For these examples I will make it as a store named "NexoMC"

### ResourcePack

For including a ResourcePack, the ideal way is to use an "External Pack"\
Nexo allows for merging multiple full resourcepacks, so to avoid conflicts, it is the best approach\
Using proper namespaces is also ideal, not stuffing everything into the default minecraft-namespace\
`Nexo/pack/external_packs/NexoMC/assets/nexomc/models/item/some_model.json`\
This allows you to minimize possible conflicts with other packs and items others might have made

```
📁Nexo
└── 📁pack
    └── 📁external_packs
        ├── 📁RequiredPack.zip         #Nexo Default
        ├── 📁DefaultPack.zip          #Nexo Default
        └── 📁NexoMC
            └── 📁assets
                └── 📁nexomc
                    ├── 📁models
                    |   └── ...
                    └── 📁textures
                        └── ...
```

### Items

Nexo also improves the structuring of items abit by allowing subfolders inside `Nexo/items`\
This means the recommended way to add premade itemconfigs is the following `Nexo/items/NexoMC/nexo_christmas_furniture.yml`

```
📁Nexo
└── 📁items
    └── 📁NexoMC
        ├── 📄 christmas_furniture.yml
        └── 📄 easter_armor.yml
```

\
There are also some config-changes compared to Oraxen, mainly to [Furniture](../mechanics/furniture-mechanic/) & [Custom-Block](../mechanics/custom-block-mechanics/) mechanics.\
🟨`itemid.Mechanics.furniture.display_entity_properties` -> `itemid.Mechanics.furniture.properties`\
`🟨itemid.displayname` -> `itemid.itemname`\
🟨`itemid.customname` to use old "DisplayName" logic from 1.20.4<\
🟨 Furniture Hitbox-structure has changed, refer to [docs](../mechanics/furniture-mechanic/#hitboxes)\
🟨 Custom-Blocks has changed, refer to [NoteBlock](../mechanics/custom-block-mechanics/noteblock-mechanic/)/[StringBlock](../mechanics/custom-block-mechanics/stringblock-mechanic.md)\
❌ `itemid.Mechanics.furniture.type` Nexo only supports Display-Entities\
❌ `itemid.Pack.generate_model` is determined automatically\
✔️ `itemid.Components.item_model` can be used on 1.21.2+ to avoid entire `itemid.Pack` \
✔️ `itemid.Pack.texture` can be used if you only have a single texture\
✔️ `itemid.Pack.textures` accepts a single texture, a list of textures or a map of texture-key to texture

### Glyphs

There are no big changes to glyphs, but it allows for multiple namespaces now\
Same as with resourcepacks, you should use a separate namespace where you can

```yaml
santa_claus:
  texture: nexomc:santa_claus
  font: nexomc:christmas_glyphs
  ...
```

