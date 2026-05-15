
<img width="2139" height="735" alt="3901b2dd-0b21-4062-9708-efcf3d0a2036" src="https://github.com/user-attachments/assets/87dd7ff5-6cad-47a1-9ee5-7206300c44c6" />


**A lightweight, fully Folia-compatible plugin that applies configurable potion effects  
to players on join, death, respawn, totem pop, and world switch.**

</div>

---

## Features

- Apply any number of potion effects when a player **joins** the server
- Apply effects on **death**, **respawn after death**, and **totem of undying** pop
- Apply effects on **world switch**
- Each trigger is **independently toggled** — enable only what you need
- Effects can be **infinite** or **time-limited** (in seconds)
- Supports **multiple effects per event** with individual amplifier control
- **Live reload** via `/joineffect reload` — no server restart needed
- Full **Folia thread-safety** — uses entity scheduler, no main-thread blocking
- Zero external dependencies, pure Paper/Folia API

---

## Requirements

| Requirement | Version |
|---|---|
| Paper or Folia | 1.21.x |
| Java | 21+ |

---

## Installation

1. Download `JoinEffect.jar` from [Releases](../../releases)
2. Drop it into your server's `plugins/` folder
3. Start or restart the server to generate `config.yml`
4. Edit `plugins/JoinEffect/config.yml` to your liking
5. Run `/joineffect reload` to apply changes without restarting

---

## Configuration

`plugins/JoinEffect/config.yml`

```yaml
# Effects applied when a player joins the server
join-effect:
  enabled: true
  infinite: true        # true = lasts forever | false = uses 'seconds'
  seconds: 60           # duration when infinite is false
  effects:
    - name: NIGHT_VISION
      amplifier: 0      # 0 = Level I,  1 = Level II, ...
    - name: SPEED
      amplifier: 0

# Effects applied when a player dies, respawns, or pops a totem of undying
death-effect:
  enabled: true
  infinite: true
  seconds: 60
  effects:
    - name: NIGHT_VISION
      amplifier: 0

# Effects applied when a player switches worlds
world-change-effect:
  enabled: true
  infinite: true
  seconds: 60
  effects:
    - name: NIGHT_VISION
      amplifier: 0
```

### Available Effect Names

```
NIGHT_VISION      SPEED             SLOWNESS          HASTE
MINING_FATIGUE    STRENGTH          JUMP_BOOST        NAUSEA
REGENERATION      RESISTANCE        FIRE_RESISTANCE   WATER_BREATHING
INVISIBILITY      BLINDNESS         HUNGER            WEAKNESS
POISON            WITHER            HEALTH_BOOST      ABSORPTION
SATURATION        GLOWING           LEVITATION        LUCK
UNLUCK            SLOW_FALLING      CONDUIT_POWER     DOLPHINS_GRACE
BAD_OMEN          HERO_OF_THE_VILLAGE                 DARKNESS
```

---

## Commands & Permissions

| Command | Description | Permission |
|---|---|---|
| `/joineffect reload` | Reloads config.yml live | `joineffect.admin` |
| `/je reload` | Alias for the above | `joineffect.admin` |

---

## How Each Trigger Works

| Trigger | When it fires | Notes |
|---|---|---|
| `join-effect` | Player connects to the server | Applied 1 second after join to let the spawn animation finish |
| `death-effect` | Player dies | Applied immediately at death |
| `death-effect` | Player respawns | Re-applied 0.25 s after the respawn screen closes |
| `death-effect` | Totem of undying pops | Applied immediately — no respawn screen |
| `world-change-effect` | Player switches worlds | Applied immediately on world change |

---

## License

All rights reserved. Do not redistribute or modify without permission.
