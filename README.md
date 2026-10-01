# Tasmota Device Control

Control Tasmota smart plugs and devices via their HTTP API. Device mapping is saved in a YAML config file.

## Features

- Device management via YAML config
- Power on/off/toggle commands
- Status reporting
- Power consumption monitoring (for energy-metering devices)
- Device discovery

## Quick Start

```bash
# Initialize config
tasmota init

# Add your devices to ~/.config/tasmota/devices.yaml
# Then control them:
tasmota my_plug on
tasmota my_plug off
tasmota my_plug status
tasmota my_plug power

# List configured devices
tasmota list
```

## Config Format

`~/.config/tasmota/devices.yaml`:

```yaml
devices:
  living_room_lamp:
    ip: 192.168.88.11
    relay: 1
    has_power_meter: true
  kitchen_fan:
    ip: 192.168.88.12
    relay: 1
    has_power_meter: false
```

## Commands

| Command | Description |
|---------|-------------|
| `tasmota <device> on` | Turn device ON |
| `tasmota <device> off` | Turn device OFF |
| `tasmota <device> toggle` | Toggle device state |
| `tasmota <device> status` | Get device status |
| `tasmota <device> power` | Get power consumption data |
| `tasmota rename <device> <new_name>` | Rename device on hardware + update config |
| `tasmota updateip <device> <new_ip>` | Change device IP on hardware + update config |
| `tasmota list` | List all configured devices |
| `tasmota discover` | Discover Tasmota devices on network |
| `tasmota init` | Initialize config file |

## Power Data

For devices with energy metering (e.g., Sonoff POW), the `power` command reports:

- **Power** (W) - Current power consumption
- **Voltage** (V) - Line voltage
- **Current** (A) - Current draw
- **Today** (Wh) - Energy used today
- **Yesterday** (Wh) - Energy used yesterday
- **Total** (Wh) - Total energy counter

## Tasmota HTTP API

The script uses Tasmota's built-in HTTP interface:

- Power control: `http://<ip>/cm?cmnd=Power<relay>=<ON|OFF>`
- Status: `http://<ip>/cm?cmnd=Status`
- Energy: `http://<ip>/cm?cmnd=Energy`

## Requirements

- Python 3.6+
- PyYAML (`pip install pyyaml`)
- Network access to Tasmota devices

## Installation

```bash
# Make executable
chmod +x tasmota

# Move to PATH
sudo mv tasmota /usr/local/bin/

# Or use locally
./tasmota init
```

## License

MIT
