# HDMI转dvi支持

\[hdmi\_para\]那项加这两行

```
hdcp_enable = 0
hdmi_cts_compatibility = 1
```

# 微雪HDMI屏显示

最近正好遇到个网友用OPI接微雪屏无法显示白屏的情况，于是答应帮忙解决，现在解决了问题，现把解决方法给出：

![](/assets/orangepi_plus_waveshare.jpg)

1、按照网上修改script.bin的方法将script.bin转换成文本文件

##### 注：本章第二篇

2、用文本编辑器在\[hdmi\_para\]项中加入如下两行定义

```
hdcp_enable = 0
hdmi_cts_compatibility = 1
```

3、修改输出分辨率

800x480（论坛内镜像大多有这分辨率，1024x600是5）

```
screen0_output_mode = 31
```

4、转换回来script.bin并替换

##### 注：该教程理论上可用于微雪所有hdmi接口的屏幕

[![](/assets/5inch-HDMI-LCD-B-1.png)](http://www.waveshare.net/wiki/文件%3A5inch-HDMI-LCD-B-1.png)

* 背光开关：用于控制背光点亮和熄灭，相当于显示器的电源按钮。
* HDMI接口：用于连接主板和LCD显示屏。
* USB触摸接口：USB触摸/电源接口。
* USB电源接口：USB电源接口/仅当LCD供电不足时使用。
* ##### 注：1024x600还需要修改这里
* ![](/assets/232121t9u9hm8m129fzpuk.png)



