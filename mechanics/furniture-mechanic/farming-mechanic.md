---
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966831327984893992/unknown.png
coverY: 0
---

# Farming Mechanic

### How does it work?

Nexo has a system for planting plants with various stages of growth, an example of how to configure it.

**delay** the time in ticks that it takes to grow\
**probability** to grow when the delay is passed\
**light\_boost** when it has light nearby it grows faster\
**next\_stage** you specify the next stage, it has to be an already created Nexo item.

```yaml
rose_plant:
  itemname: "<gradient:#46EEAA:#2CBFC7>Rose Plant"
  material: COOKED_BEEF
  Pack:
    model: custom/plants/rose_stage_1

rose_seed:
  itemname: "<gradient:#46EEAA:#2CBFC7>Rose Seed"
  material: PAPER
  Mechanics:
    furniture:
      item: rose_plant_stage1
      evolution:
        delay: 10000
        probability: 0.5
        light_boost: true
        next_stage: rose_plant_stage1
      drop:
        silktouch: true
  Pack:
    model: custom/plants/rose_stage_1
```

### First stage

```yaml
rose_plant_stage1:
  material: PAPER
  Mechanics:
    furniture:
      evolution:
        delay: 10000
        probability: 0.5
        light_boost: true
        next_stage: rose_plant_stage2
      drop:
        silktouch: true
  Pack:
    model: custom/plants/rose_stage_1
```

### Second stage

```yaml
rose_plant_stage2:
  material: PAPER
  Mechanics:
    furniture:
      evolution:
        delay: 10000
        probability: 0.5
        light_boost: true
        next_stage: rose_plant_stage3
      drop:
        silktouch: true
  Pack:
    model: custom/plants/rose_stage_2
```

### Third stage

```yaml
rose_plant_stage3:
  material: PAPER
  Mechanics:
    furniture:
      evolution:
        delay: 100000
        probability: 0.25
        light_boost: true
      drop:
        silktouch: true
        loots:
          - { nexo_item: rose_seed, max_amount: 2, probability: 0.75 }
          - { nexo_item: rose_plant, max_amount: 5, probability: 0.55 }
  Pack:
    model: custom/plants/rose_stage_3
```

The plants can have the stages you decide, and the stages have to be a model created by you and not by the plugin for it to work. Now let's explain each mechanic **farmland\_required** It is to be placed only in fertile soil.

***
