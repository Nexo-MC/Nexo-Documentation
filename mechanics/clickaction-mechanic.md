---
description: >-
  Run commands, play sounds, or send messages when a player clicks a block or
  furniture.
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825489098489856/unknown.png
coverY: 0
---

# ClickAction Mechanic

To get started, create a basic [Custom Block](custom-block-mechanics/noteblock-mechanic/) or [Furniture](furniture-mechanic/).

Next, under the mechanics section, you can add the default clickAction mechanic under any\
CustomBlock or Furniture-Mechanic

```yaml
myitem:
  Mechanics:      
    furniture/custom_block:
      clickActions:
        - conditions:
            - '#player.hasPermission("test.permission")'
          actions:
            - '[console] say <player> hello <player>!'
```

With this setup, players will only trigger the console command `say hello <player>` action if they have the permission `test.permission`.

If you are not using conditions, you need to place brackets where they would be:

```yaml
myitem:
  Mechanics:
    furniture/custom_block:
      clickActions:
        - conditions: []
          actions:
            - '[console] say <player> hello <player>!'
```

### Conditions

Conditions are VERY configurable. You can use any of the "get" methods for Player or Server.\
A list of all methods you can use can be found on Papers Javadocs

{% embed url="https://jd.papermc.io/paper/1.21.8/org/bukkit/entity/Player.html" %}

{% embed url="https://jd.papermc.io/paper/1.21.8/org/bukkit/Server.html" %}
TIP! Click "CTRL + F" and search "get" to find valid methods.
{% endembed %}

Additionally, the Spring Documentation is a good resource for understanding how to use condition expressions.

{% embed url="https://docs.spring.io/spring-framework/docs/3.0.x/reference/expressions.html" %}

You can also do a negative check by prefixing the condition with `!` . as an example;

```yaml
myitem:
  Mechanics:      
    furniture/custom_block:
      clickActions:
        - conditions:
            - '!#player.hasPermission("test.permission")'
          actions:
            - '[console] say <player> hello <player>!'
```

This will run the action when the player does not have the **test.permission** permission.

#### Condition Examples

`#server.getOnlinePlayers().size() > 10`

`#server.getAllowEnd()`

`#server.getDefaultGameMode()`

`#player.world.name == 'world'`

`#player.hasPermission("test.permission")`

`#player.gamemode.name() == 'ADVENTURE'`

### Actions

`[console] <command>`

`[player] <command>`

`[message] <message>`

`[actionbar] <message>`

`{source=SOURCE volume=VOLUME pitch=PITCH} [sound] <sound name>`

#### Action Examples

`[console] say hello`

`[player] say hello`

`[message] <blue>Hello!`

`[actionbar] <gray>Hello from the actionbar!`

`{source=AMBIENT volume=0.1 pitch=1} [sound] minecraft:block.shulker_box.close`
