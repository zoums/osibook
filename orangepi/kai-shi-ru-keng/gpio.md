# GPIO

**General Purpose Input/Output**\(**GPIO**\)是集成电路上的通用IO口，通过运行时由用户控制或者编程控制（包括它是否输入输出）。作为开发板外接的接口，很适合被用户用来做各种各样奇怪的事情，但是，连接各种奇怪的东西前，请注意看接口定义和内外电路！损坏了的别怪我不提醒。。。顺便说句。。低价收坏PI了喂\(/滑稽\)。

## 概述

GPIO引脚没有特殊的定义，通常在默认情况下不使用。这样的做法是是，有时系统开发商想建立一个完整的系统，使用芯片可能会发现有一些额外的数字控制线路是有用的，有些是没用的，而且从芯片中可以直接获得这些接口可以省去额外的电路来提供它们。

GPIO端口是由一组GPIO引脚（通常有8个PA、PC、PE等）组成，并且作为单个端口进行处理。

# 在主线内核访问GPIO引脚通过sysfs用户空间

GPIO能被来自用户空间的sysfs访问。要打开它你需要打开这个内核选项：CONFIG\_GPIO\_SYSFS

建议在此之前检查/sys/class/gpio下是否有export和unexport，如果有，你不用重新编译内核而去使用sysfs。

```
Device Drivers  --->GPIO Support  --->/sys/class/gpio/... (sysfs interface)
```

要访问一个GPIO管脚你，你首先得导出它用如下命令：

```
echo XX > /sys/class/gpio/export
```

你需要通过计算获得所需要的针脚的数值XX，下面以PH18为实例：

```
(第二位字母按A-Z的排序值 - 1) * 32 + 针脚数值
```

例如 PH18 是 \( 8 - 1\) \* 32 + 18 = 224 + 18 = 242 \(H是第八个字母\)。

简而言之，是PH18第二位字母H的排序8减去1乘以32再加引脚号。

在此之后你就能成功访问PH18通过**/sys/class/gpio/gpio\*NUMBER\***\(在这里PH18是/sys/class/gpio/gpio242\).

通过 /sys/class/gpio/gpio\*NUMBER\*/direction 你能设置管脚的输入输出（in/out）。

```
echo "out" > /sys/class/gpio/gpio*NUMBER*/direction
```

然后你能通过 **/sys/class/gpio/gpio\*NUMBER\*/value 读写管脚。**

当你要取消访问管脚时，可以：

```
echo XX > /sys/class/gpio/unexport
```

注：XX是管脚计算出来的编号，具体看上面访问管脚部分。

# 访问GPIO通过sysfs在sunxi-3.4/3.10（全志的bsp内核）

这个方法可能随时失效，不过我在3.4.103上依旧能用，恕不另行通知。并且如果你想用mainline的方法，可以把模块去掉（可能还需要去/etc/modules里面去掉），如果没有/sys/class/gpio，你还需要按mainline的方法去配置内核。

首先你得确保script.bin有定义一些引脚，否则当你加载这个模块时会报错提示没有引脚定义在script.bin。一些系统的script.bin原本已经定义了不少GPIO管脚，3.10一般是全志H5或者A64，他们一般在Linux下使用**DTB**而不是script.bin。dtb和script.bin修改方法在进阶那章。

如下给出script.bin的相关定义，dtb日后再给。

```
 [gpio_para]
 gpio_used= 1
 gpio_num=12
 gpio_pin_1= port:PE00
 gpio_pin_2= port:PE01
 gpio_pin_3= port:PE02
 gpio_pin_4= port:PE03
 gpio_pin_5= port:PE04
 gpio_pin_6= port:PE05
 gpio_pin_7= port:PE06
 gpio_pin_8= port:PE07
 gpio_pin_9= port:PE08
 gpio_pin_10= port:PE09
 gpio_pin_11= port:PE10
 gpio_pin_12= port:PE11
```

