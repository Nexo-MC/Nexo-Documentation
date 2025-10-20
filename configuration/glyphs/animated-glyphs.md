# 🎞️ Animated Glyphs

With Nexo you can make Animated Glyphs, or GIFs, which you can use to animate GUIs or gif-emotes.\
It is very simple, Nexo does most of the hard work to convert the GIF-file to a compatible format.

Simply put your GIF-file in the resourcepack. As an example we will use `Nexo/pack/assets/nexo/textures/gifs/necoflap.gif`

### Gif-Glyph Config

```yaml
necoflap:
  gif: nexo:gifs/necoflap.gif
  ascent: 9
  height: 11
  #frame_count: X      Optional, mainly used for limiting larger GIFs
  #offset: X            Mainly if the GIF is not overlapping frames perfectly
```

Unlike normal Glyphs, font cannot be customized, as Nexo sets it for you.\
Texture-property is based on the `gif`-property and can be customized that way

{% hint style="info" %}
If you are unsure how to reference a Texture in a Glyph config[#how-do-i-reference-a-resourcepack-file-in-a-config](../../general-usage/faq.md#how-do-i-reference-a-resourcepack-file-in-a-config "mention")
{% endhint %}

{% hint style="warning" %}
GIFs rely on Core Shaders and might break on version updates.\
Large GIFs might also cause lag if the frame-count is really high, consider optimizing GIFs you intend to use
{% endhint %}

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTAoAxayP9PrBtX9UQ5wa%2Fuploads%2FnciiMhz3TRl476nq82Kp%2F2025-05-26%2015-31-12.mp4?alt=media&token=c563fad9-3620-4285-b3f5-753a9b410d19" %}
Example of GIFs in Chat & on Text Displays
{% endembed %}
