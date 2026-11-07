# Adapter bring-up

Checks for a freshly assembled ReThink Adapter v1.0 (Full variant), before it carries a keyboard. Work through the tables in order. Each row says what to do and what to expect: if it matches, go to the next row; if not, the last column says where to look. Fix it and repeat the row. Results from the first adapter and known limits are in [Adapter v1.0 notes](adapter_notes.md).

Stages 1 and 2 need a multimeter, a bench supply and a scope, and no Control Board: a fault found there costs an adapter, not the board. Stages 3 and 4 run on the Control Board with the `adapter` shell commands of [rethink-zmk-config](https://github.com/Ziemniaczenka/rethink-zmk-config) (`rethink-usb-shell` snippet).

## Conventions

- Net names follow the [schematic](../circuit/ReThink_adapter_Schematic.pdf), pads the [KiCad PCB](../circuit/ReThink_adapter/ReThink_adapter.kicad_pcb).
- The 3-pad solder jumpers come bridged 1-2 in copper and change only by cutting, so the tables take their defaults as given: U1 supply = LED_3V3, TP1_PWR = TP_5V, TP2_PWR = TP_3V3, TP1 lines through the level shifter, TP2 lines direct. Pads 1 and 3 are numbered on the silkscreen, pad 2 is the middle one.
- JP1-JP3 are open 2-pad jumpers, named by the net on each side.
- Not fitted: J9-J11 (2.54 mm test headers; fit pins to clip leads on), R23, C16, C21. Their empty pads are probe points.

## Probe points

| Net | Where |
| --- | --- |
| GND | Pin 2 of J9, J10, J11. Mounting holes H1-H4, H7, H8 |
| LED_3V3 (from the Control Board, always on) | J11 pin 1, JP10 pad 1 |
| U1 supply | JP10 pad 2 |
| TP_3V3 (switched by Control Board P3.12) | JP10 pad 3, JP7 pad 1, JP6 pad 3, JP1 TP_3V3 side |
| TP_5V (charge pump U2) | JP6 pad 1, JP7 pad 3 |
| PUMP_EN | JP1 PUMP_EN side |
| VIN (VLED_BL from the Control Board) | JP2 VIN side |
| BOOST_EN | JP2 BOOST_EN side |
| BL_5V (boost U4) | J10 pin 1, JP3 BL_5V side |
| FW_CLK / FW_DAT (Control Board side, 3.3 V) | JP8 pad 1, JP4 pad 3 / JP9 pad 1, JP5 pad 3 |
| LS_CLK / LS_DAT (level shifter, 5 V side) | JP8 pad 3, JP4 pad 1 / JP9 pad 3, JP5 pad 1 |
| PCA9306 VREF2/EN | C8, R5 |
| SCL / SDA / INT / RESET | R1 / R2 / R3 / R4, the pad not on the U1 supply |
| OUT1 (U1 P0_7, spare) | J9 pin 1 |
| TP1_RST / TP2_RST | C16 / R23 (empty pads), R14 / R22 |
| PWM | C21 (empty pad), R24 |
| Status LED lines, connector side | Mezzanine: R11 Caps Lock, R12 Power, R15 Mute, R16 Mic mute. FFC2: R17 Fn lock, R18 Mute, R19 Mic mute, R20 Caps Lock, R21 Num Lock |

U1's pins run 1-8 PUMP_EN, BOOST_EN, HOTKEY, PWRSWITCH, DRV15, DRV16, DRV17, OUT1; 9 VSS; 10-17 TP1_RST, TP2_RST, the five LED lines, KBD_BL_DTCT; 18 ADDR; 19-24 SCL, SDA, VDD(P), INT, VDD(I2C), RESET. Neighbours on this list are neighbours on the package, where solder bridges form.

On the Control Board: test points VLED1 (LED_3V3), TPV (TP_3V3), VBL (VLED_BL), TPD/TPC/TPI (SDA/SCL/INT), G1 (GND), and the 2.54 mm header JKB (pins 1-8 KSI0-7, 9-26 KSO0-17).

## 1. Unpowered, adapter alone

Multimeter in resistance mode. Rail readings climb while the capacitors charge: wait for them to settle.

| # | Measure | Pass | If not |
| --- | --- | --- | --- |
| 1.1 | LED_3V3, TP_3V3, TP_5V, VIN, BL_5V, each to GND | Kilohms or more | Short on that rail: its capacitors and IC pins |
| 1.2 | LED_3V3 to TP_3V3, TP_3V3 to TP_5V, VIN to BL_5V | Open | JP10 pads 2-3, U2, U4 |
| 1.3 | Across R1-R4 (SCL, SDA, INT, RESET to the U1 supply) | 10 kΩ each | 0 Ω: bridge on U1 pins 19-24 |
| 1.4 | SCL, SDA, INT, RESET to GND | Not a short (1.3 can't see this) | Bridge to U1's exposed pad |
| 1.5 | PUMP_EN to BOOST_EN | Open (stage 4 can't test this pair) | Bridge on U1 pins 1-2 |
| 1.6 | Across R6, R7 (FW lines to TP_3V3) and R8, R9 (LS lines to TP_5V) | 4.7 kΩ each | Bridge at U3 |
| 1.7 | PWM to GND | 100 kΩ (R24) | R24, R13, C22 |

## 2. Bench supply, adapter alone

Solder supply wires to J11 (LED_3V3), C3 (TP_3V3) and C9 (VIN), GND to pin 2 of J9-J11. Use these pads rather than jumper pads, which a wire could bridge. Start each channel with a low current limit and stop at any current well above the expected one.

Rows 2.2-2.9 switch the converters on by closing JP1 and JP2 with tweezers or a solder blob. No series resistor is needed: each jumper ties the enable to its converter's own supply. U1 is never configured on the bench, so its enable pins stay inputs.

> [!WARNING]
> Open JP1 and JP2 again before stage 3. The firmware drives PUMP_EN and BOOST_EN low, which shorts TP_3V3 or VLED_BL through U1 while a jumper is closed. Keep a jumper closed only together with its firmware option, `CONFIG_RETHINK_PUMP_EN_TIED` or `CONFIG_RETHINK_BOOST_EN_TIED`.

| # | Do | Pass | If not |
| --- | --- | --- | --- |
| 2.1 | LED_3V3 = 3.3 V, limit 10 mA, multimeter in series. TP_3V3 not connected | Up to ~0.5 mA, unsteady: U1's inputs float until the firmware gives them pull-ups. SCL, SDA, INT, RESET at 3.3 V. TP_3V3 (JP10 pad 3) under 0.1 V | Over 1 mA: fault on LED_3V3. A line low: back to 1.3-1.4. TP_3V3 up: something feeds it from LED_3V3 |
| 2.2 | Close JP1, then TP_3V3 = 3.3 V, limit 50 mA | TP_5V (JP6 pad 1) 4.8-5.2 V. VREF2/EN (C8) ~3.9 V. TP_3V3 current 0.1-0.2 mA | No TP_5V: U2, C5, JP1. VREF2 off: R5, U3 |
| 2.3 | 250 Ω (20 mA) from TP_5V to GND, scope TP_5V | 4.8 V or more, ripple in the tens of mV. TP_3V3 current about twice the load | U2 and its capacitors |
| 2.4 | FW_CLK (JP8 pad 1) to GND, then LS_DAT (JP9 pad 3) to GND | LS_CLK (JP8 pad 3), then FW_DAT (JP9 pad 1) follow to ~0 V and return when released | U3 pins, VREF2 |
| 2.5 | Open JP1 | TP_5V back to 0 V within milliseconds | U2 |
| 2.6 | VIN = 3.3 V, limit 0.5 A, JP2 open | BL_5V (J10) 0 V, VIN current under 1 µA | U4, BOOST_EN |
| 2.7 | Close JP2 with the limit at 1 A, scoping VIN, BL_5V and the VIN current (probe, or 0.1 Ω shunt) | BL_5V 4.93-5.07 V. At start, U4 precharges BL_5V's 64 µF at up to ~1 A, then soft-starts in ~1 ms. Note the peak: BUCK1 sees it in 4.8 | U4, L1 |
| 2.8 | 50 Ω (100 mA, 0.5 W) on J10 | BL_5V in tolerance, VIN ~0.17 A (BUCK1 gives 200 mA at most) | U4, L1, output capacitors |
| 2.9 | Open JP2. Check that JP1 and JP2 read open | BL_5V falls to 0 V in under a second (R10 through U4's PG) | R10 |

## 3. Cables and first power-up

| # | Do | Pass | If not |
| --- | --- | --- | --- |
| 3.1 | Both cables in, unpowered. Control Board to adapter: G1 to J11 pin 2, VLED1 to J11 pin 1, TPV to JP10 pad 3, VBL to JP2 VIN side, JKB 25 / 24 to JP8 / JP9 pad 1 | 0 Ω each; VBL to GND not a short | Cable orientation, connector contacts |
| 3.2 | Flash `rethink_hw_tester-rethink-usb-shell` onto the bare Control Board. Connect the adapter, power over USB through a USB meter, no battery | Bare board current plus under 1 mA. U1-U4 stay cool | Unplug, back to stage 1 |
| 3.3 | Open the board's USB serial port (any baud rate) | `ReThink adapter found (gpio@20)`, the LED self-test, and `Backlight locked` (expected without a backlit keyboard) | `not found`: SDA, SCL, U1 supply, RESET, U1 pins |

Without a battery, ZMK logs `Failed to fetch battery values: -11` every 10 s. It's harmless.

## 4. Firmware tests, no keyboard

Rows 4.1-4.5 look for shorts: they read pins, pull single lines low against pull-ups and turn on TP_3V3, already checked in stage 2. Fix what they find before 4.6, where the commands start driving pins high and switching supplies. The `adapter` commands bypass the backlight interlock: never use them with a keyboard connected.

| # | Do | Pass | If not |
| --- | --- | --- | --- |
| 4.1 | `i2c scan i2c@c8000` | Only 0x20 | ADDR (U1 pin 18) |
| 4.2 | `adapter status`, scoping SCL and SDA | Rise time (30-70 %) under 300 ns | Lower R1/R2 or the bus speed |
| 4.3 | `adapter tp on` (TP_3V3 is off from boot) | TP_3V3 3.3 V | P3.12 switch, TPV continuity |
| 4.4 | `adapter in` | HOTKEY, PWRSWITCH, KBD_BL_DTCT high | Low: shorted to GND, or bridged to BOOST_EN if it reads high after `adapter boost on` (then `adapter boost off`). Don't drive a bridged line |
| 4.5 | `adapter shorts` | `No shorts between the 40 lines`. TP1_RST low at rest (pump off) is expected | A pair: bridge on U1 or a connector. Low at rest: as 4.4 |
| 4.6 | `adapter pump on`, then `off` | TP_5V 5 V, then 0 V | PUMP_EN, U2 |
| 4.7 | `adapter vled on` | VIN 3.3 V, BL_5V still 0 V | P3.11, BUCK1, VBL continuity |
| 4.8 | `adapter boost on`, scoping VIN and BL_5V | BL_5V 5 V, the board doesn't reset | Reset: U4's inrush is too much for BUCK1 |
| 4.9 | `adapter pwm 50` | PWM (C21): 4096 Hz, 0-3.3 V, duty at most the configured maximum | JKB 26 continuity, R13 |
| 4.10 | `adapter pwm 0`, `adapter boost off`, `adapter vled off` | BL_5V and VIN 0 V | |
| 4.11 | `adapter pin <led> u`, then `0`, then `z`, for ledpwr, ledmute, ledmicmute, ledcpslock, lednumlock | Connector side of the LED's resistor: 3.3 V, then 0 V | U1 pin open, the resistor |
| 4.12 | `adapter pin <pin> 0`, then `1`, for out1, drv15, drv16, drv17 | 0 V, then 3.3 V on J9 pin 1, Mezzanine 30, FFC2 cable 36 and 37 | U1 pin open |
| 4.13 | `adapter pump on`, `adapter pin tp1_rst 0`, then `z` | C16: 0 V, then 5 V | R14, U1 pin |
| 4.14 | `adapter pin tp2_rst 0`, then `z` | R23: 0 V, then 3.3 V | R22, U1 pin |
| 4.15 | `adapter in` while shorting each input to GND: HOTKEY on Mezzanine 1, PWRSWITCH on Mezzanine 19, KBD_BL_DTCT on J8 12 | The shorted input reads low | U1 pin open |
| 4.16 | `adapter int`, then short an input to GND within 15 s | `INT went low ... released after reading them` | R3, TPI continuity |
| 4.17 | `adapter pump off`, `adapter tp off` | TP_3V3 0 V | |
| 4.18 | Optional, with a battery: wired mode, unplug USB, measure the battery current | Bare board plus a few µA | A pin between the rails: ground candidates one at a time and watch the current |

`adapter shorts` drives the 40 lines to the keyboard connectors low one at a time while the others have pull-ups: SENSE0-7, DRV0-14, FW_CLK/FW_DAT, INT, and the expander's DRV15-17, OUT1, TP1/TP2_RST, LED lines and KBD_BL_DTCT. It finds bridges anywhere along them, connectors included, but not open pins: rows 4.11-4.15 cover those.
