# PCAL6416A IO expander

ReThink Adapter U1: 16-bit I2C IO expander for the keyboard signals the Control Board has no pins for (extra matrix drive lines, direct keys, status LEDs, pointing stick reset, power enables).

## Part

- MPN: NXP PCAL6416AHF (HVQFN24, 4x4mm)
  - [Datasheet](https://www.nxp.com/docs/en/data-sheet/PCAL6416A.pdf)
- I2C address: **0x20** (ADDR to GND)
- Bus: Control Board touchpad I2C (Zephyr `&i2c22`)
  - SDA: P3.08 (CB pin 30, AB pin 5)
  - SCL: P3.04 (CB pin 31, AB pin 4)
  - Pull-ups: R1, R2 10k to the U1 supply
- ~INT: P3.06 (CB pin 33 TP_INT, AB pin 2), pull-up R3 10k
- ~RESET: pull-up R4 10k, not connected to the Control Board
- Supply (VDD(P), VDD(I2C-bus) and all pull-ups above): selected by JP10
  - 1-2 **LED_3V3** (default): always on
  - 2-3 TP_3V3: switched by the Control Board (P3.12)
- Both ports configured as push-pull, open drain achieved by switching pin to input.

## Pinout

Connector columns give the keyboard cable pin numbers used in the connector pages ([Mezzanine](mezzanine.md), [FFC1](ffc1.md), [FFC2](ffc2.md)).

|  Pin  | Port  |     Net     | Direction  |      Active      |   Mezzanine   |  FFC1  |     FFC2      |                              Function                               |
| :---: | :---: | :---------: | :--------: | :--------------: | :-----------: | :----: | :-----------: | :-----------------------------------------------------------------: |
|   1   | P0_0  |   PUMP_EN   |    Out     |   High = 5V on   |       -       |   -    |       -       |        LM2775 charge pump (TP_5V) enable, R25 100k pull-down        |
|   2   | P0_1  |  BOOST_EN   |    Out     | High = BL_5V on  |       -       |   -    |       -       |                TPS610333 backlight boost (U4) enable                |
|   3   | P0_2  |   HOTKEY    |     In     |  Low = pressed   |       1       |   -    |  29 (36/40)   |                     Fn key, outside the matrix                      |
|   4   | P0_3  |  PWRSWITCH  |     In     |  Low = pressed   |      19       |   -    |       -       |                            Power button                             |
|   5   | P0_4  |    DRV15    |    Out     |        -         |      30       | 7 (30) |  18 (36/40)   |                        Matrix drive line 15                         |
|   6   | P0_5  |    DRV16    |    Out     |        -         |       -       |   -    |  36 (36/40)   |            Matrix drive line 16 (KBD_ID on T480 36-pin)             |
|   7   | P0_6  |    DRV17    |    Out     |        -         |       -       |   -    |    37 (40)    |               Matrix drive line 17 (numpad keyboards)               |
|   8   | P0_7  |    OUT1     |    Out     |        -         |       -       |   -    |       -       |                    Spare, J9 pin 1 (not fitted)                     |
|  10   | P1_0  |   TP1_RST   | Open-drain |   High = reset   |      40       | 2 (8)  |       -       |          Pointing stick reset, R14 10k pull-up to TP1_PWR           |
|  11   | P1_1  |   TP2_RST   | Open-drain |   High = reset   |       -       |   -    |    3 (12)     | Pointing stick reset, R22 10k pull-up to TP2_PWR (or R23 pull-down) |
|  12   | P1_2  |   LEDPWR    | Open-drain |    Low = lit     | 23 (R12 220R) |   -    | 26 (R17 100R) |              Power LED (Mezzanine), Fn lock LED (FFC2)              |
|  13   | P1_3  |   LEDMUTE   | Open-drain |    Low = lit     | 33 (R15 3.9k) |   -    | 27 (R18 100R) |                              Mute LED                               |
|  14   | P1_4  | LEDMICMUTE  | Open-drain |    Low = lit     | 36 (R16 3.9k) |   -    | 28 (R19 100R) |                            Mic mute LED                             |
|  15   | P1_5  | LEDCPSLOCK  | Open-drain |    Low = lit     | 21 (R11 560R) |   -    | 31 (R20 100R) |        Caps Lock LED; **KBD_BL_DTCT on T430** (Mezzanine 21)        |
|  16   | P1_6  | LEDNUMLOCK  | Open-drain |    Low = lit     |       -       |   -    | 38 (R21 100R) |               Num Lock LED (40-pin numpad keyboards)                |
|  17   | P1_7  | KBD_BL_DTCT |     In     | Low = backlit kb |       -       |   -    |    11 (12)    |         Backlight detection, read with the internal pull-up         |

Notes:
- "Open-drain": the pin either sinks or is left as an input. The firmware switches between output-low and input, because the Zephyr PCAL64xxA driver does not accept `GPIO_OPEN_DRAIN`.
- TP2_RST with R23 (pull-down) instead of R22: reset is asserted by driving P1_1 high (push-pull), and only while TP2_PWR is on, so the pin does not back-power the pointing stick.
- The LED pins are shared between connectors: LEDPWR drives Mezzanine 23 and FFC2 26 at the same time, and so on.
- After power-up or reset all pins are inputs, so PUMP_EN (R25) and TP1/TP2_RST (pull-ups) start in their safe states. BOOST_EN has no pull resistor on the adapter.

## Use per keyboard

| Keyboard  |  Connector  |            Status LEDs             |  KBD_BL_DTCT  | Expander drive lines |    Direct keys    |  Reset  |
| :-------: | :---------: | :--------------------------------: | :-----------: | :------------------: | :---------------: | :-----: |
|    T60    |  Mezzanine  |         - (pin 36 is GND)          |       -       |        DRV15         | HOTKEY, PWRSWITCH | TP1_RST |
|   T420    |  Mezzanine  |   PWR, Caps Lock, Mute, Mic mute   |       -       |        DRV15         | HOTKEY, PWRSWITCH | TP1_RST |
|   T430    |  Mezzanine  |        PWR, Mute, Mic mute         | P1_5 (pin 21) |        DRV15         | HOTKEY, PWRSWITCH | TP1_RST |
|   L420    |    FFC1     |                 -                  |       -       |        DRV15         |         -         | TP1_RST |
|   T480    | FFC2 36-pin | Fn lock, Mute, Mic mute, Caps Lock | P1_7 (12-pin) | DRV15 (16 = KBD_ID)  |      HOTKEY       | TP2_RST |
| T580, L14 | FFC2 40-pin |  as T480, + Num Lock with numpad   | P1_7 (12-pin) |     DRV15-DRV17      |      HOTKEY       | TP2_RST |

## Jumpers and assembly options

Firmware options are set in `config/rethink.conf` of the ZMK configuration.

| Jumper/part  |             Default             |                 Alternative                  |           Firmware option           |
| :----------: | :-----------------------------: | :------------------------------------------: | :---------------------------------: |
|     JP10     |       1-2 U1 from LED_3V3       |              2-3 U1 from TP_3V3              | `CONFIG_RETHINK_EXPANDER_SUPPLY_*`  |
|     JP1      |              open               |        closed: PUMP_EN tied to TP_3V3        |    `CONFIG_RETHINK_PUMP_EN_TIED`    |
|     JP2      |              open               |    closed: BOOST_EN tied to VIN (VLED_BL)    |   `CONFIG_RETHINK_BOOST_EN_TIED`    |
|     JP3      |              open               |      closed: BL_5V to Mezzanine pin 29       |   none (backlit T430-class only)    |
|     JP6      |       1-2 TP1_PWR = TP_5V       |             2-3 TP1_PWR = TP_3V3             |    `CONFIG_RETHINK_TP1_SUPPLY_*`    |
|   JP4, JP5   |    1-2 TP1 via level shifter    |        2-3 TP1 direct (with JP6 2-3)         |             follows JP6             |
|     JP7      |      1-2 TP2_PWR = TP_3V3       |             2-3 TP2_PWR = TP_5V              |    `CONFIG_RETHINK_TP2_SUPPLY_*`    |
|   JP8, JP9   |         1-2 TP2 direct          |   2-3 TP2 via level shifter (with JP7 2-3)   |             follows JP7             |
|  R22 / R23   |       R22 pull-up fitted        |            R23 pull-down instead             |  `CONFIG_RETHINK_TP2_RESET_PULL_*`  |
|      U4      |       fitted (Full, FFC2)       |        not fitted (Mezz_no_BL, FFC1)         |    `CONFIG_RETHINK_BOOST_FITTED`    |
| CB R62 / R59 | R62: VLED_BL from BUCK1 (3.3 V) | R59: VLED_BL from VBAT; VSYS (next revision) | `CONFIG_RETHINK_BACKLIGHT_SUPPLY_*` |

> Warning: with JP1 or JP2 closed, the matching expander pin must stay an input, otherwise it drives against the supply. Set the firmware option before closing the jumper.
