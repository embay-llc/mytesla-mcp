# Tool Manifest

The mytesla.io MCP server exposes exactly these **40 fixed tools**. The set does
not change based on what a client asks for, and there is **no tool that drives
the car**. Each tool is annotated below with an MCP-standard hint:

- **read-only** (`readOnlyHint: true`) — returns data, changes nothing.
- **write** (`readOnlyHint: false`) — changes vehicle state; reversible and
  low-consequence.
- **write · sensitive** (`readOnlyHint: false, destructiveHint: true`) — grants
  physical access or changes a security setting. PIN-protected actions require a
  PIN the user sets; the AI cannot bypass it.

All command tools are signed requests through Tesla's official Fleet API and
Vehicle Command Protocol. All tool inputs are validated with strict schemas
before any upstream call.

## Reads

| Tool | Hint | Purpose |
|---|---|---|
| `get_vehicles` | read-only | List vehicles on the account |
| `get_vehicle_status` | read-only | Live state: battery, range, climate, locks, location |
| `get_credit_balance` | read-only | Remaining mytesla.io credits |

## Climate

| Tool | Hint | Purpose |
|---|---|---|
| `wake_vehicle` | write | Wake the car from sleep (needed before some commands) |
| `start_climate` / `stop_climate` | write | Turn climate on/off |
| `set_cabin_temperature` | write | Set target cabin temperature |
| `max_defrost` | write | Toggle max defrost |
| `set_seat_heater` / `set_seat_cooler` | write | Per-seat heating/cooling |
| `set_steering_wheel_heater` | write | Heated steering wheel |
| `set_climate_keeper_mode` | write | Keep/Dog/Camp mode |
| `set_cabin_overheat_protection` | write | Cabin overheat protection |

## Charging

| Tool | Hint | Purpose |
|---|---|---|
| `start_charging` / `stop_charging` | write | Start/stop a charge session |
| `set_charge_limit` | write | Set charge % limit |
| `set_charging_amps` | write | Set charge current |
| `open_charge_port` | write | Open the charge port |
| `close_charge_port` | write · sensitive | Close the charge port |
| `set_scheduled_charging` | write | Schedule a charge window |
| `set_scheduled_departure` | write | Schedule departure / precondition-by-time |

## Access & cargo

| Tool | Hint | Purpose |
|---|---|---|
| `lock_vehicle` | write · sensitive | Lock the doors |
| `unlock_vehicle` | write · sensitive | Unlock the doors (grants physical access) |
| `actuate_trunk` | write · sensitive | Open/close trunk or frunk |
| `control_windows` | write · sensitive | Vent/close windows |
| `sun_roof_control` | write · sensitive | Control the sunroof (if equipped) |

## Alerts & navigation

| Tool | Hint | Purpose |
|---|---|---|
| `honk_horn` | write | Honk the horn |
| `flash_lights` | write | Flash the lights (find the car) |
| `share_destination` | write | Send a destination to the nav system |
| `trigger_homelink` | write · sensitive | Trigger a HomeLink device (e.g. garage) |

## Security

| Tool | Hint | Purpose |
|---|---|---|
| `set_sentry_mode` | write | Toggle Sentry Mode |
| `set_valet_mode` | write · sensitive | Enable/disable Valet Mode (PIN) |
| `reset_valet_pin` | write · sensitive | Reset the Valet PIN |
| `set_speed_limit` | write · sensitive | Set a speed limit (PIN) |
| `speed_limit_activate` / `speed_limit_deactivate` | write · sensitive | Toggle speed limiting (PIN) |
| `speed_limit_clear_pin` | write · sensitive | Clear the speed-limit PIN |

## Software & feedback

| Tool | Hint | Purpose |
|---|---|---|
| `schedule_software_update` | write | Schedule a software update |
| `cancel_software_update` | write | Cancel a scheduled update |
| `report_bug` | write | Send feedback to mytesla.io (free, no vehicle action) |

## What is **not** here

There is no tool to steer, accelerate, brake, engage Autopilot/FSD, or otherwise
move the vehicle. PIN-protected functions (Valet, speed limit) always require the
user-set PIN — the AI cannot read, set, or bypass it.
