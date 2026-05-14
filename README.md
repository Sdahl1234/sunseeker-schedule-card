# sunseeker-schedule-card

[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/hacs/integration)

A custom Lovelace card for the [Sunseeker](https://www.home-assistant.io/integrations/sunseeker/) integration that lets you view and edit the robot mower's weekly mowing schedule directly from your dashboard.

<img width="510" height="792" alt="image" src="https://github.com/user-attachments/assets/2fa0d209-f491-46c6-b5da-385e2a443b37" />

---

## Features

- **Full weekly schedule** — displays all seven days (Monday – Sunday), each collapsible, with up to two mowing time-slots (entries) per day.
- **Per-entry controls** — each slot shows an enabled/disabled toggle, a start time picker, an end time picker, and a set of zone location buttons to select which zones are active during that slot.
- **Schedule-mode selector** — three mutually exclusive top-level mode buttons let you switch between *Recommended*, *User defined*, and *Pause* without leaving the card.
- **View / Edit modes** — in view mode all controls are read-only, showing the live schedule from the mower. Pressing *Edit* unlocks all controls and buffers changes locally. *Submit* sends the updated schedule to the mower via the `sunseeker.set_schedule` service; *Cancel* discards all pending changes.
- **Smart collapse** — individual day sections and entry slots can be expanded or collapsed. Disabled entries start collapsed automatically. The card header can also be collapsed. A `collapsed_header` config option controls the default state.
- **Change-detection** — the card only re-renders when the schedule actually changes, preventing unnecessary DOM churn.
- **Localised UI** — all labels and button text are translated for English, Danish, Finnish, French, German, and Polish, following the user's Home Assistant language setting.
- **Visual editor** — full support for the Lovelace UI editor; no YAML required.

---

## Requirements

- Home Assistant with the **Sunseeker** integration configured.
- A sensor entity whose `schedule` attribute contains the weekly schedule object (e.g. `sensor.sunseeker_schedule`).

---

## Installation

### HACS (recommended)

1. Open **HACS** in your Home Assistant instance.
2. Go to **Frontend** and click **+ Explore & Download Repositories**.
3. Search for **Sunseeker Schedule Card** and click **Download**.
4. Reload your browser or the Lovelace resources.

### Manual

1. Copy `sunseeker-schedule-card.js` into your `/config/www/sunseeker-schedule-card/` directory (or any subfolder of `www/`).
2. Add the resource in **Settings → Dashboards → Resources**:
   - URL: `/local/sunseeker-schedule-card/sunseeker-schedule-card.js`
   - Resource type: **JavaScript module**
3. Reload your browser or the Lovelace resources.

---

## Configuration

| Key | Type | Default | Description |
|---|---|---|---|
| `entity` | `string` | **required** | Entity ID of the Sunseeker schedule sensor (e.g. `sensor.sunseeker_schedule`). |
| `header` | `string` | `"Sunseeker Schedule"` | Card header title (localised default used when omitted). |
| `show_header` | `boolean` | `true` | Show or hide the card header. |
| `collapsed_header` | `boolean` | `false` | Start with the card body collapsed. The header remains visible and clickable to expand. |

### Minimal YAML example

```yaml
type: custom:sunseeker-schedule-card
entity: sensor.sunseeker_schedule
```

### Full YAML example

```yaml
type: custom:sunseeker-schedule-card
entity: sensor.sunseeker_schedule
header: Mowing Schedule
show_header: true
collapsed_header: false
```

---

## Version history

| Version | Notes |
|---|---|
| 1.0.8 | Added Finnish and Polish language support |
| 1.0.7 | Previous release |

