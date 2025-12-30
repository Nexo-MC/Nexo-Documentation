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

# 📦 Custom Block Mechanics

Nexo has several options for making Custom Blocks.\
They all come with a few restrictions due to the nature of how custom blocks can be implemented.\
NOTEBLOCK type custom blocks are for normal 1x1x1 blocks like Stone, Dirt etc...\
It uses the vanilla NoteBlock and thus disables most of the redstone functionality for it\
\
CHORUSBLOCK type custom blocks are based on the Chorus Plant block.\
It is mainly used for transparent blocks, like leaves.\
The hitbox is not a normal 1x1x1 so it is adviced to only use this for transparent block needs\
\
STRINGBLOCK type custom blocks are for plants, decoration etc...\
It uses the vanilla TripWire block and thus disables most of the redstone functionality for it

{% hint style="danger" %}
On all Paper-Servers you are HEAVILY recommended to disable block-updates for the types of custom blocks you plan to use.\
These can be found in \`MyServerFolder/configs/paper-global.yml\`
{% endhint %}

{% hint style="warning" %}
Due to the nature of Custom Blocks, these for the most part completely disable the original blocks vanilla functionality.\
NOTEBLOCK-type does have an option to "reimplement" the functionality, but it has some minor flaws.\
STRINGBLOCK-type completely disables vanilla functionality.\
If you want either of these, you will likely have to disable these mechanics.
{% endhint %}
