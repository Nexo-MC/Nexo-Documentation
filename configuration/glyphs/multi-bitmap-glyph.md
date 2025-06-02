# 🖼️ Multi-Bitmap Glyph

If you have a texture consisting of several emotes or a texture larger than the allowed 256x256, you can make it a multi-bitmap.\
This means you can, tie several unicodes to one image.\
In your glyph you can specify an amount of rows and columns your glyph needs.\
This will make nexo assign unicodes based on your needs.

Example for using a 512x512 texture:

{% code lineNumbers="true" fullWidth="false" %}
```yaml
myglyph:
  #texture: required/ui/menu_items
  #ascent: 37
  #height: 256
  rows: 2     # Tells Nexo this glyph should have 2 rows when assigning unicodes/chars
  columns: 2  # Tells Nexo this glyph should have 2 columns when assigning unicodes/chars
```
{% endcode %}

This will make nexo assign 4 unicodes for this glyph, which will be displayed when used.

It should be noted that some cases newlines are not supported. An example is in lore, where it would not correctly align your glyph. A workaround is by using an "range index" in your glyph-tag. Example for using in lore of your NexoItem:

```yaml
myitem:
  lore:
    - "<glyph:myglyph:1..2>"
    - "<glyph:myglyph:3..4>"
```

This would correctly align your glyph in lore. In cases where newlines are supported, you dont need to specify such a range. Nexo would by default append that to the text and align it.
