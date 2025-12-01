# Temporal ZMK Module

ZMK firmware module for the [Temporal keyboard](https://github.com/curbol/temporal).

## Features

- 44-key split ergonomic layout (22 keys per side)
- Rotary encoder support on thumb cluster
- Nice!view display support
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
      └─────┴──┬──┴──┬──┴──┬──┴──┬──┘              └──┬──┴──┬──┴──┬──┴──┬──┴─────┘
              ┌┴────┬┴────┬┴────┬┴────┬─────┐  ┌─────┬┴────┬┴────┬┴────┬┴────┐
              │ Enc │Near │ Mid │ Far │Extra│  │Extra│ Far │ Mid │Near │ Enc │
              └─────┴─────┴─────┴─────┴─────┘  └─────┴─────┴─────┴─────┴─────┘
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
cp boards/shields/temporal/temporal.keymap config/
```

## Pin Assignments

| Function    | Pin  | Notes |
|-------------|------|-------|
| Row Top     | P4   |       |
| Row Home    | P5   |       |
| Row Bottom  | P6   |       |
| Row Thumb   | P7   |       |
| Col Extra   | P21  |       |
| Col Pinky   | P20  | Also encoder switch column |
| Col Ring    | P19  |       |
| Col Middle  | P18  |       |
| Col Index   | P15  |       |
| Col Inner   | P14  |       |
| Encoder A   | P0   | Rotation |
| Encoder B   | P1   | Rotation |
| SPI MOSI    | P8   | nice!view |
| SPI SCK     | P9   | nice!view |
| SPI CS      | P10  | nice!view |

## Encoder Notes

The encoder switch (push button) is mapped to the matrix at position row_thumb × col_pinky. Ensure the encoder's switch pin is connected to row_thumb (P7) for the button press to register as a key.

The encoder rotation uses pins P0 and P1 with the EC11 driver.

## License

MIT License - see [LICENSE](LICENSE) for details.
