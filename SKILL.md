---
name: tasmota-control
description: Control Tasmota smart plugs and devices via HTTP API, report power consumption. Device mapping saved in YAML config.
category: home-automation
---

# Tasmota Device Control

Control Tasmota smart plugs/devices via their HTTP API. Device mapping is stored in `config/devices.yaml`.

## Setup

Add devices to `config/devices.yaml`:

```yaml
devices:
  device_name:
    ip: 192.168.88.XX
    relay: 1  # relay number (default 1)
    has_power_meter: true  # if device reports power data
```

## Commands

### Turn ON
```
tasmota <device> on
```

### Turn OFF
```
tasmota <device> off
```

### Toggle
```
tasmota <device> toggle
```

### Check Status
```
tasmota <device> status
```

### Power Consumption
```
tasmota <device> power
```

## How It Works

The script uses Tasmota's HTTP API:
- Power: `http://<ip>/cm?cmnd=Power<relay>=<ON|OFF>`
- Status: `http://<ip>/cm?cmnd=Status`
- Power Meter: `http://<ip>/cm?cmnd=Energy`

Power data is reported as:
- `Power` (W)
- `Voltage` (V)
- `Current` (A)
- `Today` (Wh)
- `Yesterday` (Wh)
- `Total` (Wh)
