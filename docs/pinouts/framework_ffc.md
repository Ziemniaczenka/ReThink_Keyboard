# Framework Control Board FFC connectors

34-pin FFC connector for data as well as 6-pin for Backlight power  

## Compatible connectors
???

## Pinout (34-pin)


| Pin (CB) |  nRF  | Control Board |                   Type                    | Adapter Board | Pin (AB) |
| :------: | :---: | :-----------: | :---------------------------------------: | :-----------: | :------: |
|    1     | P0.00 |   KSI_00_IN   |                                           |               |    34    |
|    2     | P0.01 |     KSI1      |                                           |               |    33    |
|    3     | P0.02 |     KSI2      |                                           |               |    32    |
|    4     | P0.03 |   KSI_03_IN   |                                           |               |    31    |
|    5     | P0.04 |     KSI4      |                                           |               |    30    |
|    6     | P0.05 |     KSI5      |                                           |               |    29    |
|    7     | P0.06 |     KSI6      |                                           |               |    28    |
|    8     | P0.07 |     KSI7      |                                           |               |    27    |
|    9     | P1.00 |     KSO0      |                                           |               |    26    |
|    10    | P1.01 |     KSO1      |                                           |               |    25    |
|    11    | P1.18 |   KSO_02_IN   |                                           |               |    24    |
|    12    | P1.19 |     KSO3      |                                           |               |    23    |
|    13    | P1.04 |     KSO4      |                                           |               |    22    |
|    14    | P1.05 |     KSO5      |                                           |               |    21    |
|    15    | P1.06 |     KSO6      |                                           |               |    20    |
|    16    | P1.07 |     KSO7      |                                           |               |    19    |
|    17    | P1.08 |     KSO8      |                                           |               |    18    |
|    18    | P1.09 |     KSO9      |                                           |               |    17    |
|    19    | P1.10 |     KSO10     |                                           |               |    16    |
|    20    | P1.11 |     KSO11     |                                           |               |    15    |
|    21    | P1.12 |     KSO12     |                                           |               |    14    |
|    22    | P1.13 |     KSO13     |                                           |               |    13    |
|    23    | P1.14 |     KSO14     |                                           |               |    12    |
|    24    | P1.15 |     KSO15     |                                           |               |    11    |
|    25    | P1.16 |     KSO16     |                                           |               |    10    |
|    26    | P1.17 |     KSO17     |                                           |               |    9     |
|    27    |   -   |    CAPS_P     |                 VLED_3.3V                 |               |    8     |
|    28    |   -   |    CAPS_N     | to ground through 330R and CAP_LED MOSFET |               |    7     |
|    29    |   -   |      NC       |               Not Connected               |               |    6     |
|    30    | P3.08 |  TP_I2C_SDA   |                                           |               |    5     |
|    31    | P3.04 |  TP_I2C_CLK   |                                           |               |    4     |
|    32    |   -   |  TP_VDD_3.3V  |                                           |               |    3     |
|    33    | P3.06 |    TP_INT     |                                           |               |    2     |
|    34    |   -   |    TP_GND     |           To GND through R8 0R            |               |    1     |

## Pinout (6-pin)


| Pin (CB) | Control Board |     Type      | Adapter Board | Pin (AB) |
| :------: | :-----------: | :-----------: | :-----------: | :------: |
|    1     |    VLED_BL    |               |               |    6     |
|    2     |    VLED_BL    |               |               |    5     |
|    3     |      NC       | Not Connected |               |    4     |
|    4     |      NC       | Not Connected |               |    3     |
|    5     |      GND      |               |               |    2     |
|    6     |      GND      |               |               |    1     |