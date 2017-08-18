# 超频（危险！！！！）


| dvfs 电压-频率模块配置 |
| :--- | :--- |
|  |  |
| :--- | :--- |
|  |  |



;

; pmuic\_type:0:none, 1:gpio, 2:i2c

; pmu\_gpio0: gpio config.

; pmu\_levelx: 0~9999: voltage\(mV\), 10000~90000:gpio0 state. voltage form high to low.

;

; extremity\_freq\(Hz\): cpu extremity frequency when run benckmark or demo apk

;                     1536MHz@1500mV with radiator, 1296MHz@1340mV without radiator

; max\_freq: cpu maximum frequency, based on Hz, can not be more than 1200MHz

; min\_freq: cpu minimum frequency, based on Hz, can not be less than 60MHz

;

; LV\_count: count of LV\_freq/LV\_volt, must be &lt; 16

;

; LV1: core vdd is 1.50v if cpu frequency is \(1296Mhz,  1536Mhz\]

; LV2: core vdd is 1.34v if cpu frequency is \(1200Mhz,  1296Mhz\]

; LV3: core vdd is 1.32v if cpu frequency is \(1008Mhz,  1200Mhz\]

; LV4: core vdd is 1.20v if cpu frequency is \(816Mhz,   1008Mhz\]

; LV5: core vdd is 1.10v if cpu frequency is \(648Mhz,    816Mhz\]

; LV6: core vdd is 1.04v if cpu frequency is \(0Mhz,      648Mhz\]

; LV7: core vdd is 1.04v if cpu frequency is \(0Mhz,      648Mhz\]

; LV8: core vdd is 1.04v if cpu frequency is \(0Mhz,      648Mhz\]

;

;----------------------------------------------------------------------------------

\[dvfs\_table\]

pmuic\_type = 2

pmu\_gpio0         = port:PL06&lt;1&gt;&lt;1&gt;&lt;2&gt;&lt;1&gt;

pmu\_level0        = 11300

pmu\_level1        = 01100

extremity\_freq = 1536000000

\#max\_freq = 1200000000

max\_freq = 900000000

min\_freq = 10000000



LV\_count = 8



\#LV1\_freq = 1200000000

LV1\_freq = 900000000

LV1\_volt = 1200

\#LV1\_volt = 1500



\#LV2\_freq = 1008000000

LV2\_freq = 800000000

LV2\_volt = 1100

\#LV2\_volt = 1300



\#LV3\_freq = 0

LV3\_freq = 700000000

LV3\_volt = 1080

\#LV3\_volt = 1200



LV4\_freq = 500000000

LV4\_volt = 1020



LV5\_freq = 300000000

LV5\_volt = 1010



LV6\_freq = 150000000

LV6\_volt = 1000



LV7\_freq = 100000000

LV7\_volt = 990



LV8\_freq = 50000000

LV8\_volt = 980



\[gpu\_dvfs\_table\]



G\_LV\_count = 3



G\_LV0\_freq = 212000000

G\_LV0\_volt = 1200000

G\_LV1\_freq = 284000000

G\_LV1\_volt = 1200000

G\_LV2\_freq = 356000000

G\_LV2\_volt = 1200000

