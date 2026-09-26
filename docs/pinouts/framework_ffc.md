# Framework Control Board FFC connectors

34-pin FFC connector for data as well as 6-pin for Backlight power  

## Compatible connectors

1. 34-pin
   - pitch: 0.5mm
   - key: straight
   - side: dual?
   - lock: back
   - Compatible MPN:
     - Hirose FH34SRJ-34S-0.5SH(50)?
       - [Mouser](https://www.mouser.pl/en/ProductDetail/Hirose-Connector/FH34SRJ-34S-0.5SH50?qs=iyLo5FA4poAumYnqXazWvw%3D%3D)
2. 6-pin
   - pitch: 0.5mm
   - key: straight
   - side: dual?
   - lock: back
   - Compatible MPN:
     - Hirose FH34SRJ-6S-0.5SH(50)?
       - [Mouser](https://www.mouser.pl/en/ProductDetail/Hirose-Connector/FH34SRJ-6S-0.5SH50?qs=vnk2wBG9e15jF3vv7p0sbw%3D%3D)

## Pinout (34-pin)


| Pin (CB) |  nRF  | Control Board |                   Type                    | Adapter Board | Pin (AB) |
| :------: | :---: | :-----------: | :---------------------------------------: | :-----------: | :------: |
|    1     | P0.00 |   KSI_00_IN   |                                           |      IO0      |    34    |
|    2     | P0.01 |     KSI1      |                                           |      IO1      |    33    |
|    3     | P0.02 |     KSI2      |                                           |      IO2      |    32    |
|    4     | P0.03 |   KSI_03_IN   |                                           |      IO3      |    31    |
|    5     | P0.04 |     KSI4      |                                           |      IO4      |    30    |
|    6     | P0.05 |     KSI5      |                                           |      IO5      |    29    |
|    7     | P0.06 |     KSI6      |                                           |      IO6      |    28    |
|    8     | P0.07 |     KSI7      |                                           |      IO7      |    27    |
|    9     | P1.00 |     KSO0      |                                           |      IO8      |    26    |
|    10    | P1.01 |     KSO1      |                                           |      IO9      |    25    |
|    11    | P1.18 |   KSO_02_IN   |                                           |     IO10      |    24    |
|    12    | P1.19 |     KSO3      |                                           |     IO11      |    23    |
|    13    | P1.04 |     KSO4      |                                           |     IO12      |    22    |
|    14    | P1.05 |     KSO5      |                                           |     IO13      |    21    |
|    15    | P1.06 |     KSO6      |                                           |     IO14      |    20    |
|    16    | P1.07 |     KSO7      |                                           |     IO15      |    19    |
|    17    | P1.08 |     KSO8      |                                           |     IO16      |    18    |
|    18    | P1.09 |     KSO9      |                                           |     IO17      |    17    |
|    19    | P1.10 |     KSO10     |                                           |     IO18      |    16    |
|    20    | P1.11 |     KSO11     |                                           |     IO19      |    15    |
|    21    | P1.12 |     KSO12     |                                           |     IO20      |    14    |
|    22    | P1.13 |     KSO13     |                                           |     IO21      |    13    |
|    23    | P1.14 |     KSO14     |                                           |     IO22      |    12    |
|    24    | P1.15 |     KSO15     |                                           |     IO23      |    11    |
|    25    | P1.16 |     KSO16     |                                           |     IO24      |    10    |
|    26    | P1.17 |     KSO17     |                                           |     IO25      |    9     |
|    27    |   -   |    CAPS_P     |           VLED_3.3V (always on)           |    LED_3V3    |    8     |
|    28    | P3.07 |    CAPS_N     | to ground through 330R and CAP_LED MOSFET |    CAPS_N     |    7     |
|    29    |   -   |      NC       |               Not Connected               |      NC       |    6     |
|    30    | P3.08 |  TP_I2C_SDA   |                                           |    I2C_SDA    |    5     |
|    31    | P3.04 |  TP_I2C_CLK   |                                           |    I2C_CLK    |    4     |
|    32    |   -   |  TP_VDD_3.3V  |      switchable by TP_Power_Control       |    TP_3V3     |    3     |
|    33    | P3.06 |    TP_INT     |                                           |     IO26      |    2     |
|    34    |   -   |    TP_GND     |           To GND through R8 0R            |      GND      |    1     |

## Pinout (6-pin)


| Pin (CB) | Control Board |     Type      | Adapter Board | Pin (AB) |
| :------: | :-----------: | :-----------: | :-----------: | :------: |
|    1     |    VLED_BL    |               |      VIN      |    6     |
|    2     |    VLED_BL    |               |      VIN      |    5     |
|    3     |      NC       | Not Connected |               |    4     |
|    4     |      NC       | Not Connected |               |    3     |
|    5     |      GND      |               |      GND      |    2     |
|    6     |      GND      |               |      GND      |    1     |