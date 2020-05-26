# Trims Based (1.20-1.21.1)

If using trims as your custom-armor type, most things is handled automatically for you.\
TRIMS method requires using CHAINMAIL as the base-item.

\
Nexo then generates a datapack based on your configured custom armors.\
Due to it requiring a datapack, the server needs to do a full restart any time you add/remove an armor-set.

{% hint style="danger" %}
After changing `CustomArmor.armor_type` to `TRIMS` you need to:

1. Start your server to let datapack be generated
2. Stop your server
3. Start it again to enable the previously generated datapack
{% endhint %}

## How to configure your armor?

{% hint style="info" %}
Make sure that the itemID of your NexoItem follows the pattern `armorname_armortype`.\
For the rest of the above set it would be `ruby_chestplate`, `ruby_leggings` and `ruby_boots`.

Make sure your armor-layer files follow the format of **armorname**\_armor\_layer\_1/2.png.\
In the example below, we would need a **ruby**\_armor\_layer\_1.png & **ruby**\_armor\_layer\_2.png
{% endhint %}

```yaml
ruby_helmet:
  displayname: "<gradient:#FA7CBB:#F14658>Ruby Helmet"
  material: CHAINMAIL_HELMET
  Pack:
    parent_model: "item/generated"
    # Optional, if not specified, Nexo searches for any texture
    # with the filename armorname_armor_layer_X.png
    #CustomArmor:
    #  layer1: default/armors/ruby_armor_layer_1.png
    #  layer2: default/armors/ruby_armor_layer_2.png
    texture: default/armors/ruby_helmet
```

A trim-pattern is also necessary for the armor to display correctly.\
Nexo will automatically assign it if it has not been manually specified.\
You can optionally manually assign the `trim_pattern` if you want to.\
The value should be `nexo:armorname`, so in our example;

```yaml
ruby_helmet:
  trim_pattern: nexo:ruby
```
