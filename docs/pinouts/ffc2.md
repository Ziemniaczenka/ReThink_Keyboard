# FFC 2 connector

Modern 6-row keyboard\
Dual keyed FFC connectors:
- 36-pin (40-pin with numpad) P0.5mm keyed for Matrix, LEDs, Navigation Buttons
- 12-pin P1.0mm keyed for Pointing Stick and Backlight

## Compatible connectors

1. 36-pin
   - pitch: 0.5mm
   - key: **notched**
   - side: bottom
   - lock: yes?
   - Compatible MPN:
     - HIGHS_FC5AF361-1151H (T470)
     - Hirose FH34SRJ-40S-0.5SH(50) (**40pin, straight key. Skip 2 pins from each end!**)
       - [Mouser](https://www.mouser.pl/en/ProductDetail/Hirose-Connector/FH34SRJ-40S-0.5SH50?qs=iyLo5FA4poDa6AcLdJDWMw%3D%3D)
2. 40-pin
   - pitch: 0.5mm
   - key: **tabbed**
   - side: bottom
   - lock: yes?
   - Compatible MPN:
     - JAE-CON40-7-GP (T570)
     - HIGHS_FC5AF401-3181H (L14g1, L15g1, E480, E580)
     - Hirose FH52-40S-0.5SH (**direct match**)
       - [Mouser](https://www.mouser.pl/en/ProductDetail/Hirose-Connector/FH52-40S-0.5SH?qs=x%2FqqGkZFGGusKc6kcNGZEQ%3D%3D)
3. 12-pin
   - pitch: 1.0mm
   - key: **notched**
   - side: bottom
   - lock: yes?
   - Compatible MPN:
     - HIGHS_FC1AF121-1151H (T480, L14G1)
     - JAE-CON12-1-GP-U (T580)
     - JAE_FL10F012HA1R3000 (E490)
     - Omron XF3M(1)-1415-1B (**14pin, straight key. Skip 1 pin from each end, needs aligment guide!**)
       - [Mouser](https://www.mouser.pl/en/ProductDetail/Omron-Electronics/XF3M1-1415-1B?qs=0q6jlcGHEi2cMtnOEJgNDA%3D%3D)


## Compatible models (TBD)

- T470, T480, T25 (w/o power button), A475, A485 (36pin)
- T570, T580, P51s, P52s (40pin)
- L14g1, L14g2 (40pin)
- L15g1, L15g2 (40pin)
- E480, E485, E490, E495, L380, L390, L480, L490, T480s, T490, T14g1, T14g2, P43, P43s, P14sG1, P14sG2 (40pin)
- E580, E585, E590, E595, L580, L590, T590, P52, P53, P53s, P72, P73 (40pin)
- T15g1, T15g2, P15g1, P15g2, P17g1, P17g2 (40pin)

## Pinout (36-pin/40pin)

|  Pin  |     T480     |   T580/L14   |                         Type                          | Adapter Board |
| :---: | :----------: | :----------: | :---------------------------------------------------: | :-----------: |
|   1   |    SENSE3    |    SENSE3    |                                                       |               |
|   2   |    SENSE7    |    SENSE7    |                                                       |               |
|   3   |    SENSE6    |    SENSE6    |                                                       |               |
|   4   |    DRV14     |    DRV14     |                                                       |               |
|   5   |    SENSE4    |    SENSE4    |                                                       |               |
|   6   |    SENSE1    |    SENSE1    |                                                       |               |
|   7   |     DRV0     |     DRV0     |                                                       |               |
|   8   |    SENSE2    |    SENSE2    |                                                       |               |
|   9   |    SENSE0    |    SENSE0    |                                                       |               |
|  10   |     DRV4     |     DRV4     |                                                       |               |
|  11   |     DRV2     |     DRV2     |                                                       |               |
|  12   |    SENSE5    |    SENSE5    |                                                       |               |
|  13   |     DRV1     |     DRV1     |                                                       |               |
|  14   |     DRV3     |     DRV3     |                                                       |               |
|  15   |     DRV6     |     DRV6     |                                                       |               |
|  16   |     DRV7     |     DRV7     |                                                       |               |
|  17   |     DRV5     |     DRV5     |                                                       |               |
|  18   |    DRV15     |    DRV15     |                                                       |               |
|  19   |    DRV13     |    DRV13     |                                                       |               |
|  20   |     DRV9     |     DRV9     |                                                       |               |
|  21   |    DRV12     |    DRV12     |                                                       |               |
|  22   |    DRV10     |    DRV10     |                                                       |               |
|  23   |     DRV8     |     DRV8     |                                                       |               |
|  24   |    DRV11     |    DRV11     |                                                       |               |
|  25   |    VCC3M     |    VCC3M     |                      0.1u to GND                      |               |
|  26   |  LED_FNLOCK  |  LED_FNLOCK  |           100R series resistor, 0.1u to GND           |               |
|  27   |   LED_MUTE   |   LED_MUTE   |         100R series resistor,    0.1u to GND          |               |
|  28   | LED_MICMUTE  | LED_MICMUTE  |           100R series resistor, 0.1u to GND           |               |
|  29   |    HOTKEY    |    HOTKEY    |                                                       |               |
|  30   |     GND      |     GND      |                                                       |      GND      |
|  31   | LED_CAPSLOCK | LED_CAPSLOCK |         100R series resistor,    0.1u to GND          |               |
|  32   |     GND      |     GND      |                                                       |      GND      |
|  33   |   TP4LEFT    |   TP4LEFT    |                                                       |               |
|  34   |   TP4RIGHT   |   TP4RIGHT   |                                                       |               |
|  35   |  TP4MIDDLE   |  TP4MIDDLE   |                                                       |               |
|  36   |  **KBD_ID**  |  **DRV16**   | KBD_ID NC on 01AX516, <br/> NC on non-numpad L14 etc. |               |
|  37   |      -       |    DRV17     |               NC on non-numpad L14 etc.               |               |
|  38   |      -       | LED_NUMLOCK  |    NC on non-numpad L14 etc, 100R series resistor     |               |
|  39   |      -       |      NC      |                     Not Connected                     |               |
|  40   |      -       |      NC      |                     Not Connected                     |               |




## Pinout (12-pin)

|  Pin  |    T480     |    T580     |     L14     |                              Type                              | Adapter Board |
| :---: | :---------: | :---------: | :---------: | :------------------------------------------------------------: | :-----------: |
| **1** |  **VCC5B**  |  **VCC5B**  |  **VCC3B**  | VCC_TP, 10nF to GND  <br/> option of 3V3 and 5V, diff defaults |               |
|   2   |   TP4DATA   |   TP4DATA   |   TP4DATA   |            Pointing Stick Data, Pullup 4.7k@VCC_TP             |               |
|   3   |  TP4_RESET  |  TP4_RESET  |  TP4_RESET  |            Pointing Stick reset, Pullup 10k@VCC_TP             |               |
|   4   |  TP4MIDDLE  |  TP4MIDDLE  |  TP4MIDDLE  |                                                                |               |
|   5   |  TP4RIGHT   |  TP4RIGHT   |  TP4RIGHT   |                                                                |               |
|   6   |   TP4LEFT   |   TP4LEFT   |   TP4LEFT   |                                                                |               |
|   7   |     GND     |     GND     |     GND     |                       Pointing Stick GND                       |               |
|   8   |   TP4CLK    |   TP4CLK    |   TP4CLK    |                Pointing Stick Clk, 4.7k@VCC_TP                 |               |
|   9   |    VCC5B    |    VCC5B    |    VCC5B    |                  LED VCC (5V), 2x22uF to GND                   |               |
|  10   | KBD_BL_PWM  | KBD_BL_PWM  | KBD_BL_PWM  |                      LED PWM, 220p to GND                      |               |
|  11   | KBD_BL_DTCT | KBD_BL_DTCT | KBD_BL_DTCT |                      Backlight detection                       |               |
|  12   |     GND     |     GND     |     GND     |                            LED GND                             |               |

