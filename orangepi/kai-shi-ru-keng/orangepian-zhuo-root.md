# OrangePi安卓root

H3

> 需要的软件 UsbModeSwitch. apk和 UPDATE-SuperSU-v2. 46. zip， 电脑安装 kingroot，

H5 / A64

> 需要 UPDATE-SuperSU-v2. 46. zip

确保开发板的 otg 可以连接到电脑。

1. 打开 adb 调试模式

H3

> 将 UsbModeSwitch. apk 用 U 盘 或 读 卡 器 安 装 进 开 发 板 系 统 中 ， 打 开
>
> UsbModeSwitch. apk 应用， 勾选“enable usb device mode”

H5

> 关于系统里面版本号不停点击，直到显示“开发者选项已打开”然后进去启用调试和USB口

然后用调试线\(要数据线， 有些线不识别\) 将开发板的 otg 接口与计算机相连， 一般计算机将会自 动搜索安装 adb 驱动软件， 若驱动安装失败， 可安装 PC 版豌豆荚， 可成功安装对应的驱动软件\(或者去创客群共享文件里面下载 otg. zip\) 。

1. 成功将开发板与计算机相连后， 打开计算机的命令行模式， 输入 adb 相关命令\(需要安装 adb 调试命令， 豌豆荚里自 带有 adb 命令\) ， 命令如下

```
adb devices
```

会输出所有连接的设备

```
adb shell
```

进入安卓adb的Shell，是root用户下的shell，我们利用这点对安卓进行root。

windows\(win+r\) 命令行进入命令行模式， 进入 kingroot 的目 录. 执行下列步骤

```
adb shell
mount -o remount,rw /
mkdir /tmp
cd /system/bin
mount -o remount, rw /system
ln -s busybox-smp unzip
```

Ctrl + C退出 adb shell 模式或执行:

```
exit
```

解压 UPDATE-SuperSU-v2. 46. zip,将解压之后得到的 META-INF/com/google/android/update-binary 文件放到和该压缩包同一目 录中。

```
adb push /path/UPDATE-SuperSU-v2.46.zip /data/local/tmp
```

注：path 是UPDATE-SuperSU-v2. 46. zip文件在电脑上的文件夹路径

```
adb push /path/update-binary /data/local/tmp
```

注：path 是update-binary文件在电脑上的文件夹路径

```
adb shell
cd /data/local/tmp
sh update-binary 0 1 /data/local/tmp/UPDATE-SuperSU-v2.46.zip
```

> ............................................................................................

等待执行完脚本后， 输入重启命令 reboot 后， 可正常使用设备中的授权软件。

#### 附件

ADB及OTG驱动

链接: [http://pan.baidu.com/s/1miHX72C](http://pan.baidu.com/s/1miHX72C) 密码: gydt

