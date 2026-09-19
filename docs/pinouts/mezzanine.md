# Mezzanine connector

Classic 7-row keyboard (2 types) and old chiclet

## Compatible connectors
- JAE AA01B-S040VA1 (original, hard to find)
- WM6787CT-ND (alternative, no locating feature, easy to break and posibility of misaligment)

## Compatible models (TBD)
- T60, T61, T400, R60, R61, R400, R500, W500, W700 (w/o numpad)  (classic type 1, narrow navigation keys, gap between kb and navigation keys)
- X60?, X60S?, X61?, X61S? (gap filled between kb and navigation keys)
- X200?, X210?, X300? (colorful narrow navigation keys, gap filled between kb and navigation keys)
- T410, T420, T510, T520, W510, W520, X220 (classic type 2, wide navigation keys)
- T430, T530, W530, X230 (chiclet with top bezel, optional backlight)
## Pinout

Slight differences between generations

|  Pin   |    T60     |      T420      |      T430       |                 Type                  |  AdapterBoard   |
| :----: | :--------: | :------------: | :-------------: | :-----------------------------------: | :-------------: |
|   1    |   HOTKEY   |     HOTKEY     |     HOTKEY      |                   ?                   |        ?        |
|   2    |    DRV4    |      DRV4      |      DRV4       |                                       |                 |
|   3    |   SENSE5   |     SENSE5     |     SENSE5      |                                       |                 |
|   4    |    DRV5    |      DRV5      |      DRV5       |                                       |                 |
|   5    |   SENSE0   |     SENSE0     |     SENSE0      |                                       |                 |
|   6    |    DRV8    |      DRV8      |      DRV8       |                                       |                 |
|   7    |   SENSE3   |     SENSE3     |     SENSE3      |                                       |                 |
|   8    |    DRV6    |      DRV6      |      DRV6       |                                       |                 |
|   9    |   SENSE2   |     SENSE2     |     SENSE2      |                                       |                 |
|   10   |    DRV3    |      DRV3      |      DRV3       |                                       |                 |
|   11   |   SENSE4   |     SENSE4     |     SENSE4      |                                       |                 |
|   12   |    DRV7    |      DRV7      |      DRV7       |                                       |                 |
|   13   |   SENSE1   |     SENSE1     |     SENSE1      |                                       |                 |
|   14   |    DRV2    |      DRV2      |      DRV2       |                                       |                 |
|   15   |   SENSE6   |     SENSE6     |     SENSE6      |                                       |                 |
|   16   |   DRV10    |     DRV10      |      DRV10      |                                       |                 |
|   17   |   SENSE7   |     SENSE7     |     SENSE7      |                                       |                 |
|   18   |    DRV1    |      DRV1      |      DRV1       |                                       |                 |
|   19   | PWRSWITCH  |   PWRSWITCH    |    PWRSWITCH    |                                       |                 |
|   20   |    DRV9    |      DRV9      |      DRV9       |                                       |                 |
| **21** |   **NC**   | **LEDCPSLOCK** | **KBD_BL_DTCT** |                                       |                 |
|   22   |    DRV0    |      DRV0      |      DRV0       |                                       |                 |
| **23** |   **NC**   |   **LEDPWR**   |   **LEDPWR**    |                                       |                 |
|   24   |   DRV11    |     DRV11      |      DRV11      |                                       |                 |
| **25** | **KBDID0** |   **KBDID0**   | **KBD_BL_PWM**  |                                       |                 |
|   26   |   DRV14    |     DRV14      |      DRV14      |                                       |                 |
| **27** | **KBDID1** |   **KBDID1**   |     **GND**     |                                       |                 |
|   28   |   DRV12    |     DRV12      |      DRV12      |                                       |                 |
| **29** | **KBDID2** |   **KBDID2**   |    **VCC5B**    |                                       |                 |
|   30   |   DRV15    |     DRV15      |      DRV15      |                                       |                 |
|   31   |    GND     |      GND       |       GND       |                                       |                 |
|   32   |   DRV13    |     DRV13      |      DRV13      |                                       |                 |
| **33** |   **NC**   |  **LED_MUTE**  |  **LED_MUTE**   |                                       |                 |
|   34   |    GND     |      GND       |       GND       |                                       |                 |
| **35** |   **NC**   |   **VCC3M**    |    **VCC3M**    |                                       |                 |
| **36** |  **GND**   | **LEDMICMUTE** | **LEDMICMUTE**  |                                       |                 |
|   37   |  TP4DATA   |    TP4DATA     |     TP4DATA     | TrackPoint Data line, pullup 4.7k@5V  | ?, pullup @3V3  |
|   38   |   VCC5B    |     VCC5B      |      VCC5B      |                                       |                 |
|   39   |   TP4CLK   |     TP4CLK     |     TP4CLK      | TrackPoint Clock line, pullup 4.7k@5V | ?, pullup @3V3  |
|   40   | TP4_RESET  |   TP4_RESET    |    TP4_RESET    | TrackPoint Reset line, pullup 10k@5V  | ?, pullup @3V3? |
|   41   |    GND     |      GND       |       GND       |            Mounting point             |       GND       |
|   42   |    GND     |      GND       |       GND       |            Mounting point             |       GND       |
|   43   |    GND     |      GND       |       GND       |            Mounting point             |       GND       |
|   44   |    GND     |      GND       |       GND       |            Mounting point             |       GND       |