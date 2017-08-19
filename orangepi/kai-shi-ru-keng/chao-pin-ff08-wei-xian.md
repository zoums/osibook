# 超频（危险！！！！）

参数解释，具体修改文件参考dtb与script.bin的修改，此教程仅适用Legacy传统的BSP内核。

| dvfs 电压-频率模块配置 |
| :--- |


| 配置 | 参数 |
| :--- | :--- |
| pmuic\_type | 0:none, 1:gpio, 2:i2c |
| pmu\_gpio0 | pmu的GPIO配置 |
| pmu\_levelx | PMU调节的电压等级，0~9999: 电压\(mV\)，10000~90000:gpio0 状态. 电压从高到低 |
| extremity\_freq\(Hz\) | 当benckmark或demo程序时CPU的极致频率（安卓，怎么感觉是为了跑分专用？）推荐1536MHz@1500mV时用散热器, 在1296MHz@1340mV可以不用。 |
| max\_freq | CPU最高频率，单位Hz，不能高于1200MHz |
| min\_freq | CPU最低频率，单位Hz，不能低于60Mhz |
| LV\_count | 频率与电压等级调节计数，必须小于16个 |

注：电压等级，OPIPC/PCPLUS/PC2/PLUS&2/2/PLUS2E用[SY8106A](http://linux-sunxi.org/SY8106A)电压调节器来提供CPU核心电压\(VDD\_CPUX\)，最高电压1.5V，推荐1.4V，能到多少自己测试，不过目前最高普遍能稳定的在1536/1500mv。ONE/Lite/Zero系列是SY8113B \([datasheet](https://www.olimex.com/Products/Breadboarding/BB-PWR-8113/resources/SY8113.pdf)\)，有1.1V和1.3V电压，频率只能到1296Mhz。

频率等级例子（OPIPC）

```
LV1: core vdd is 1.50v if cpu frequency is (1296Mhz,  1536Mhz]
LV2: core vdd is 1.34v if cpu frequency is (1200Mhz,  1296Mhz]
LV3: core vdd is 1.32v if cpu frequency is (1008Mhz,  1200Mhz]
LV4: core vdd is 1.20v if cpu frequency is (816Mhz,   1008Mhz]
LV5: core vdd is 1.10v if cpu frequency is (648Mhz,    816Mhz]
LV6: core vdd is 1.04v if cpu frequency is (0Mhz,      648Mhz]
LV7: core vdd is 1.04v if cpu frequency is (0Mhz,      648Mhz]
LV8: core vdd is 1.04v if cpu frequency is (0Mhz,      648Mhz]
```

配置参数例子（OPIPC）每个LV有两个配置，LV\*volt电压及LV\*freq频率。后面G\_LV的GPU配置等同。

```
[dvfs_table]
pmuic_type = 2
pmu_gpio0         = port:PL06<1><1><2><1>
pmu_level0        = 11300
pmu_level1        = 01100
extremity_freq = 1536000000
#max_freq = 1200000000
max_freq = 900000000
min_freq = 10000000
LV_count = 8
#LV1_freq = 1200000000
LV1_freq = 900000000
LV1_volt = 1200
#LV1_volt = 1500
#LV2_freq = 1008000000
LV2_freq = 800000000
LV2_volt = 1100
#LV2_volt = 1300
#LV3_freq = 0
LV3_freq = 700000000
LV3_volt = 1080
#LV3_volt = 1200
LV4_freq = 500000000
LV4_volt = 1020
LV5_freq = 300000000
LV5_volt = 1010
LV6_freq = 150000000
LV6_volt = 1000
LV7_freq = 100000000
LV7_volt = 990
LV8_freq = 50000000
LV8_volt = 980
[gpu_dvfs_table]
G_LV_count = 3
G_LV0_freq = 212000000
G_LV0_volt = 1200000
G_LV1_freq = 284000000
G_LV1_volt = 1200000
G_LV2_freq = 356000000
G_LV2_volt = 1200000
```

---

年轻人不要老是想着搞事，不过在此，我要大声讲，呀\*啦梁\*\*。。。不对。。。低价收损坏PI了喂。。。

