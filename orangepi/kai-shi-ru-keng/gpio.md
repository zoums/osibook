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



