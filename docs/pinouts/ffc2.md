# FFC 2 connector

Modern 6-row keyboard\
Dual keyed FFC connectors:
- 36-pin (40-pin with numpad) P0.5mm keyed for Matrix, LEDs, Navigation Buttons
- 12-pin P1.0mm keyed for Pointing Stick and Backlight

## Compatible connectors

- 36-pin:
  - HIGHS_FC5AF361-1151H (T470)
- 40-pin:
  - JAE-CON40-7-GP (T570)
  - HIGHS_FC5AF401-3181H (L14g1, L15g1, E480, E580)
- 12-pin:
  - HIGHS_FC1AF121-1151H (T480, L14G1)
  - JAE-CON12-1-GP-U (T580)
  - JAE_FL10F012HA1R3000 (E490)


## Compatible models (TBD)

- T470, T480, T25 (w/o power button), A475, A485 (36pin)
- T570, T580, P51s, P52s (40pin)
- L14g1, L14g2 (40pin)
- L15g1, L15g2 (40pin)
- E480, E485, E490, E495, L380, L390, L480, L490, T480s, T490, T14g1, T14g2, P43, P43s, P14sG1, P14sG2 (40pin)
- E580, E585, E590, E595, L580, L590, T590, P52, P53, P53s, P72, P73 (40pin)
- T15g1, T15g2, P15g1, P15g2, P17g1, P17g2 (40pin)

## Pinout (30-pin)

| Pin (CB) |     T480     |   T580/L14   |                      Type                       | Adapter Board |
| :------: | :----------: | :----------: | :---------------------------------------------: | :-----------: |
|    1     |    SENSE3    |    SENSE3    |                                                 |               |
|    2     |    SENSE7    |    SENSE7    |                                                 |               |
|    3     |    SENSE6    |    SENSE6    |                                                 |               |
|    4     |    DRV14     |    DRV14     |                                                 |               |
|    5     |    SENSE4    |    SENSE4    |                                                 |               |
|    6     |    SENSE1    |    SENSE1    |                                                 |               |
|    7     |     DRV0     |     DRV0     |                                                 |               |
|    8     |    SENSE2    |    SENSE2    |                                                 |               |
|    9     |    SENSE0    |    SENSE0    |                                                 |               |
|    10    |     DRV4     |     DRV4     |                                                 |               |
|    11    |     DRV2     |     DRV2     |                                                 |               |
|    12    |    SENSE5    |    SENSE5    |                                                 |               |
|    13    |     DRV1     |     DRV1     |                                                 |               |
|    14    |     DRV3     |     DRV3     |                                                 |               |
|    15    |     DRV6     |     DRV6     |                                                 |               |
|    16    |     DRV7     |     DRV7     |                                                 |               |
|    17    |     DRV5     |     DRV5     |                                                 |               |
|    18    |    DRV15     |    DRV15     |                                                 |               |
|    19    |    DRV13     |    DRV13     |                                                 |               |
|    20    |     DRV9     |     DRV9     |                                                 |               |
|    21    |    DRV12     |    DRV12     |                                                 |               |
|    22    |    DRV10     |    DRV10     |                                                 |               |
|    23    |     DRV8     |     DRV8     |                                                 |               |
|    24    |    DRV11     |    DRV11     |                                                 |               |
|    25    |    VCC3M     |    VCC3M     |                                                 |               |
|    26    |  LED_FNLOCK  |  LED_FNLOCK  |                                                 |               |
|    27    |   LED_MUTE   |   LED_MUTE   |                                                 |               |
|    28    | LED_MICMUTE  | LED_MICMUTE  |                                                 |               |
|    29    |    HOTKEY    |    HOTKEY    |                                                 |               |
|    30    |     GND      |     GND      |                                                 |               |
|    31    | LED_CAPSLOCK | LED_CAPSLOCK |                                                 |               |
|    32    |     GND      |     GND      |                                                 |               |
|    33    |   TP4LEFT    |   TP4LEFT    |                                                 |               |
|    34    |   TP4RIGHT   |   TP4RIGHT   |                                                 |               |
|    35    |  TP4MIDDLE   |  TP4MIDDLE   |                                                 |               |
|    36    |    KBD_ID    |    DRV16     | KBD_ID NC on 01AX516, NC on non-numpad L14 etc. |               |
|    37    |   GND (MP)   |    DRV17     |            NC on non-numpad L14 etc.            |               |
|    38    |   GND (MP)   | LED_NUMLOCK  |            NC on non-numpad L14 etc.            |               |
|    39    |      -       |      NC      |                  Not Connected                  |               |
|    40    |      -       |      NC      |                  Not Connected                  |               |
|    41    |      -       |   GND (MP)   |                 Mounting Point                  |               |
|    42    |      -       |   GND (MP)   |                 Mounting Point                  |               |




## Pinout (8-pin)

|  Pin  |    T480     |    T580     |     L14     |                Type                 | Adapter Board |
| :---: | :---------: | :---------: | :---------: | :---------------------------------: | :-----------: |
| **1** |  **VCC5B**  |  **VCC5B**  |  **VCC3B**  | option of 3V3 and 5V, diff defaults |               |
|   2   |   TP4DATA   |   TP4DATA   |   TP4DATA   |                                     |               |
|   3   |  TP4_RESET  |  TP4_RESET  |  TP4_RESET  | Pointing Stick reset, Pullup 10k@5V |               |
|   4   |  TP4MIDDLE  |  TP4MIDDLE  |  TP4MIDDLE  |                                     |               |
|   5   |  TP4RIGHT   |  TP4RIGHT   |  TP4RIGHT   |                                     |               |
|   6   |   TP4LEFT   |   TP4LEFT   |   TP4LEFT   |                                     |               |
|   7   |     GND     |     GND     |     GND     |         Pointing Stick GND          |               |
|   8   |   TP4CLK    |   TP4CLK    |   TP4CLK    |         Pointing Stick Clk          |               |
|   9   |    VCC5B    |    VCC5B    |    VCC5B    |            LED VCC (5V)             |               |
|  10   | KBD_BL_PWM  | KBD_BL_PWM  | KBD_BL_PWM  |               LED PWM               |               |
|  11   | KBD_BL_DTCT | KBD_BL_DTCT | KBD_BL_DTCT |       Backlight detection(?)        |               |
|  12   |     GND     |     GND     |     GND     |               LED GND               |               |
|  13   |  GND (MP)   |  GND (MP)   |  GND (MP)   |           Mounting Point            |               |
|  14   |  GND (MP)   |  GND (MP)   |  GND (MP)   |           Mounting Point            |               |

