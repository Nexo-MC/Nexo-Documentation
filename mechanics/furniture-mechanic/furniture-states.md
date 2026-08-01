# 🔀 Furniture States

Nexo lets a furniture have several states which it cycles between when a player interacts with it.\
A lightswitch, a TV with different channels, a trashcan that fills up, and so on.

Every state is a named subsection of `states`, and interacting with the furniture cycles to the next one.\
Nexo always adds an empty state, which is the furniture as defined outside of the `states` section.\
This means a furniture with 2 defined states cycles between 3 states in total, the empty one included.

```yaml
myitem:
  itemname: "<gray>TV"
  material: PAPER
  Pack:
    model: default/tv
  Mechanics:
    furniture:
      hitbox:
        barriers:
          - 0,0,0
      states:
        channel_one:
          type: ITEM_MODEL
          item_model: nexo:furniture/tv_channel_one
        channel_two:
          type: ITEM_MODEL
          item_model: nexo:furniture/tv_channel_two
```

## State-Types

The `type` decides what a state actually changes on the furniture.\
If left unspecified it defaults to `DEFAULT`, which changes nothing on its own.

### ITEM\_MODEL

Swaps the ItemModel of the furniture, using the `item_model` property.

```yaml
      states:
        on:
          type: ITEM_MODEL
          item_model: nexo:furniture/lamp_on
```

### CUSTOM\_MODEL\_DATA

Swaps the CustomModelData of the furniture, using the `value` property.\
Mainly useful for older packs that do not use ItemModels.

The type of the value is detected automatically, meaning it can be a string, number, true/false or a color.

```yaml
      states:
        on:
          type: CUSTOM_MODEL_DATA
          value: lamp_on
```

### FURNITURE

The most flexible type. The state is a full furniture-mechanic of its own, which is merged on top of the parent furniture.\
Anything you can put in the `furniture`-section can be put in this state, and it will override the parent value.\
Properties you do not specify are inherited from the parent furniture.

Useful when a state should also change the hitbox, lights, seats or properties, not just the model.

```yaml
      states:
        open:
          type: FURNITURE
          item_model: nexo:furniture/cabinet_open
          properties:
            translation: 0,0.5,0
          hitbox:
            barriers:
              - 0,0,0
              - 0,1,0
```

{% hint style="info" %}
A `FURNITURE`-state cannot define its own `states`-section, as that would recurse infinitely.
{% endhint %}

### MODELENGINE

Swaps the ModelEngine-model of the furniture to the given `blueprint`.\
When leaving this state, the furnitures normal `modelengine_id` model is put back, if it has one.

Requires ModelEngine on the server, and the blueprint must exist.

```yaml
      states:
        broken:
          type: MODELENGINE
          blueprint: my_broken_tv
```

### ANIMATION

Plays a ModelEngine-animation on the furnitures current model when entering the state, and stops it when leaving.\
Requires that the furniture itself is a [ModelEngine Furniture](./#modelengine-furniture).

**animation -** The name of the animation to play\
**lerp\_in -** Duration to blend into the animation (1t, 2s, 3m, etc...). Default is 0\
**lerp\_out -** Duration to blend out of the animation. Default is 0\
**speed -** Speed-multiplier of the animation. Default is 1.0\
**force -** If the animation should override any currently playing animation. Default is true

```yaml
      states:
        opening:
          type: ANIMATION
          animation: open
          lerp_in: 5t
          lerp_out: 5t
          speed: 1.0
          force: true
```

### MODELENGINE\_ANIM

A combination of `MODELENGINE` and `ANIMATION`. It swaps to the given `blueprint` and plays the given `animation` on it.\
Takes all the properties of both types.

```yaml
      states:
        broken:
          type: MODELENGINE_ANIM
          blueprint: my_broken_tv
          animation: sparks
```

## Automatic State-Changes

States do not have to be cycled by a player, they can also change on their own after a set duration.\
Both take a duration-format (1t, 2s, 3m, etc...), and `reset_after` takes priority if both are set.

**reset\_after -** Returns to the empty state after this duration\
**next\_after -** Cycles to the next state after this duration

Both can be set on the `states`-section itself to apply to every state, and any state can override it.

```yaml
      states:
        next_after: 3s      # Default for every state below
        channel_one:
          type: ITEM_MODEL
          item_model: nexo:furniture/tv_channel_one
        channel_two:
          type: ITEM_MODEL
          item_model: nexo:furniture/tv_channel_two
          reset_after: 10s  # Overrides the parents next_after
```

## Conditions

You can limit who is able to cycle states, and what states they can cycle to.

The `condition`-property on the `states`-section decides if the player may cycle the furniture at all.\
The `conditions`-property on a state decides if that specific state can be cycled to, states failing it are skipped.

Both accept either a single condition or a list of them, and all of them must pass.\
They are written as [Spring Expression Language](https://docs.spring.io/spring-framework/reference/core/expressions/language-ref.html)-expressions, where the root object is the interacting player.\
There is also a `#player` and `#server` variable available.

```yaml
      states:
        condition: "hasPermission('nexo.tv.use')"
        channel_one:
          type: ITEM_MODEL
          item_model: nexo:furniture/tv_channel_one
        premium_channel:
          type: ITEM_MODEL
          item_model: nexo:furniture/tv_premium
          conditions:
            - "hasPermission('nexo.tv.premium')"
            - "#server.onlinePlayers.size() > 1"
```
