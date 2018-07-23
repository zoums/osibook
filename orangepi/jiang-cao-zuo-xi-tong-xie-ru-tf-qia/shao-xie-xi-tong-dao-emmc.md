# OrangePi烧写系统到EMMC\(全志\) {#-}

## 安卓

##### 卡刷：

卡量产烧入sdcard启动会有进度条。。等进度条完了拔卡重启就行。

##### 线刷：

1.在WINDOWS上\(其他系统好像有个LiveSuit工具，不知道能不能用）下载phonixsuite工具.

2.按住板子上的升级键。安装驱动，驱动可以去网上找，还有个[Zadig](http://zadig.akeo.ie/)工具，可以安装这个驱动，用法看下面。有些板子没升级键，比如PC PLUS/ZERO PLUS2系列，要么自己找原理图找出UBOOT脚，把它连接到GND让其低电平就能进入刷写模式，还有一个方法是刷特制的sd卡镜像进入刷写模式（[地址](https://raw.githubusercontent.com/zoums/fel-mass-storage/h5-support/fel-sdboot.img)，仅支持H3，H5的有空再制作）。

3.用phonixsuite工具选择镜像，连接电脑上电，烧写。

## linux

linux是烧镜像到sdcard启动，OPI官方系统可以执行

> `（H3）`
>
> `install_to_emmc`
>
> `或者`
>
> `（H5）`
>
> `OrangePi_install2EMMC`

如果没这些命令基本上不能烧进去启动,但是脚本可以手动下。

> `(H3)`
>
> `wget`[`https://raw.githubusercontent.com/zoums/osibook/master/assets/files/install_to_emmc.sh`](https://raw.githubusercontent.com/zoums/osibook/master/assets/files/install_to_emmc.sh)
>
> `chmod +x install__to__emmc.sh && ./install__to__emmc.sh`
>
> `(H5)`
>
> `wget`[`https://raw.githubusercontent.com/zoums/osibook/master/assets/files/OrangePi_install2EMMC.sh`](https://raw.githubusercontent.com/zoums/osibook/master/assets/files/OrangePi_install2EMMC.sh)
>
> `chmod +x OrangePi_install2EMMC.sh && ./OrangePi_install2EMMC.sh`

是armbian之类的可以执行nand-sata-install 实在不行又想尝试一下可以把卡或镜像dd到emmc

emmc可以ls /dev/mmcblk\*来看，看到有boot0和boot1后缀的mmcblk1就是emmc了（有些是mmcblk0，视情况而定）

没图。。。没图。。。没图。。。。等哪天旁边有板子了就上图。。。。。

### 线刷LINUX（仅适用H3/H5部分系统）

按住板子上的升级键。。然后连接电脑，驱动可以去网上找，还有个[Zadig](http://zadig.akeo.ie/)工具，可以安装这个驱动，用法看下面。有些板子没升级键，比如PC PLUS/ZERO PLUS2系列，要么自己找原理图找出UBOOT脚，把它连接到GND让其低电平就能进入刷写模式，还有一个方法是刷特制的sd卡镜像进入刷写模式（[地址](https://raw.githubusercontent.com/zoums/fel-mass-storage/h5-support/fel-sdboot.img)，仅支持H3，H5的有空再制作）。

##### Zadig使用





