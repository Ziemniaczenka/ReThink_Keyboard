# Adapter v1.0 notes

Measurements on the first assembled adapter, what to check when something misbehaves, and points for a next revision. The test procedure is [Adapter bring-up](adapter_bringup.md).

## Measured

First adapter (Full variant) on the Control Board, no keyboard unless stated.

| What | Result | Verdict |
| --- | --- | --- |
| I2C rise time (30-70 %), 400 kHz, R1/R2 10 kΩ | SCL 300 ns, SDA 270 ns. The high level reaches about 3.1 V before the next edge | Works, at the Fast-mode limit (300 ns). Scope: ZOYI ZT-703S, 10× probe |
| Charge pump U2, 220 Ω on TP_5V (23 mA) | 5.0 V, ripple under 6 mV | Good |
| Boost U4 start on BUCK1, no load | VIN swings between 3.3 V and 1.7 V for about 1 ms (U4 precharges BL_5V), then steady. The board keeps running | Works, BUCK1 briefly overloaded |
| Boost U4 from a 3.3 V bench supply, 33 Ω on BL_5V (about 150 mA) | 5.0 V steady, ripple about 40 mV | Good: U4 itself delivers 150 mA |
| Boost U4 on BUCK1, 100 Ω on BL_5V (50 mA) | VIN and BL_5V steady at nominal. Ripple: VIN about 240 mV, BL_5V about 50 mV | Good |
| Boost U4 on BUCK1, 47 Ω on BL_5V (about 106 mA) | VIN drops to 2.1 V in frequent spikes, BL_5V is a 2.9-3.6 V sawtooth, coil whine | Fails. U4 handles more on the bench, so the VLED_BL path can't supply the ~0.19 A U4 needs: BUCK1's 200 mA limit, or the drop across Q3 and the cable |
| System OFF, wired power-off on battery | 0.000 mA on the multimeter's mA range, as the bare board | Good, with every idle U1 pin on a pull (`idle-gpios`). Floating, U1 drew about 0.5 mA, TP2_RST alone about 100 µA |
| Stick switched on from a weak source | E580 (3.3 V stick, TP2) from a bench supply through a multimeter's mA range: the board resets at every start below 3.8 V and starts again, a boot loop; from the EFM32 kit's 3.3 V the same. With 100 µF across the battery input at the board, it works down to 3.2 V. T420 (5 V stick, charge pump): from a good 1000 mAh cell at 3.15 V it works, through the meter's mA range it resets, on its 10 A range it works; from a worn 400 mAh cell (about 350 mΩ) it resets at 3.45 V; on the EFM32 kit it needs 1000 µF across the input. 100 µF on LED_3V3 (BUCK2's output) instead: the board doesn't start | The switch-on surge (TP_3V3, about 10-20 µF at once through Control Board Q2) is too fast for the supply's path; see [For a next revision](#for-a-next-revision) |
| Two Norwegian L420 keyboards on FFC1, `rethink_scanner` | First: no key on SENSE6/SENSE7 (J4 pins 28/29) on either keyboard. After reworking all J4 pins: all 85 keys on one keyboard, all but Enter (SENSE6 × DRV10) on the other | J4 joints were open. The pinout matches the L420 schematic (CN5) |

Current with each keyboard, by FRU: [Keyboard power](keyboard_power.md).

Still to measure:
- The largest BL_5V load on BUCK1, between 50 mA (works) and 106 mA (fails): 68 Ω (74 mA), with VBL on the Control Board and VIN on the adapter measured together to split BUCK1's sag from the drop across Q3 and the cable.
- Backlight current of real keyboards (T430, T480 class), at full brightness and at the PWM duty limit.
- How worn a cell may get before the stick's switch-on resets the board (a good cell works at 3.15 V, a worn one fails at 3.45 V): VBAT and the 3.3 V rail with a scope at Fn+F8, with the E580 (3.3 V stick) and the T420 (5 V stick, behind the charge pump).

## If something doesn't work

| Symptom | Check |
| --- | --- |
| Expander not found, or I2C errors now and then | Rise time is at the limit: run i2c22 at 100 kHz (`clock-frequency = <I2C_BITRATE_STANDARD>`) or fit 4.7 kΩ for R1/R2 |
| Board resets or the backlight flickers when it switches on | U4's precharge pulls VLED_BL down. Lower the load, or feed VLED_BL from VSYS (Control Board resistor option, `CONFIG_RETHINK_BACKLIGHT_SUPPLY_VSYS`) |
| Backlight dim or whining at high brightness | VLED_BL overloaded: lower `CONFIG_RETHINK_BACKLIGHT_MAX_DUTY`, or VSYS as above |
| System OFF current above a few µA | A U1 pin between the rails: a keyboard pin not covered by its shield's `idle-gpios`, or firmware without them. Ground candidates one at a time and watch the current |
| HOTKEY, PWRSWITCH, DRV15-17 dead or acting together | U1 pins 3-7: bridges or opens at the HVQFN24 (bring-up 4.4, 4.5, 4.12, 4.15) |
| A whole SENSE row missing on every keyboard of one connector | An open joint on that connector's SENSE pin: see bring-up 5.7 |
| Board resets when the stick switches on (boot loop, or at Fn+F8), on a bench supply, a profiler or a worn cell | The switch-on surge through the source's resistance: a multimeter on its 10 A range or bridged, or a reservoir capacitor (low leakage) across the battery input at the board (100 µF on the bench, 1000 µF for the T420 on the EFM32 kit); a worn cell needs replacing. The firmware leaves the stick off after such a reset, until USB power or Fn+F8, and goes to ship mode after 3 resets in a row on battery |
| Pointing stick doesn't start | TP_3V3 is off from boot; PUMP_EN only with TP_3V3 on; TP1/TP2_RST rest on pull-downs until the TrackPoint support drives them |

## For a next revision

- **I2C pull-ups:** 4.7 kΩ for R1/R2 gives margin at 400 kHz.
- **PUMP_EN across resets:** U1 stays powered from LED_3V3 and keeps PUMP_EN high when the Control Board resets, while TP_3V3 may drop with P3.12. Until the firmware rewrites U1 (bootloader time included), the LM2775's EN sits above its supply (rating: VIN + 0.3 V). A series resistor of about 10 kΩ between U1 P0_0 and U2 EN limits the current; with R25 (100 kΩ) EN still reaches about 3 V.
- **Boost input:** U4 precharges BL_5V's 64 µF at up to ~1 A, more than BUCK1 delivers, and VIN ripples about 240 mV at a 50 mA load. More input capacitance on VIN (C9 is 10 µF) helps both. Other options: less capacitance on BL_5V, or a boost with a gentler start.
- **TP_3V3 switch-on:** Control Board Q2 switches TP_3V3 on within tens of nanoseconds (gate pulled down through 1 kΩ), so C3 (10 µF) and the stick's capacitors charge at once: a surge of a few hundred mA from the battery input, which a bench supply through a multimeter, a profiler or a worn cell can't deliver (a good cell can, down to 3.15 V). The prerelease bootloader on early Control Boards switches TP_3V3 on at every power-up (P3.12 high while it runs): from a weak source a boot loop before the firmware runs, until the bootloader is updated. The load switch below covers that too. The firmware can't soften it. Options, best first: a load switch with a set rise time (e.g. TPS22917 or TPS22918, SOT-23-6, about 1 ms) in front of the stick and the pump, switched on by TP_3V3 itself, with C3 behind it and about 1 µF in front (about 70 mA at switch-on). Not a reservoir on LED_3V3 (BUCK2's output): with 100 µF there the board doesn't start. A 5 V stick adds the charge pump's start (TP_5V through the doubler): less capacitance on TP_5V, or a 5 V boost with a set soft start instead of the pump. Decide after the measurement above. Details: [Pointing stick switch-on surge](https://github.com/Ziemniaczenka/rethink-zmk-config/blob/main/docs/power.md#pointing-stick-switch-on-surge) in the firmware repository.
- **VLED_BL source:** decide between BUCK1 and VSYS once real backlight currents are known. On BUCK1, 50 mA at 5 V runs cleanly and about 106 mA fails.
- **U1 package:** two sides of the HVQFN24 bridged at hand assembly and were hard to inspect. The TSSOP24 version (PCAL6416APW, 0.65 mm pitch) is easier to solder and check, or reduce the stencil apertures for the QFN.
- **Test pads:** J9-J11 and the jumper pads worked well as probe points; pads for SCL, SDA and INT would save probing R1-R3.
