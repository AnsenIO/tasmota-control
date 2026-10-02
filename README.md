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
    has_power_meter: true
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

For devices with energy metering (e.g., Eightree 16A Plug), the `power` command reports:

- **Power** (W) - Current power consumption
- **Voltage** (V) - Line voltage
- **Current** (A) - Current draw
- **Today** (Wh) - Energy used today
- **Yesterday** (Wh) - Energy used yesterday
- **Total** (Wh) - Total energy counter
- **Factor** (PF) - Power factor
- **ApparentPower** (VA) - Apparent power
- **ReactivePower** (VAR) - Reactive power

## Tasmota HTTP API

The script uses Tasmota's built-in HTTP interface:

- Power control: `http://<ip>/cm?cmnd=Power<relay>=<ON|OFF>`
<<<<<<< HEAD
- Status: `http://<ip>/cm?cmnd=Status`
- Energy: `http://<ip>/cm?cmnd=status%208`
=======
- Status: `http://<ip>/cm?cmnd=status%208`
- Status (abbreviated): `http://<ip>/cm?cmnd=status%201`

## Testing

**Tested exclusively on Eightree 16A Plugs (ET28) with Tasmota firmware.**

All four devices verified:
- temp1 (192.168.88.2) - Eightree 16A Plug
- temp2 (192.168.88.3) - Eightree 16A Plug
- rpi-kvm-gx10 (192.168.88.11) - Eightree RPI KVM
- gx10 (192.168.88.10) - Eightree GX10

No testing has been performed on other Tasmota device types (Sonoff, Shelly, etc.). Compatibility with other hardware may vary.
>>>>>>> 952fdfa0a8f7a7a2ece60de954bcce61ec14ad5e

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
