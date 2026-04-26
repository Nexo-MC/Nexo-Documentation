# Components

As of Minecraft 1.20.6, items now use what is called Components, or DataComponents, to specify specific features. This covers anything from consumable items, tool-properties and death protection.\
Due to the nature of these they are very version-specific, so there are some differences and new additions between Minecraft version changes.

Each component below has a hover-click to show an example of how to use it, with additional info.

{% tabs %}
{% tab title="1.21.11" %}
[**Max Stack Size**](#user-content-fn-1)[^1] **-** Sets the maximum slot-size for the NexoItem\
[**Enchantment Glint Override**](#user-content-fn-2)[^2] - Sets an override-state for the enchantment glint\
[**Fire Resistant**](#user-content-fn-3)[^3] - Sets whether this NexoItem is immune to fire and lava\
[**Max Damage**](#user-content-fn-4)[^4] - Sets the maximum amount of damage the NexoItem can take\
[**Hide Tooltip**](#user-content-fn-5)[^5] - Hides all tooltips from the given NexoItem on hover\
[**Food**](#user-content-fn-6)[^6] - Makes this item consumable with several different properties\
[**Tool**](#user-content-fn-7)[^7] **-** Makes your item into a tool with configurable behaviour for blocks its breaking

[**Custom Data**](#user-content-fn-8)[^8] **-** Defines custom properties to add to the item\
[**Jukebox Playable**](#user-content-fn-9)[^9] - Lets this item be inserted into a Jukebox and play a given song

[**Consumable**](#user-content-fn-10)[^10] - Makes an item consumable, with bunch of sub-properties\
[**Equippable**](#user-content-fn-11)[^11] **-** Makes an item equippable, like armor\
[**Damage Resistant**](#user-content-fn-12)[^12] **-** Specify a damage-type this item is invulnerable to\
[**Enchantable**](#user-content-fn-13)[^13] **-** Set the maximum enchantment-cost for this item\
[**Glider**](#user-content-fn-14)[^14] **-** Allows the player to glide, like with elytras, when equipped\
[**Item Model** ](#user-content-fn-15)[^15]- Defines the base model-properties of this item\
[**Tooltip Style**](#user-content-fn-16)[^16] **-** Used to make custom tooltip-styles for your item\
[**Use Cooldown**](#user-content-fn-17)[^17] - Applies a cooldown to all matching items when used\
[**Use Remainder**](#user-content-fn-18)[^18] - Replaces the item with a remainder item if its stack count has decreased after use\
[**Repairable**](#user-content-fn-19)[^19] - What item(s) should be allowed in anvils to repair durability\
[**Death Protection**](#user-content-fn-20)[^20] - Protects the player from when equipped on death. Optionally applies effects too\
[**Player Profile**](#user-content-fn-21)[^21] - Specify profile-properties to show player-skins on item\
[**Unset Components**](#user-content-fn-22)[^22] - This lets you specify Components Nexo should remove from the item\
[**Custom Model Data**](#user-content-fn-23)[^23] - Used for all the new formatting for [1.21.4 CMD component](https://minecraft.wiki/w/Data_component_format#custom_model_data)

[**Tooltip Display**](#user-content-fn-24)[^24] - Sets the Components to hide tooltips from. This should be used instead of ItemFlags\
[**Break Sound**](#user-content-fn-25)[^25] - Set the sound to play when the item loses all its durability\
[**Weapon**](#user-content-fn-26)[^26] **-** Makes the item act like a weapon\
[**Blocks Attacks**](#user-content-fn-27)[^27] **-** Makes the item act as a shield & can block attacks\
[**CanPlaceOn/CanBreak**](#user-content-fn-28)[^28] **-** Defines what this item can break or be placed on in Adventure Mode

[**Painting Variant**](#user-content-fn-29)[^29] **-** Used with the new [custom-paintings.md](../custom-paintings.md "mention") feature to specify which painting to place

**New properties for 1.21.11+:**

[**Kinetic Weapon**](#user-content-fn-30)[^30] **-** Enables charge-type attack when using item\
[**Piercing Weapon**](#user-content-fn-31)[^31] **-** Actions done when weapon pierces target\
[**Attack Range**](#user-content-fn-32)[^32] **-** The range and hitbox margin of a weapon\
[**Swing Animation**](#user-content-fn-33)[^33] **-** The Animation to play when swinging item\
[**Use Effects**](#user-content-fn-34)[^34] **-** Vibration & player movement penalties when continuously using item\
[**Damage Type**](#user-content-fn-35)[^35] **-** The type of damage the item deals\
[**Minimum Attack Charge**](#user-content-fn-36)[^36] **-** Minimum attack-indicator value required to attack with item
{% endtab %}

{% tab title="1.21.8" %}
[**Max Stack Size**](#user-content-fn-1)[^1] **-** Sets the maximum slot-size for the NexoItem\
[**Enchantment Glint Override**](#user-content-fn-2)[^2] - Sets an override-state for the enchantment glint\
[**Fire Resistant**](#user-content-fn-3)[^3] - Sets whether this NexoItem is immune to fire and lava\
[**Max Damage**](#user-content-fn-4)[^4] - Sets the maximum amount of damage the NexoItem can take\
[**Hide Tooltip**](#user-content-fn-5)[^5] - Hides all tooltips from the given NexoItem on hover\
[**Food**](#user-content-fn-6)[^6] - Makes this item consumable with several different properties\
[**Tool**](#user-content-fn-7)[^7] **-** Makes your item into a tool with configurable behaviour for blocks its breaking

[**Custom Data**](#user-content-fn-8)[^8] **-** Defines custom properties to add to the item\
[**Jukebox Playable**](#user-content-fn-9)[^9] - Lets this item be inserted into a Jukebox and play a given song

[**Consumable**](#user-content-fn-10)[^10] - Makes an item consumable, with bunch of sub-properties\
[**Equippable**](#user-content-fn-11)[^11] **-** Makes an item equippable, like armor\
[**Damage Resistant**](#user-content-fn-12)[^12] **-** Specify a damage-type this item is invulnerable to\
[**Enchantable**](#user-content-fn-13)[^13] **-** Set the maximum enchantment-cost for this item\
[**Glider**](#user-content-fn-14)[^14] **-** Allows the player to glide, like with elytras, when equipped\
[**Item Model** ](#user-content-fn-15)[^15]- Defines the base model-properties of this item\
[**Tooltip Style**](#user-content-fn-16)[^16] **-** Used to make custom tooltip-styles for your item\
[**Use Cooldown**](#user-content-fn-17)[^17] - Applies a cooldown to all matching items when used\
[**Use Remainder**](#user-content-fn-18)[^18] - Replaces the item with a remainder item if its stack count has decreased after use\
[**Repairable**](#user-content-fn-19)[^19] - What item(s) should be allowed in anvils to repair durability\
[**Death Protection**](#user-content-fn-20)[^20] - Protects the player from when equipped on death. Optionally applies effects too\
[**Player Profile**](#user-content-fn-21)[^21] - Specify profile-properties to show player-skins on item\
[**Unset Components**](#user-content-fn-22)[^22] - This lets you specify Components Nexo should remove from the item\
[**Custom Model Data**](#user-content-fn-23)[^23] - Used for all the new formatting for [1.21.4 CMD component](https://minecraft.wiki/w/Data_component_format#custom_model_data)

[**Tooltip Display**](#user-content-fn-24)[^24] - Sets the Components to hide tooltips from. This should be used instead of ItemFlags\
[**Break Sound**](#user-content-fn-25)[^25] - Set the sound to play when the item loses all its durability\
[**Weapon**](#user-content-fn-26)[^26] **-** Makes the item act like a weapon\
[**Blocks Attacks**](#user-content-fn-27)[^27] **-** Makes the item act as a shield & can block attacks\
[**CanPlaceOn/CanBreak**](#user-content-fn-28)[^28] **-** Defines what this item can break or be placed on in Adventure Mode

**New properties for 1.21.8+:**

[**Painting Variant**](#user-content-fn-29)[^29] **-** Used with the new [custom-paintings.md](../custom-paintings.md "mention") feature to specify which painting to place
{% endtab %}

{% tab title="1.21.5" %}
[**Max Stack Size**](#user-content-fn-1)[^1] **-** Sets the maximum slot-size for the NexoItem\
[**Enchantment Glint Override**](#user-content-fn-2)[^2] - Sets an override-state for the enchantment glint\
[**Fire Resistant**](#user-content-fn-3)[^3] - Sets whether this NexoItem is immune to fire and lava\
[**Max Damage**](#user-content-fn-4)[^4] - Sets the maximum amount of damage the NexoItem can take\
[**Hide Tooltip**](#user-content-fn-5)[^5] - Hides all tooltips from the given NexoItem on hover\
[**Food**](#user-content-fn-6)[^6] - Makes this item consumable with several different properties\
[**Tool**](#user-content-fn-7)[^7] **-** Makes your item into a tool with configurable behaviour for blocks its breaking

[**Custom Data**](#user-content-fn-8)[^8] **-** Defines custom properties to add to the item\
[**Jukebox Playable**](#user-content-fn-9)[^9] - Lets this item be inserted into a Jukebox and play a given song

[**Consumable**](#user-content-fn-10)[^10] - Makes an item consumable, with bunch of sub-properties\
[**Equippable**](#user-content-fn-11)[^11] **-** Makes an item equippable, like armor\
[**Damage Resistant**](#user-content-fn-12)[^12] **-** Specify a damage-type this item is invulnerable to\
[**Enchantable**](#user-content-fn-13)[^13] **-** Set the maximum enchantment-cost for this item\
[**Glider**](#user-content-fn-14)[^14] **-** Allows the player to glide, like with elytras, when equipped\
[**Item Model** ](#user-content-fn-15)[^15]- Defines the base model-properties of this item\
[**Tooltip Style**](#user-content-fn-16)[^16] **-** Used to make custom tooltip-styles for your item\
[**Use Cooldown**](#user-content-fn-17)[^17] - Applies a cooldown to all matching items when used\
[**Use Remainder**](#user-content-fn-18)[^18] - Replaces the item with a remainder item if its stack count has decreased after use\
[**Repairable**](#user-content-fn-19)[^19] - What item(s) should be allowed in anvils to repair durability\
[**Death Protection**](#user-content-fn-20)[^20] - Protects the player from when equipped on death. Optionally applies effects too\
[**Player Profile**](#user-content-fn-21)[^21] - Specify profile-properties to show player-skins on item\
[**Unset Components**](#user-content-fn-22)[^22] - This lets you specify Components Nexo should remove from the item\
[**Custom Model Data**](#user-content-fn-23)[^23] - Used for all the new formatting for [1.21.4 CMD component](https://minecraft.wiki/w/Data_component_format#custom_model_data)

**New properties for 1.21.5+:**

[**Tooltip Display**](#user-content-fn-24)[^24] - Sets the Components to hide tooltips from. This should be used instead of ItemFlags\
[**Break Sound**](#user-content-fn-25)[^25] - Set the sound to play when the item loses all its durability\
[**Weapon**](#user-content-fn-26)[^26] **-** Makes the item act like a weapon\
[**Blocks Attacks**](#user-content-fn-27)[^27] **-** Makes the item act as a shield & can block attacks\
[**CanPlaceOn/CanBreak**](#user-content-fn-28)[^28] **-** Defines what this item can break or be placed on in Adventure Mode
{% endtab %}

{% tab title="1.21.4" %}
[**Max Stack Size**](#user-content-fn-1)[^1] **-** Sets the maximum slot-size for the NexoItem\
[**Enchantment Glint Override**](#user-content-fn-2)[^2] - Sets an override-state for the enchantment glint\
[**Fire Resistant**](#user-content-fn-3)[^3] - Sets whether this NexoItem is immune to fire and lava\
[**Max Damage**](#user-content-fn-4)[^4] - Sets the maximum amount of damage the NexoItem can take\
[**Hide Tooltip**](#user-content-fn-5)[^5] - Hides all tooltips from the given NexoItem on hover\
[**Food**](#user-content-fn-6)[^6] - Makes this item consumable with several different properties\
[**Tool**](#user-content-fn-7)[^7] **-** Makes your item into a tool with configurable behaviour for blocks its breaking

[**Custom Data**](#user-content-fn-8)[^8] **-** Defines custom properties to add to the item\
[**Jukebox Playable**](#user-content-fn-37)[^37] - Lets this item be inserted into a Jukebox and play a given song

[**Consumable**](#user-content-fn-10)[^10] - Makes an item consumable, with bunch of sub-properties\
[**Equippable**](#user-content-fn-11)[^11] **-** Makes an item equippable, like armor\
[**Damage Resistant**](#user-content-fn-12)[^12] **-** Specify a damage-type this item is invulnerable to\
[**Enchantable**](#user-content-fn-13)[^13] **-** Set the maximum enchantment-cost for this item\
[**Glider**](#user-content-fn-14)[^14] **-** Allows the player to glide, like with elytras, when equipped\
[**Item Model** ](#user-content-fn-15)[^15]- Defines the base model-properties of this item\
[**Tooltip Style**](#user-content-fn-16)[^16] **-** Used to make custom tooltip-styles for your item\
[**Use Cooldown**](#user-content-fn-17)[^17] - Applies a cooldown to all matching items when used\
[**Use Remainder**](#user-content-fn-18)[^18] - Replaces the item with a remainder item if its stack count has decreased after use\
[**Repairable**](#user-content-fn-19)[^19] - What item(s) should be allowed in anvils to repair durability\
[**Death Protection**](#user-content-fn-20)[^20] - Protects the player from when equipped on death. Optionally applies effects too\
[**Player Profile**](#user-content-fn-21)[^21] - Specify profile-properties to show player-skins on item\
[**Unset Components**](#user-content-fn-22)[^22] - This lets you specify Components Nexo should remove from the item

**New properties for 1.21.4+:**\
[**Custom Model Data**](#user-content-fn-23)[^23] - Used for all the new formatting for [1.21.4 CMD component](https://minecraft.wiki/w/Data_component_format#custom_model_data)
{% endtab %}

{% tab title="1.21.3" %}
[**Max Stack Size**](#user-content-fn-1)[^1] **-** Sets the maximum slot-size for the NexoItem\
[**Enchantment Glint Override**](#user-content-fn-2)[^2] - Sets an override-state for the enchantment glint\
[**Fire Resistant**](#user-content-fn-3)[^3] - Sets whether this NexoItem is immune to fire and lava\
[**Max Damage**](#user-content-fn-4)[^4] - Sets the maximum amount of damage the NexoItem can take\
[**Hide Tooltip**](#user-content-fn-5)[^5] - Hides all tooltips from the given NexoItem on hover\
[**Food**](#user-content-fn-6)[^6] - Makes this item consumable with several different properties\
[**Tool**](#user-content-fn-7)[^7] **-** Makes your item into a tool with configurable behaviour for blocks its breaking

[**Custom Data**](#user-content-fn-8)[^8] **-** Defines custom properties to add to the item\
[**Jukebox Playable**](#user-content-fn-37)[^37] - Lets this item be inserted into a Jukebox and play a given song

**New properties for 1.21.3+:**

[**Consumable**](#user-content-fn-10)[^10] - Makes an item consumable, with bunch of sub-properties\
[**Equippable**](#user-content-fn-11)[^11] **-** Makes an item equippable, like armor\
[**Damage Resistant**](#user-content-fn-12)[^12] **-** Specify a damage-type this item is invulnerable to\
[**Enchantable**](#user-content-fn-13)[^13] **-** Set the maximum enchantment-cost for this item\
[**Glider**](#user-content-fn-14)[^14] **-** Allows the player to glide, like with elytras, when equipped\
[**Item Model** ](#user-content-fn-15)[^15]- Defines the base model-properties of this item\
[**Tooltip Style**](#user-content-fn-16)[^16] **-** Used to make custom tooltip-styles for your item\
[**Use Cooldown**](#user-content-fn-17)[^17] - Applies a cooldown to all matching items when used\
[**Use Remainder**](#user-content-fn-18)[^18] - Replaces the item with a remainder item if its stack count has decreased after use\
[**Repairable**](#user-content-fn-19)[^19] - What item(s) should be allowed in anvils to repair durability\
[**Death Protection**](#user-content-fn-20)[^20] - Protects the player from when equipped on death. Optionally applies effects too\
[**Player Profile**](#user-content-fn-21)[^21] - Specify profile-properties to show player-skins on item\
[**Unset Components**](#user-content-fn-22)[^22] - This lets you specify Components Nexo should remove from the item
{% endtab %}

{% tab title="1.21.1" %}
[**Max Stack Size**](#user-content-fn-1)[^1] **-** Sets the maximum slot-size for the NexoItem\
[**Enchantment Glint Override**](#user-content-fn-2)[^2] - Sets an override-state for the enchantment glint\
[**Fire Resistant**](#user-content-fn-3)[^3] - Sets whether this NexoItem is immune to fire and lava\
[**Max Damage**](#user-content-fn-4)[^4] - Sets the maximum amount of damage the NexoItem can take\
[**Hide Tooltip**](#user-content-fn-5)[^5] - Hides all tooltips from the given NexoItem on hover\
[**Food**](#user-content-fn-38)[^38] - Makes this item consumable with several different properties\
[**Tool**](#user-content-fn-7)[^7] **-** Makes your item into a tool with configurable behaviour for blocks its breaking

**New properties for 1.21.1+:**

[**Custom Data**](#user-content-fn-8)[^8] **-** Defines custom properties to add to the item\
[**Jukebox Playable**](#user-content-fn-37)[^37] - Lets this item be inserted into a Jukebox and play a given song
{% endtab %}
{% endtabs %}

[^1]: ```yaml
    my_item:
      Components:
        max_stack_size: 64
    ```

    The number must be between 1 & 99

[^2]: ```yaml
    my_item:
      Components:
        enchantment_glint_override: true
    ```

[^3]: ```yaml
    my_item:
      Components:
        fire_resistant: true
    ```

[^4]: ```yaml
    my_item:
      Components:
        max_damage: 100
    ```

    Max Damage/Durability can be any value above 0

[^5]: ```yaml
    my_item:
      Components:
        hide_tooltip: true
    ```

[^6]: ```yaml
    my_item:
      Components:
        food:
          nutrition: 2
          saturation: 2 
          can_always_eat: false
                      
    ```

    **can\_always\_eat -** Defaults to false if unspecified\
    **eat\_seconds -** Defaults to 1.6 if unspecified

[^7]: ```yaml
    my_item:
      Components:
        tool:
          damage_per_block:
          default_mining_speed:
          rules:
            - speed: 1.0
              correct_for_drops: true
              material: DIAMOND_BLOCK
              #materials:
              #  - DIAMOND_BLOCK
              #  - NETHERITE_BLOCK
              tag: minecraft:mineable/axe
              #tags:
              #  - minecraft:mineable/axe
              #  - minecraft:mineable/shovel
    ```

    **damage\_per\_block:**\
    The amount of damage to apply to the tool per block broken. Defaults to 1\
    \
    **default\_mining\_speed:**

    The default speed of this tool, excluding modifiers in rules. Defaults to 1.0\
    \
    **Rules:**\
    Rules are behaviour for specific blocks.\
    You can set the speed, if the tool is correct and the block should drop its drop, etc\
    \
    **Tags:**\
    List of all tags can be found [here](https://minecraft.wiki/w/Tag#Block_tags_2)

[^8]: ```yaml
    my_item:
      Components:
        custom_data:
          nexo:string: "Some string"
          nexo:integer: 2
          nexi:integer_list: [1, 2, 3]
          nexo:string_list:
            - "something"
            - "something else"
          nexo:compound:
            nexo:c_string: "String"
            nexo:c_integer: 3
            namespace:boolean: true
    ```

    This is data that is added into the "root" of the CustomData on the Item.\
    It is one step outside what PersistentData is

[^9]: ```yaml
    my_item:
      Components:
        jukebox_playable:
          song_key: namespace:key
    ```

    This component lets you mark an item as a "Music Disc". It can then be inserted into a jukebox to play a given sound.\
    \
    The sound is the key defined in either your sounds.json in your ResourcePack, or in Nexo's sounds.yml

[^10]: ```yaml
    my_item:
      Components:
        consumable:
          sound: minecraft:entity.generic.eat     # Optional, default is entity.generic.eat
          consume_particles: true                 # Optional, default is true
          consume_seconds: 1.6                    # Optional, default is 1.6
          animation: EAT                          # Optional, default is EAT
          effects:
            APPLY_EFFECTS:
              mining_fatigue:
                duration: 10
                amplifier: 1
                ambient: false
                show_icon: true
                show_particles: true
                probability: 1.0
            REMOVE_EFFECTS:
            - speed
            CLEAR_ALL_EFFECTS: {}
            TELEPORT_RANDOMLY:
              diameter: 16.0
            PLAY_SOUND:
              sound: minecraft:ambient.basalt_deltas.additions1
    ```

[^11]: ```yaml
    my_item:
      Components:
        equippable:
          slot: HEAD
          #asset_id: minecraft:example
          #camera_overlay: minecraft:example
          #equip_sound: item.armor.equip_chain
          #allowed_entity_types:
          #  - PLAYER
          #  - SKELETON
          #dispensable: true
          #swappable: true
          #damage_on_hurt: true
    ```

    [**Minecraft Wiki**](https://minecraft.wiki/w/Data_component_format#equippable)\
    \
    **Asset ID:**

    The asset to show for the equipped texture.\
    If using a 3D Model for helmet, do not specify this field

    **Camera Overlay:**

    The resource-overlay to show on screen whilst equipped.\
    This field is optional

    **Equip Sound:**

    The sound to play when equipped.\
    Defaults to `item.armor.equip_generic`

    **Allowed Entity Types:**

    A list of all types can be found [here](https://jd.papermc.io/paper/1.21.8/org/bukkit/entity/EntityType.html)\
    If unspecified, defaults to all entities

[^12]: ```yaml
    my_item:
      Components:
        damage_resistant: is_fire
    ```

    This specifies the DamageType the item is invulnerable to.\
    If you want a custom DamageType which the vanilla ones do not cover, you will need to add it via a custom Datapack\
    \
    A list of all DamageTypes can be found [here](https://minecraft.wiki/w/Damage_type_tag_\(Java_Edition\))

[^13]: ```yaml
    my_item:
      Components:
        enchantable: 15
    ```

    This specifies the maximum Enchantment Cost for this item.\
    Setting this to 0 will prevent the item from being enchantable

[^14]: ```yaml
    my_item:
      Components:
        glider: true
    ```

    This component is best used together with Equippable

[^15]: ```yaml
    my_item:
      Components:
        item_model: namespace:key
    ```

    This defines the base model of an item.\
    By default it will use `minecraft:type`\
    For PAPER this would be `minecraft:paper`\
    \
    It is heavily recommended to use a custom ItemModel instead of CustomModelData when possible\
    \
    With an ItemModel you do not need CustomModelData as you alter the base-model of your item\
    \
    Nexo will make this for you if you manually set this property in your item, and do not have CustomModelData specified, or you have enabled `Pack.generation.prefer_item_models` in `settings.yml`

[^16]: ```yaml
    my_item:
      Components:
        tooltip_style: namespace:key
    ```

    [**Minecraft Wiki**](https://minecraft.wiki/w/Data_component_format#tooltip_style)

    A Tooltip Style refers to a set of textures in your ResourcePack.\
    It is made up of a **background** and **frame** texture, with an optional mcmeta file for each\
    \
    It can also be customized & animated using [MCMeta](https://minecraft.wiki/w/Resource_pack#Animation#Gui)\
    \
    The config property refers to this path in your ResourcePack:\
    `assets/NAMESPACE/textures/gui/sprites/tooltip/KEY_frame`\
    `assets/NAMESPACE/textures/gui/sprites/tooltip/KEY_background`

[^17]: ```yaml
    my_item:
      Components:
        use_cooldown:
          seconds: 1.2
          group: nexo:example
    ```

    This component triggers the cooldown feature for this Item, similar to using an Ender Pearl in vanilla.\
    \
    **Seconds:**\
    The time in seconds the cooldown should last. Defaults to 1.0\
    \
    **Group (Optional):**\
    This can be used to apply the cooldown on all instances of an item & even other items with the same group

[^18]: ```yaml
    my_item:
      Components:
        use_remainder:
          #minecraft_type: DIAMOND
          #crucible_item: crucibleid
          #mmoitems_id: id
          #mmoitems_type: type
          nexo_item: itemid
    ```

[^19]: ```yaml
    my_item:
      Components:
        repairable: minecraft:planks
        #repairable:
        # - minecraft:diamond
    ```

    This defines the items that can be used to repair this NexoItem.\
    It only supports vanilla Materials, not Custom Items.\
    \
    It supports both tags and individual materials, like shown above.\
    Can be a single entry or a list of entries

[^20]: ```yaml
    my_item:
      Components:
        death_protection:
          death_effects:                      #Optional, can be empty/set to []
            APPLY_EFFECTS:
              mining_fatigue:
                duration: 10
                amplifier: 1
                ambient: false
                show_icon: true
                show_particles: true
                probability: 1.0
              REMOVE_EFFECTS:
              - speed
              CLEAR_ALL_EFFECTS: {}
              TELEPORT_RANDOMLY:
                diameter: 16.0
              PLAY_SOUND:
                sound: minecraft:ambient.basalt_deltas.additions
    ```

[^21]: ```yaml
    myitem:
      material: PLAYER_HEAD
      Components:
        profile:
          name: boy0000
          uuid: 1234
          properties:
            name: name
            value: value
            signature: signature
    ```

    The component can be applied to any item, but only has a visible effect for those with PLAYER\_HEAD material.

    In the profile component itself, you have to specify either **name, uuid** or **properties,** not all.\
    Properties is mostly for referencing skins from databases etc which might not be entirely linked to a player anymore.\
    In properties, name and value are required, but signature is optional

[^22]: ```yaml
    myitem:
      material: DIAMOND_PICKAXE
      Components:
        unset_components:
          - minecraft:tool
    ```

[^23]: ```yaml
    my_item:
      Components:
        custom_model_data:
          #floats: [ 1f, 2f, ...]            #Optional, same logic as with CMD before
          #colors: [ 1, 123456, [r, g, b]]
          #string: [ "something", "somethingelse", ...]
          #flags: []
    ```

    [**Minecraft Wiki**](https://minecraft.wiki/w/Data_component_format#custom_model_data)

[^24]: ```
    my_item:
      Components:
        tooltip_display:
          - minecraft:dyed_color
          - minecraft:enchantments
          - minecraft:attribute_modifiers
    ```

    This component is used to replace the old `show_in_tooltip` -property for individual components.\
    A list of components can be found [here](https://minecraft.wiki/w/Data_component_format#List_of_components)\
    \
    If `hide_tooltip`-component is set to true, this is ignored

[^25]: ```yaml
    my_item:
      Components:
        break_sound: namespace:key
    ```

[^26]: ```yaml
    my_item:
      Components:
        weapon:
         damage_per_attack: 1
         disable_blocking: 0.0
    ```

[^27]: ```yaml
    my_item:
      Components:
        blocks_attacks:
          block_delay: 0.0
          disable_cooldown_scale: 1.0
          block_sound: namespace:key
          disable_sound: namespace:key
          bypassed_by: namespace:key
          item_damage:
            base: 1.0
            factor:1.0
            threshold: 0.0
          damage_reductions:
            - base: 1.0
              factor: 1.0
              horizontal_blocking: 90.0
              types: namespace:key
              #types:
              #  - namespace:key
    ```

    **Damage Reductions:**

    **types** can be specified as a single element or a list, and takes a NamespacedKey for a DamageType or Tag

[^28]: ```yaml
    my_item:
      Components:
        can_place_on/can_break:
          block: stone
          blocks:
            - stone
            - ores
    ```

    This supports all block-ids or block-tags.\
    Can either specify a single element or a list of elements

[^29]: ```yaml
    my_item:
      Components:
        painting_variant: namespace:key
    ```

[^30]: ```yaml
    my_item:
      Components:
        kinetic_weapon:
          contact_cooldown: 10t
          delay: 0t
          damage_multiplier: 1.0
          sound: namespace:key
          hit_sound: namespace:key
          dismount_conditions:
            max_duration: 0t
            min_speed: 0f
            min_relative_speed: 0f
          knockback_conditions:
            max_duration: 0t
            min_speed: 0f
            min_relative_speed: 0f
          damage_conditions:
            max_duration: 0t
            min_speed: 0f
            min_relative_speed: 0f
                  
    ```

[^31]: ```yaml
    my_item:
      Components:
        piercing_weapon:
          sound: namespace:key
          hit_sound: namespace:key
          dismounts: false
          deals_knockback: true
    ```

[^32]: ```yaml
    my_item:
      Components:
        attack_range:
          reach: 0..64
          #min_reach: 0
          #max_read: 64
          hitbox_margin: 0.3
          mob_factor: 1
    ```

[^33]: ```yaml
    my_item:
      Components:
        swing_animation:
          type: WHACK
          duration: 6t
    ```

    Available animations found [here](https://jd.papermc.io/paper/io/papermc/paper/datacomponent/item/SwingAnimation.html)

[^34]: ```yaml
    my_item:
      Components:
        use_effects:
          can_sprint: false
          interact_vibrations: true
          speed_multiplier: 0.2
    ```

[^35]: ```yaml
    my_item:
      Components:
        damage_type: piercing
    ```

[^36]: ```yaml
    my_item:
      Components:
        minimum_attack_charge: 1f
    ```

[^37]: ```yaml
    my_item:
      Components:
        jukebox_playable:
          show_in_tooltip: true
          song_key: namespace:key
    ```

    This component lets you mark an item as a "Music Disc". It can then be inserted into a jukebox to play a given sound.\
    \
    The sound is the key defined in either your sounds.json in your ResourcePack, or in Nexo's sounds.yml

[^38]: ```yaml
    my_item:
      Components:
        food:
          nutrition: 2
          saturation: 2 
          can_always_eat: false
          eat_seconds: 1.6
          replacement:
            #minecraft_type: DIAMOND
            #crucible_item: crucibleid
            #eco_item: ecoid
            #mmoitems_id: id
            #mmoitems_type: type
            nexo_item: itemid
          effects:
            mining_fatigue:
              duration: 10
              amplifier: 1
              ambient: false
              show_icon: true
              show_particles: true
              probability: 0.5
    ```

    **can\_always\_eat -** Defaults to false if unspecified\
    **eat\_seconds -** Defaults to 1.6 if unspecified
