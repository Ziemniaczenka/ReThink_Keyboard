# ReThink Keyboard

Adapting older ThinkPad laptop keyboard modules into standalone keyboards using Framework Control Board.

## Hardware overview
- **Framework Control Board** - nRF54LM20A, Bluetooth/dongle/USB-C connection, nPM1300 power management IC.
- **ReThink Adapter Board** - bridge between Control Board and ThinkPad keyboards.
- **3D Printed case** - housing for components, different for each keyboard type.
- **ThinkPad keyboard modules** - 6 and 7row, classic and chiclet, with or without backlight, with integrated Pointing Stick (nub) and mouse keys. Full list TBD.
- **ZMK Firmware** - based on Zephyr RTOS, provides customizability. Each keyboard type will be different shield.

> Note: This is preliminary information. Everything is subject to change and more information will follow.

## Reference pinouts

<!-- - [Framework Wireless Touchpad Keyboard connector](docs/pinouts/framework_ffc.md) -->
- [Mezzanine Connector](docs/pinouts/mezzanine.md)
<!-- - [L420 Connector] -->

## Mechanical CAD
  
- TBD

## ReThink Adapter

   Adapter board that will connect to Control Board using FFC cable, then have a bunch of connectors for different generations of ThinkPad, boost converter (if necessary for pointing stick, backlight (TBD)) and probably i2c IO expander (because of number of direct, non-matrix keys and LEDs on older generations that I want to keep functional).

## Battery

- TBD

## Firmware and Bootloader

- ZMK Configuration will be based on GitHub in separate repository (TBD)

## Compatibility Table

- TBD

## License

ReThink keyboard by Ziemniaczenka is licensed under CC BY-SA 4.0.
To view a copy of this license, visit https://creativecommons.org/licenses/by-sa/4.0/

## Disclaimers
> Framework Control Board was provided pre-release by Framework Computer Inc. through Control Board Developer Program.

> ThinkPad and TrackPoint are registered trademarks of Lenovo. ReThink is an independent open-source project and is not affiliated with, endorsed by, or certified by Lenovo Group Limited.
