# Changelog

## [0.1.1] - 2025-12-05

- Added file lock (`/tmp/pulsar-x3.lock`) to prevent concurrent USB access conflicts
- Added retry logic (3 attempts) for USB communication errors
- Fixes "Resource busy" errors when multiple processes try to access the mouse

## [0.1.0] - 2025-11-29

- Initial release
- CLI tool (`pulsar-x3`) for controlling mouse settings
- GTK4/Libadwaita GUI (`pulsar-x3-gui`)
- Support for wired and wireless modes
- Features: DPI, DPI stages, battery, motion sync, lift-off distance, angle snapping, ripple control, debounce
- Udev rules for non-root USB access
- Desktop entry for application menu
