# 🔗 Reference Glyph

Reference-glyphs are used when you want to "reference" a part of a Multi-Bitmap Glyph.\
For example if you have a multi-bitmap glyph with 10 emojis, you can reference a specific one like follows

```yaml
multi_bitmap:
  texture: spritesheet
  rows: 2
  columns 5

#index is the row and column number
first_emoji:
  reference: multi_bitmap
  index: 1
...
tenth_emoji:
  reference: multi_bitmap
  index: 10
```
