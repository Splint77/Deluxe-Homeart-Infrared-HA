# Deluxe Homeart Infrared

[![hacs][hacs-badge]][hacs]
[![GitHub Release][releases-shield]][releases]
![Project Maintenance][maintenance-shield]

Home Assistant custom integration for **Deluxe Homeart LED candles** controlled by the infrared remote model **FB-0001** (EAN 745114424044).

It sends the remote's NEC infrared commands through Home Assistant's built-in [`infrared`][ha-infrared] component, so any IR transmitter registered with that component (for example a BroadLink or an ESPHome IR blaster) can control the candles.

> This is not an official Deluxe Homeart integration. The IR codes were reverse-engineered from the original remote using a BroadLink RM4 Pro.

## Supported functionality

The integration creates the following entities:

| Platform | Entity          | Description                                   |
| :------- | :-------------- | :-------------------------------------------- |
| `light`  | *(device name)* | Turn on/off and step brightness up/down       |
| `button` | Brightness up   | Increase brightness by one step               |
| `button` | Brightness down | Decrease brightness by one step               |
| `button` | Timer 2H        | Start the candles' built-in 2-hour auto-off   |
| `button` | Timer 4H        | Start the candles' built-in 4-hour auto-off   |
| `button` | Timer 6H        | Start the candles' built-in 6-hour auto-off   |
| `button` | Timer 8H        | Start the candles' built-in 8-hour auto-off   |

## Requirements

- Home Assistant **2026.6.0** or newer.
- An IR transmitter registered with the Home Assistant [infrared][ha-infrared] integration, such as a [BroadLink][broadlink] device or an [ESPHome][esphome] device with `remote_transmitter`, placed within line of sight of the candles.

## Installation

### HACS (recommended)

1. Open **HACS** in Home Assistant.
2. Search for **Deluxe Homeart Infrared** and download it.
3. Restart Home Assistant.

[![Open your Home Assistant instance and open this repository in HACS.][hacs-repo-badge]][hacs-repo]

If the integration is not yet listed in the HACS default store, add it as a custom repository:

1. In **HACS**, open the three-dot menu → **Custom repositories**.
2. Add `https://github.com/Splint77/Deluxe-Homeart-Infrared-HA` with type **Integration**.
3. Search for **Deluxe Homeart Infrared**, download it and restart Home Assistant.

### Manual

1. Copy the `custom_components/deluxe_homeart_infrared` folder into your Home Assistant `config/custom_components/` directory.
2. Restart Home Assistant.

## Configuration

1. Go to **Settings → Devices & services → Add integration**.
2. Search for **Deluxe Homeart Infrared**.
3. Select the infrared emitter entity that should send the commands.

You can add the integration once per infrared emitter. If no emitter is found, the setup is aborted. Set up your IR transmitter first.

## Limitations

- **Assumed state.** The candles don't report their state back, so Home Assistant tracks on/off and brightness locally and restores them after a restart. If the candles are controlled with the physical remote, the state in Home Assistant can drift.
- **Stepwise brightness only.** The candles don't support setting an absolute brightness. Each brightness change sends a single "up" or "down" command, and the brightness shown in Home Assistant is an estimate (about 10% per step).
- **Broadcast IR.** Every candle within range of the transmitter reacts to every command. Individual candles can't be addressed.

## IR codes

The codes were captured from the original remote with a BroadLink RM4 Pro.

| Button          | Protocol     | Address  | Command |
| --------------- | ------------ | -------- | ------- |
| On              | NEC          | `0x00`   | `0x5E`  |
| Off             | NEC          | `0x00`   | `0x0C`  |
| Timer 2H        | NEC          | `0x00`   | `0x46`  |
| Timer 4H        | NEC          | `0x00`   | `0x40`  |
| Timer 6H        | NEC          | `0x00`   | `0x15`  |
| Timer 8H        | NEC          | `0x00`   | `0x19`  |
| Brightness up   | Extended NEC | `0x08B7` | `0x12`  |
| Brightness down | Extended NEC | `0x08B7` | `0x10`  |

## Issues

Please report bugs and feature requests on the [issue tracker][issues].

## License

[MIT](LICENSE)

[hacs]: https://hacs.xyz
[hacs-badge]: https://img.shields.io/badge/HACS-Custom-41BDF5.svg
[ha-infrared]: https://www.home-assistant.io/integrations/infrared/
[broadlink]: https://www.home-assistant.io/integrations/broadlink/
[esphome]: https://www.home-assistant.io/integrations/esphome/
[releases-shield]: https://img.shields.io/github/release/Splint77/Deluxe-Homeart-Infrared-HA.svg
[releases]: https://github.com/Splint77/Deluxe-Homeart-Infrared-HA/releases
[maintenance-shield]: https://img.shields.io/maintenance/yes/2026.svg
[hacs-repo]: https://my.home-assistant.io/redirect/hacs_repository/?owner=Splint77&repository=Deluxe-Homeart-Infrared-HA&category=integration
[hacs-repo-badge]: https://my.home-assistant.io/badges/hacs_repository.svg
[issues]: https://github.com/Splint77/Deluxe-Homeart-Infrared-HA/issues
