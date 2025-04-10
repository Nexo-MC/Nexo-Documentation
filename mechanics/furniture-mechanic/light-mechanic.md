# 💡 Light Mechanic

Using the Light-Mechanic you can configure your furniture to emits light. \
It takes an **offset** from the base-furniture and a **light-level** between 1 & 15\
Light can also be made toggleable by adding `toggleable: true`, meaning right-clicking the furniture will toggle the light on/off.\
Using `toggled_model` you can provide a NexoItem to display when the furniture-light is toggled on\
Likewise, `toggled_item_model` lets you provide an ItemModel directly without a NexoItem to display when toggled on. Note; this is for 1.21.2+ servers only

```yaml
myitem:
  Mechanics:
    furniture:
      lights:
        #toggleable: false                    # Default is false
        #toggled_model: some_nexo_item        # The NexoItem to show when light is on
        #toggled_item_model: namespace:model  # The ItemModel to use when light is on  
        lights:
          - 0,0,0 15    # x,y,z lightLevel
```

<div><figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Table Lamp included in Nexo Default Items (off)</p></figcaption></figure> <figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Table Lamp included in Nexo Default Items (on)</p></figcaption></figure></div>
