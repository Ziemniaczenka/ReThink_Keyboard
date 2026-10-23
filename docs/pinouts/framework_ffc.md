# Framework Control Board FFC connectors

34-pin FFC connector for data as well as 6-pin for Backlight power  

## Compatible connectors

1. 34-pin
   - pitch: 0.5mm
   - key: straight
   - side: dual?
   - lock: back
   - Compatible MPN:
     - Hirose FH34SRJ-34S-0.5SH(50)
       - [Mouser](https://www.mouser.pl/en/ProductDetail/Hirose-Connector/FH34SRJ-34S-0.5SH50?qs=iyLo5FA4poAumYnqXazWvw%3D%3D)
2. 6-pin
   - pitch: 0.5mm
   - key: straight
   - side: dual?
   - lock: back
   - Compatible MPN:
     - Hirose FH34SRJ-6S-0.5SH(50)
       - [Mouser](https://www.mouser.pl/en/ProductDetail/Hirose-Connector/FH34SRJ-6S-0.5SH50?qs=vnk2wBG9e15jF3vv7p0sbw%3D%3D)

## Pinout (34-pin) (TODO: VERIFY ORIENTATION!!!)


| Pin (CB) |  nRF  | Control Board |                   Type                    | Adapter Board | Pin (AB) |
| :------: | :---: | :-----------: | :---------------------------------------: | :-----------: | :------: |
|    1     | P0.00 |   KSI_00_IN   |                                           |    SENSE0     |    34    |
|    2     | P0.01 |     KSI1      |                                           |    SENSE1     |    33    |
|    3     | P0.02 |     KSI2      |                                           |    SENSE2     |    32    |
|    4     | P0.03 |   KSI_03_IN   |                                           |    SENSE3     |    31    |
|    5     | P0.04 |     KSI4      |                                           |    SENSE4     |    30    |
|    6     | P0.05 |     KSI5      |                                           |    SENSE5     |    29    |
|    7     | P0.06 |     KSI6      |                                           |    SENSE6     |    28    |
|    8     | P0.07 |     KSI7      |                                           |    SENSE7     |    27    |
|    9     | P1.00 |     KSO0      |                                           |     DRV0      |    26    |
|    10    | P1.01 |     KSO1      |                                           |     DRV1      |    25    |
|    11    | P1.18 |   KSO_02_IN   |                                           |     DRV2      |    24    |
|    12    | P1.19 |     KSO3      |                                           |     DRV3      |    23    |
|    13    | P1.04 |     KSO4      |                                           |     DRV4      |    22    |
|    14    | P1.05 |     KSO5      |                                           |     DRV5      |    21    |
|    15    | P1.06 |     KSO6      |                                           |     DRV6      |    20    |
|    16    | P1.07 |     KSO7      |                                           |     DRV7      |    19    |
|    17    | P1.08 |     KSO8      |                                           |     DRV8      |    18    |
|    18    | P1.09 |     KSO9      |                                           |     DRV9      |    17    |
|    19    | P1.10 |     KSO10     |                                           |     DRV10     |    16    |
|    20    | P1.11 |     KSO11     |                                           |     DRV11     |    15    |
|    21    | P1.12 |     KSO12     |                                           |     DRV12     |    14    |
|    22    | P1.13 |     KSO13     |                                           |     DRV13     |    13    |
|    23    | P1.14 |     KSO14     |                                           |     DRV14     |    12    |
|    24    | P1.15 |     KSO15     |      Pointing Stick data line (3V3)       |    FW_DAT     |    11    |
|    25    | P1.16 |     KSO16     |       Pointing Stick clk line (3V3)       |    FW_CLK     |    10    |
|    26    | P1.17 |     KSO17     |           PWM backlight control           |      PWM      |    9     |
|    27    |   -   |    CAPS_P     |           VLED_3.3V (always on)           |    LED_3V3    |    8     |
|    28    | P3.07 |    CAPS_N     | to ground through 330R and CAP_LED MOSFET |    CAPS_N     |    7     |
|    29    |   -   |      NC       |               Not Connected               |      NC       |    6     |
|    30    | P3.08 |  TP_I2C_SDA   |                                           |    I2C_SDA    |    5     |
|    31    | P3.04 |  TP_I2C_CLK   |                                           |    I2C_CLK    |    4     |
|    32    |   -   |  TP_VDD_3.3V  |      switchable by TP_Power_Control       |    TP_3V3     |    3     |
|    33    | P3.06 |    TP_INT     |                                           |     IO26      |    2     |
|    34    |   -   |    TP_GND     |           To GND through R8 0R            |      GND      |    1     |

## Pinout (6-pin)  (TODO: VERIFY ORIENTATION!!!)

| Pin (CB) | Control Board |     Type      | Adapter Board | Pin (AB) |
| :------: | :-----------: | :-----------: | :-----------: | :------: |
|    1     |    VLED_BL    |               |      VIN      |    1     |
|    2     |    VLED_BL    |               |      VIN      |    2     |
|    3     |      NC       | Not Connected |               |    3     |
|    4     |      NC       | Not Connected |               |    4     |
|    5     |      GND      |               |      GND      |    5     |
|    6     |      GND      |               |      GND      |    6     |