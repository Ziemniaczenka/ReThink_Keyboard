# Keyboard power

Current drawn from the Control Board's battery with each keyboard on the adapter, by keyboard FRU. Two keyboards of one model can differ by a factor of two, almost all of it in the pointing stick, so each keyboard is listed on its own.

## Setup

- Control Board on its battery (about 4.2 V), the multimeter's mA range in series with the battery, USB unplugged.
- Firmware: [rethink-zmk-config](https://github.com/Ziemniaczenka/rethink-zmk-config), the keyboard's shield built with the shell (`-Snippet rethink-usb-shell`), at the commit in the table. Connected to a host over Bluetooth, idle, hands off the keyboard and the stick. The stick reports 80 times a second (`tp set rate`, the default on battery).
- Stick off: Fn+F8, which switches TP_3V3 off (and the charge pump with it).
- Stick supply: TP1 (Mezzanine, FFC1) at 5 V from the adapter's charge pump through the level shifter (JP4, JP5, JP6 at 1-2), so the battery pays about twice the stick's own current. TP2 (FFC2) at 3.3 V, direct (JP7, JP8, JP9 at 1-2).

## Measurements

| Keyboard | FRU | Layout | Port | Stick off | Stick on | Lock LEDs | Firmware | Date |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| T420 | 45N2161 (P/N 45N2126, model C9-90N0) | Norwegian ISO | Mezzanine, TP1 5 V | 1.56 mA | 19.1 mA | Caps Lock +1.9 mA | 1396ae9, 42ded20 | 2026-11-08 |
| T420 | 45N2241 (P/N 45N2206, model C989) | US ANSI | Mezzanine, TP1 5 V | 1.5 mA | 25.5 mA | | 1396ae9, 42ded20 | 2026-11-11 |
| L420 | 45N2373 | Norwegian ISO | FFC1, TP1 5 V | 1.5 mA | 33 mA | | 42ded20 | 2026-11-11 |
| L420 | 45N2362 | Norwegian ISO | FFC1, TP1 5 V | 1.5 mA | 18 mA | | 42ded20 | 2026-11-11 |
| T480 | 01AX516 | UK ISO | FFC2, TP2 3.3 V | 1.6 mA | 4.5 mA | Caps Lock: 5.0 mA, 8.0 mA with the stick | 5796c7e | 2026-11-11 |
| E580 | 01YN773 | US ANSI (Thai legends) | FFC2, TP2 3.3 V | 1.5 mA | 2.1 mA | Caps Lock 3.2 mA, Num Lock 3.3 mA; both and the stick 4.8 mA | 5796c7e | 2026-11-11 |

The firmware column is the rethink-zmk-config commit. The T420 keyboards read the same with both commits. The T480 and E580 were measured with their shields as committed in 5796c7e, except that Alt+Fn+F8 (press-to-select) was still bound.

## Notes

- The stick is nearly all of the difference: on top of the board's 1.5 mA it adds 0.6 mA (E580) to 31.5 mA (L420 45N2373). The 3.3 V sticks of the 2018 keyboards draw a tenth of what the 5 V sticks of 2011 do.
- Lock LED current depends on the keyboard's own LED resistor: Caps Lock adds 1.7 mA on the E580, 1.9 mA on the T420, 3.4 mA on the T480.
- Unused, the firmware switches the stick off after 10 minutes (the stick-off figure) and, on battery, the whole board after 30 minutes (System OFF, about 7 µA).
- Stick details (more in the firmware's README, Pointing stick): the T420 stick reports ID 01, firmware 0e. Press-to-select doesn't work on the T480's and E580's sticks; newer generations dropped it.

## Backlight

Current from the battery with the backlight on, at the firmware's two steps (Fn+Space): 51 % and 100 % of the duty cap (`CONFIG_RETHINK_BACKLIGHT_MAX_DUTY`, or `backlight max` in the shell). VLED_BL from the Control Board's BUCK1 (3.3 V), boosted to 5 V by the adapter's U4. Same setup as above, with the stick on, over Bluetooth, and 100 µF across the battery input (the prerelease bootloader's boot loop through the meter, see the firmware's docs/power.md).

| Keyboard | FRU | PWM | Cap | Off | Low | High | Firmware | Date |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| E580 | 01YN773 | 4096 Hz | 10 % | 2.2 mA | 28 mA | 53 mA | 1e4f733 | 2026-11-17 |
| E580 | 01YN773 | 25 kHz | 10 % | 2.3 mA | 27.5 mA | 50.5 mA | after 1e4f733 | 2026-11-17 |
| E580 | 01YN773 | 25 kHz | 15 % | | 38.7 mA | 75.9 mA | after 1e4f733 | 2026-11-17 |
| E580 | 01YN773 | 25 kHz | 20 % | | | 93-100 mA | after 1e4f733 | 2026-11-17 |

- About 5 mA from the battery per 1 % of duty, so full duty would draw about 0.5 A, more than BUCK1 delivers (200 mA at 3.3 V). The firmware runs the E580 at a 20 % cap.
- At 4096 Hz, AC-coupled on the scope: VLED_BL 610 mV p-p (dips about 40 µs long, one per PWM period), BL_5V 62 mV p-p, the battery input 100 mV p-p (through the meter). Coil whine, audible with the keyboard out of its case. At 25 kHz still faintly audible at the low step; at 50 kHz (and 100 kHz) silent, so the firmware uses 50 kHz.
- On USB, charging at 450 mA, the charge current dropped with the backlight on: the nPM1300's USB input limit, 500 mA. The firmware now raises it to 1.5 A on USB-C sources that offer 1.5 A or 3 A: 440 mA into the cell with the backlight on (see the firmware's docs/power.md).
