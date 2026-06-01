# sunseeker-schedule-card

[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/hacs/integration)

A custom Lovelace card for the [Sunseeker](https://www.home-assistant.io/integrations/sunseeker/) integration that lets you view and edit the robot mower's weekly mowing schedule directly from your dashboard. Works with both **wireless models** (V, V1, X, S) and **old wired models**.

<img width="510" height="792" alt="image" src="https://github.com/user-attachments/assets/2fa0d209-f491-46c6-b5da-385e2a443b37" />

---

## Features

- **Old wired model support** — the card automatically detects old wired models and switches to a simplified one-slot-per-day layout with an enabled toggle, start/end time pickers, and a border-trim toggle. The Recommended / User defined / Pause mode buttons are hidden as they are not applicable.
- **Schedule active toggle** — for old wired models, an optional *Schedule active* button at the top of the card mirrors the mower's "Schedule active" switch. Clicking it immediately turns the schedule on or off: turning it off clears the schedule on the server while keeping the times stored locally; turning it back on restores the stored schedule to the server. Requires the `schedule_switch` config option to be set *(old wired models)*.
- **Full weekly schedule** — displays all seven days (Monday – Sunday), each collapsible, with up to two mowing time-slots (entries) per day *(wireless models)*.
- **Per-entry controls** — each slot shows an enabled/disabled toggle, a start time picker, an end time picker, and a set of zone location buttons to select which zones are active during that slot *(wireless models)*.
- **Schedule-mode selector** — three mutually exclusive top-level mode buttons let you switch between *Recommended*, *User defined*, and *Pause* without leaving the card *(wireless models)*.
- **View / Edit modes** — in view mode all controls are read-only, showing the live schedule from the mower. Pressing *Edit* unlocks all controls and buffers changes locally. *Submit* sends the updated schedule to the mower via the `sunseeker.set_schedule` service; *Cancel* discards all pending changes.
- **Smart collapse** — individual day sections and entry slots can be expanded or collapsed. Disabled entries start collapsed automatically. The card header can also be collapsed. A `collapsed_header` config option controls the default state.
- **Change-detection** — the card only re-renders when the schedule actually changes, preventing unnecessary DOM churn.
- **Localised UI** — all labels and button text are translated for English, Danish, Finnish, French, German, and Polish, following the user's Home Assistant language setting.
- **Visual editor** — full support for the Lovelace UI editor; no YAML required.

---

## Requirements

- Home Assistant with the **Sunseeker** integration configured.
- A sensor entity whose `schedule` attribute contains the weekly schedule object (e.g. `sensor.sunseeker_schedule`).
  - **Wireless models (V, V1, X, S):** use the dedicated `Schedule` sensor created by the integration.
  - **Old wired models:** use the `Schedule` sensor. The integration automatically includes a `model_type: "old"` field in the schedule attribute, which the card uses to switch to the simplified layout.
- To use the **Schedule active** toggle on old wired models, you also need the `Schedule active` switch entity created by the integration (e.g. `switch.sunseeker_schedule_active`). Pass it via the `schedule_switch` config option.

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
| `schedule_switch` | `string` | `null` | Entity ID of the Sunseeker *Schedule active* switch (e.g. `switch.sunseeker_schedule_active`). When set, a toggle button is shown for old wired models that turns the schedule on/off directly. |
| `header` | `string` | `"Sunseeker Schedule"` | Card header title (localised default used when omitted). |
| `show_header` | `boolean` | `true` | Show or hide the card header. |
| `collapsed_header` | `boolean` | `false` | Start with the card body collapsed. The header remains visible and clickable to expand. |

### Minimal YAML example

```yaml
type: custom:sunseeker-schedule-card
entity: sensor.sunseeker_schedule
```

### Full YAML example (old wired model)

```yaml
type: custom:sunseeker-schedule-card
entity: sensor.sunseeker_schedule
schedule_switch: switch.sunseeker_schedule_active
header: Mowing Schedule
show_header: true
collapsed_header: false
```

### Full YAML example (wireless model)

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
| 1.0.9 | Added support for old wired models (single slot per day, border trim toggle, automatic layout detection); added Schedule active toggle for old wired models via `schedule_switch` config option |
| 1.0.8 | Added Finnish and Polish language support |
| 1.0.7 | Previous release |

