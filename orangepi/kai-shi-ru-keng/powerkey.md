# 香橙派关机键设置

#### 大家买香橙派的时候应该发现香橙派有开机键吧，由于香橙派没有电源管理IC，想用它来开机是不可能的，但是拿来关机还是可以的，香橙派安卓系统关机键可以直接用，不用设置，本次教程是针对Linux系统，下面我们开始教程。

首先我们输入

```
sudo apt-get update
```

更新一下源，然后输入安装acpid

```
sudo apt install acpid
```

这个是Linux的ACPI高级电源管理

安装完毕输入

```
sudo nano /etc/acpi/events/ button_power
```

随便用个文本编辑器吧，我用的是nano

输入以下内容

```
event=button/power
action=/sbin/shutdown -h now
```

这个代码是设置电源键为关机键

这个是重启代码

```
event=button/power
action=/sbin/reboot
```

然后按Ctrl键加O键回车确认文件名保存，按Ctrl键加X键退出（其他的文本编辑器随你）

然后执行

```
service acpid restart
```

生效



