# Pulsar Feinmann F01 Linux Control

Control your Pulsar Feinmann F01 gaming mouse on Linux without needing the Windows Pulsar Fusion app. Wireless only (via Feinmann 8K Dongle).

Based on [pulsar-x3-python](https://github.com/jonkristian/pulsar-x3-python) by jonkristian.

> **Disclaimer**: This is an unofficial, community-developed tool. It is not affiliated with, endorsed by, or supported by Pulsar Gaming Gears. Use at your own risk.

## Features

| Feature | Read | Write | Notes |
|---------|------|-------|-------|
| Firmware Version | ✅ | - | Mouse and dongle versions |
| DPI | ✅ | ✅ | 50-26000 DPI |
| DPI Stage | ✅ | ✅ | Switch between stages 1-6 |
| Battery | ✅ | - | Real-time percentage |
| Motion Sync | ✅ | ✅ | On/Off |
| Lift-off Distance | ✅ | ✅ | 0.7mm, 1mm, 2mm |
| Angle Snapping | ✅ | ✅ | On/Off |
| Ripple Control | ✅ | ✅ | On/Off |
| Debounce | ✅ | ✅ | Time in ms |
| Polling Rate | ⚠️ | ❌ | Read unreliable, write not working |

## Requirements

- Python 3.6+
- PyUSB library (`python-pyusb` on Arch)
- GTK4 and Libadwaita (for GUI)

## Installation

```bash
# Install PyUSB (Arch Linux)
sudo pacman -S python-pyusb

# Setup udev rules for non-root access
sudo cp 99-pulsar-mouse.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules
sudo udevadm trigger

# Reconnect dongle after adding rules
```

## Usage

### GUI

```bash
python3 pulsar_f01_gui.py
```

### CLI

```bash
# Show all info
python3 pulsar_f01.py --info

# Set DPI directly
python3 pulsar_f01.py --dpi 800

# Switch DPI stage
python3 pulsar_f01.py --stage 2

# Check battery
python3 pulsar_f01.py --battery

# Motion sync
python3 pulsar_f01.py --motion-sync on

# Lift-off distance
python3 pulsar_f01.py --lod 1

# Angle snapping
python3 pulsar_f01.py --angle-snap off

# Ripple control
python3 pulsar_f01.py --ripple-control on

# Debounce time
python3 pulsar_f01.py --debounce 3
```

## Example Output

```
$ python3 pulsar_f01.py --info
✓ Found: Pulsar Feinmann F01 (wireless)
======================================================================
Pulsar Feinmann F01 Mouse Information
======================================================================

Dongle Firmware: 0123
Mouse Firmware: 00.00.00.00

DPI: 700 (stage 1)
Motion Sync: OFF
Lift-off Distance: 1mm
Angle Snapping: OFF
Ripple Control: OFF
Debounce: 3ms
Battery: 94%
Polling Rate: 1000Hz (unreliable)
======================================================================
```

## Device Information

- **Vendor ID**: `0x3710` (Pulsar)
- **Product ID (Feinmann 8K Dongle)**: `0x5404`
- **Interface**: 3 (HID Feature Reports)
- **Protocol**: Same as Pulsar X3 — 64-byte USB HID feature reports with 16-bit LE checksum

## Troubleshooting

### Permission denied
Make sure udev rules are installed and you've reconnected the dongle.

### Device not found
```bash
lsusb | grep 3710
```

### Polling rate
Polling rate read/write is not working correctly. Use the Windows Pulsar Fusion/Bibimbap app to change polling rate.
