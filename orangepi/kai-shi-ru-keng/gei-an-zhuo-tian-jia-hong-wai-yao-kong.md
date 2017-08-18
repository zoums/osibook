# 给安卓添加红外遥控

###### 我们都知道OrangePI有红外接收，但是没有一个指导的文档来教我们怎么去使用它，这个帖子将教你怎么去使用它。

首先你需要一个已经root了的安卓系统，我用的是这个：

[http://www.orangepi.cn/orangepibbscn/forum.php?mod=viewthread&tid=57&extra=page%3D1](http://www.orangepi.cn/orangepibbscn/forum.php?mod=viewthread&tid=57&extra=page%3D1)

然后需要一个终端模拟器例如安卓终端、ssh客户端等，以及最好有一个支持挂载系统文件夹为读写的文件管理器例如MT管理器、RE管理器等，或者你使用如下的命令挂载文件系统。

```
mount -o remount,rw /system
```

现在打开终端模拟器并输入以下代码：

```
su
```

这个将使终端模拟器得到root。首先我们来修改遥控器的配置文件。打开你的文件管理器并进入/system/usr/keylayout挂载成读写，更改此目录下的sunxi-ir.kl成sunxi-ir.kl.bak以做备用及参照。你也可以在终端里执行如下命令实现上面的步骤：

```
mount -o remount,rw /system
mv /system/usr/keylayout/sunxi-ir.kl /system/usr/keylayout/sunxi-ir.kl.bak
```

然后在文件管理器里创建一个新的配置文件并命名为sunxi-ir.kl或执行如下命令：

```
mount -o remount,rw /system
echo new > /system/usr/keylayout/sunxi-ir.kl
```

接下来要重新加载红外驱动以便更改配置。终端下执行如下命令：

```
rmmod sunxi_ir_rx
insmod /vendor/modules/sunxi-ir-rx.ko
```

##### 注： 建议重启，似乎这样能正常点，重启记得做前两步。

然后需要为遥控器添加配置文件，现在配置文件是空的。先执行如下命令获取键代码：

```
getevent
```

出现如下信息：

```
root@dolphin-fvd-p1:/ # getevent
add device 1: /dev/input/event6
  name:     "sunxi-ir"
add device 2: /dev/input/event7
  name:     "Virtual.Acc"
could not get driver version for /dev/input/js0, Invalid argument
add device 3: /dev/input/event5
  name:     "Logitech USB Optical Mouse"
could not get driver version for /dev/input/mouse1, Not a typewriter
add device 4: /dev/input/event4
  name:     "USB USB Keykoard"
add device 5: /dev/input/event3
  name:     "USB USB Keykoard"
add device 6: /dev/input/event2
  name:     "sunxi-ths"
add device 7: /dev/input/event1
  name:     "sunxi-gpiokey"
could not get driver version for /dev/input/mouse0, Not a typewriter
add device 8: /dev/input/event0
  name:     "vmouse"
could not get driver version for /dev/input/mice, Not a typewriter
/dev/input/event3: 0004 0004 00070028
/dev/input/event3: 0001 001c 00000000
/dev/input/event3: 0000 0000 00000000
/dev/input/event6: 0001 0012 00000001
/dev/input/event6: 0000 0000 00000000
^@/dev/input/event6: 0001 0012 00000000
/dev/input/event6: 0000 0000 00000000
/dev/input/event6: 0001 000b 00000001
```

可以看到开始两行有“add device 1: /dev/input/event6”和名字“sunxi-ir”，这告诉我们红外接收是event6，接下来不要对鼠标键盘进行操作，否则会数次调试信息干扰获取红外的键代码。如果按下遥控器上某个按键就会有调试输出像如下代码那样：

```
/dev/input/event6: 0001 0012 00000001
/dev/input/event6: 0000 0000 00000000
```

需要的键代码是第一行的第二组数字

```
0012
```

但是这组数字是十六进制的，要把它需要转换成十进制，我使用的是这个

[在线转换16进制到10进制的工具](http://www.binaryhexconverter.com/hex-to-decimal-converter)

0012转换成十进制就是18，然后你要把他们记下来继续调试，调试结束按Ctrl-C来停止getevent。调试完毕后在文件管理器里打开之前创建的/system/usr/keylayout/sunxi-ir.kl

（记得先确认是否挂载成读写再去编辑它）以及添加遥控器配置进去。配置文件格式是：

```
key "键代码" “安卓命令”
```

##### \(可参照之前备份的sunxi-ir.kl.bak\)。

下面列出的是我用的键代码。然后保存这个配置文件并重新加载驱动来应用新的配置文件即可。

```
key    18  POWER WAKE
key    19  MUTE
key    14  MEDIA_STOP
key    31  MEDIA_PLAY
key    30  MEDIA_PAUSE
key    15  MEDIA_PREVIOUS
key    26  MEDIA_NEXT
key    11  DPAD_UP
key    21  DPAD_DOWN
key    24  DPAD_LEFT
key    12  DPAD_RIGHT
key    22  ENTER
key    13  BACK
key    25  VOLUME_UP
key    29  VOLUME_DOWN
```

重新加载驱动，不过建议重启。

```
rmmod sunxi_ir_rx
insmod /vendor/modules/sunxi-ir-rx.ko
```

如果没什么错误你的遥控器已经开始工作了。

##### 下面说说我遇到的一个小问题：

##### 我在添加配置文件并修改好重新配置加载驱动后发现遥控器并未工作，研究一番后发现键代码格式不对，对比/system/usr/keylayout下其他配置文件发现key与键代码与安卓命令之间的空格数目不一样，结果把几个空格对应加上并重新加载驱动遥控器才正常工作。



