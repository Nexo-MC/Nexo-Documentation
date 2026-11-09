# 📋 Glyph Templates

Glyph templates let you share properties between glyphs, like the [ItemTemplate](../items/README.md#itemtemplate) does for items.\
Point a glyph at another glyph with `template`, and it copies every property of it that the glyph does not set itself.

```yaml
icon_base:
  ascent: 8
  height: 8
  font: nexo:icons
  is_emoji: true

heart:
  template: icon_base
  texture: default/chat/heart

star:
  template: icon_base
  texture: default/chat/star
  ascent: 7    # Overrides the template
```

A glyph used as a template is only a template, and is not loaded as a glyph of its own.\
It therefore does not need a `texture`.

## Multiple Templates

`template` also takes a list, and `templates` works as well.\
They are applied in order, so a later template overrides an earlier one, and the glyph's own properties override them all.\
Templates can also use templates of their own.

```yaml
icon_base:
  ascent: 8
  height: 8

emoji_base:
  font: nexo:emojis
  is_emoji: true
  tabcomplete: true

heart:
  templates:
    - icon_base
    - emoji_base
  texture: default/chat/heart
```

Templates can be defined in any file in the glyphs folder, not just the one using them.

{% hint style="info" %}
`char` is never copied from a template, every glyph gets its own.\
If unspecified, Nexo assigns one and saves it into the glyph's config
{% endhint %}

{% hint style="warning" %}
`placeholders` are copied like any other property, so every glyph using that template would share them.\
Put `placeholders` on the glyphs themselves rather than on the template
{% endhint %}
