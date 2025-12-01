# Temporal ZMK Module

ZMK firmware module for the [Temporal keyboard](https://github.com/curbol/temporal).

## Features

- 44-key split ergonomic layout (22 keys per side)
- Rotary encoder support on thumb cluster
- Nice!view display with 26pt font and battery percentage
- Deep sleep power management (30 min idle timeout)
- Compatible with nice!nano v2 and other Pro Micro compatible controllers

## Keyboard Layout

```
Left Side                                          Right Side
┌─────┬─────┬─────┬─────┬─────┬─────┐              ┌─────┬─────┬─────┬─────┬─────┬─────┐
│Extra│Pinky│Ring │ Mid │Index│Inner│              │Inner│Index│ Mid │Ring │Pinky│Extra│
├─────┼─────┼─────┼─────┼─────┼─────┤              ├─────┼─────┼─────┼─────┼─────┼─────┤
│Extra│Pinky│Ring │ Mid │Index│Inner│              │Inner│Index│ Mid │Ring │Pinky│Extra│
└─────┼─────┼─────┼─────┼─────┼─────┤              ├─────┼─────┼─────┼─────┼─────┼─────┘
      │Pinky│Ring │ Mid │Index│Inner│              │Inner│Index│ Mid │Ring │Pinky│
      └─────┴─────┴─────┴─────┴─────┘              └─────┴─────┴─────┴─────┴─────┘
         ┌─────┬─────┬─────┬─────┬─────┐        ┌─────┬─────┬─────┬─────┬─────┐
         │ Enc │Near │ Mid │ Far │Extra│        │Extra│ Far │ Mid │Near │ Enc │
         └─────┴─────┴─────┴─────┴─────┘        └─────┴─────┴─────┴─────┴─────┘
```

## Usage

### Adding to your zmk-config

Add this module to your `config/west.yml`:

```yaml
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: curbol
      url-base: https://github.com/curbol
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: main
      import: app/west.yml
    - name: temporal-zmk
      remote: curbol
      revision: main
  self:
    path: config
```

### Build Configuration

In your `build.yaml`:

```yaml
---
include:
  - board: nice_nano_v2
    shield: temporal_left nice_view_adapter nice_view
  - board: nice_nano_v2
    shield: temporal_right nice_view_adapter nice_view
```

### Keymap

Copy the default keymap to your config folder and customize:

```bash
curl -o config/temporal.keymap https://raw.githubusercontent.com/curbol/temporal-zmk/main/boards/shields/temporal/temporal.keymap
```

## License

MIT License - see [LICENSE](LICENSE) for details.
