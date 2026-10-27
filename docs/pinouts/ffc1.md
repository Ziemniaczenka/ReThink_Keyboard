# FFC 1 connector

Classic 6-row keyboard
Dual FFC connectors (30-pin P1.0mm for matrix, 8-pin P1.0mm for Pointing Stick)

## Compatible connectors

1. 30-pin
   - pitch: 1.0mm
   - key: straight
   - side: **top** (based on planed bends for adapter placement, not on laptop placement)
   - lock: yes?
   - Compatible MPN:
     - 85208-3007N-01???
     - Omron XF3M(1)-3015-1B
       - [Mouser](https://www.mouser.pl/en/ProductDetail/Omron-Electronics/XF3M1-3015-1B?qs=1He0yLMpldDsC1Cgk53qLQ%3D%3D)
2. 8-pin
   - pitch: 1.0mm
   - key: straight
   - side: **bottom**
   - lock: yes?
   - Compatible MPN:
     - Omron XF3M(1)-0815-1B
       - [Mouser](https://www.mouser.pl/en/ProductDetail/Omron-Electronics/XF3M1-0815-1B?qs=q%2FTJjBi8OU92LX9jQs7B8Q%3D%3D)


## Compatible models (TBD)

- L410, L412, L420, L421, L510, L512, L520, SL300, SL410, SL510
- X120???

## Pinout (30-pin)

|  Pin  |  L420  |       Type        | Adapter Board |
| :---: | :----: | :---------------: | :-----------: |
|   1   |   NC   |   Not Connected   |      NC       |
|   2   |   NC   |   Not Connected   |      NC       |
|   3   | RIGHT  | Navigation Button |   TP1_RIGHT   |
|   4   | MIDDLE | Navigation Button |  TP1_MIDDLE   |
|   5   |  LEFT  | Navigation Button |   TP1_LEFT    |
|   6   |  GND   |                   |      GND      |
|   7   |  MY15  |                   |     DRV15     |
|   8   |  MY10  |                   |     DRV10     |
|   9   |  MY11  |                   |     DRV11     |
|  10   |  MY14  |                   |     DRV14     |
|  11   |  MY13  |                   |     DRV13     |
|  12   |  MY12  |                   |     DRV12     |
|  13   |  MY3   |                   |     DRV3      |
|  14   |  MY6   |                   |     DRV6      |
|  15   |  MY8   |                   |     DRV8      |
|  16   |  MY7   |                   |     DRV7      |
|  17   |  MY4   |                   |     DRV4      |
|  18   |  MY2   |                   |     DRV2      |
|  19   |  MX0   |                   |    SENSE0     |
|  20   |  MY1   |                   |     DRV1      |
|  21   |  MY5   |                   |     DRV5      |
|  22   |  MX3   |                   |    SENSE3     |
|  23   |  MX2   |                   |    SENSE2     |
|  24   |  MY0   |                   |     DRV0      |
|  25   |  MX5   |                   |    SENSE5     |
|  26   |  MX4   |                   |    SENSE4     |
|  27   |  MY9   |                   |     DRV9      |
|  28   |  MX6   |                   |    SENSE6     |
|  29   |  MX7   |                   |    SENSE7     |
|  30   |  MX1   |                   |    SENSE1     |


## Pinout (8-pin)
|  Pin  |       L420        | Type  | Adapter Board |
| :---: | :---------------: | :---: | :-----------: |
|   1   |  TRACK_POINT_DAT  |       |    TP1_DAT    |
|   2   | TRACK_POINT_RESET |       |    TP1_RST    |
|   3   |      MIDDLE       |       |  TP1_MIDDLE   |
|   4   |       RIGHT       |       |   TP1_RIGHT   |
|   5   |       LEFT        |       |   TP1_LEFT    |
|   6   |  TRACK_POINT_CLK  |       |    TP1_CLK    |
|   7   |        GND        |       |      GND      |
|   8   |        5V         |       |    TP1_PWR    |