如果你想在端口输入时设置上拉或者下拉，你可以去阅读FEX教程这一部分[Port Definitions](http://linux-sunxi.org/Fex_Guide#Port_Definitions)。中文的在此链接: [http://pan.baidu.com/s/1nvObrvz](http://pan.baidu.com/s/1nvObrvz) 密码: vp32

然后你需要去加载这个内核模块：

```
  modprobe gpio-sunxi
```

然后导入你要的管脚。（然而，有些版本的内核在上一部加载模块后在**/sys/class/gpio\_sw**已有相应管脚访问了，所以不是所有内核版本都适用。）

```
 for A in 1 2 3 4 5 6 7 8 9 10 11 12; do echo "$A" > /sys/class/gpio/export ; done
```

然后应该会有一些链接在 sys/class/gpio/，或者不行的可以去/sys/class/gpio\_sw：

```
 root@headless2:/sys/class/gpio# ls -l
 total 0
 --w------- 1 root root 4096 Jan 10 00:12 export
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio10_pe9 -> ../../devices/platform/gpio-sunxi/gpio/gpio10_pe9/
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio11_pe10 -> ../../devices/platform/gpio-sunxi/gpio/gpio11_pe10/
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio12_pe11 -> ../../devices/platform/gpio-sunxi/gpio/gpio12_pe11/
 lrwxrwxrwx 1 root root    0 Jan 10 00:11 gpio1_pe0 -> ../../devices/platform/gpio-sunxi/gpio/gpio1_pe0/
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio2_pe1 -> ../../devices/platform/gpio-sunxi/gpio/gpio2_pe1/
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio3_pe2 -> ../../devices/platform/gpio-sunxi/gpio/gpio3_pe2/
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio4_pe3 -> ../../devices/platform/gpio-sunxi/gpio/gpio4_pe3/
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio5_pe4 -> ../../devices/platform/gpio-sunxi/gpio/gpio5_pe4/
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio6_pe5 -> ../../devices/platform/gpio-sunxi/gpio/gpio6_pe5/
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio7_pe6 -> ../../devices/platform/gpio-sunxi/gpio/gpio7_pe6/
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio8_pe7 -> ../../devices/platform/gpio-sunxi/gpio/gpio8_pe7/
 lrwxrwxrwx 1 root root    0 Jan 10 00:12 gpio9_pe8 -> ../../devices/platform/gpio-sunxi/gpio/gpio9_pe8/
 lrwxrwxrwx 1 root root    0 Jan 10 00:10 gpiochip1 -> ../../devices/platform/gpio-sunxi/gpio/gpiochip1/
 --w------- 1 root root 4096 Jan 10 00:09 unexport
 root@headless2:/sys/class/gpio#
```

设置需要的方向direction（比如这里是out输出）：

```
 echo out > /sys/class/gpio/gpio12_pe11/direction
```

然后你能输出一些东西（管脚高电平，3.3v）：

```
 echo 1 > /sys/class/gpio/gpio12_pe11/value
```

仔细阅读内核文档sysfs gpio可以获得更多可用的特征及方法。[Documentation/gpio/sysfs.txt](https://www.kernel.org/doc/Documentation/gpio/sysfs.txt)

# 另请参阅

* [JTAG](http://linux-sunxi.org/JTAG)
* [MicroSD Breakout](http://linux-sunxi.org/MicroSD_Breakout)
* [A10/PIO](http://linux-sunxi.org/A10/PIO)
* [A13/PIO](http://linux-sunxi.org/A13/PIO)
* [A20/PIO](http://linux-sunxi.org/A20/PIO)
* [H3/PIO](http://linux-sunxi.org/H3/PIO)

# 参考文献

1. [https://github.com/torvalds/linux/blob/master/drivers/pinctrl/sunxi/pinctrl-sunxi.h\#L19](https://github.com/torvalds/linux/blob/master/drivers/pinctrl/sunxi/pinctrl-sunxi.h#L19)

# 外部链接

* [ALSA Development List](http://www.spinics.net/lists/alsa-devel/msg03646.html)
* [Linux Kernel Doc on GPIO](https://git.kernel.org/cgit/linux/kernel/git/linusw/linux-gpio.git/tree/Documentation/gpio/gpio.txt)
* [LinuxTV GPIO Pins Info](http://linuxtv.org/wiki/index.php/GPIO_pins)
* [GPIO Tutorial - بیر رباتیک](http://bir-robotic.ir/blog/2014/04/21/راه-اندازی-gpio-بخش-دوم/)
* [Access GPIO from Linux user space](http://falsinsoft.blogspot.de/2012/11/access-gpio-from-linux-user-space.html)



