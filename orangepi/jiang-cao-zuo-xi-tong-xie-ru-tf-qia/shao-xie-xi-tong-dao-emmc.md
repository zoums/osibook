# OrangePi烧写系统到EMMC\(全志\) {#-}

# 安卓 {#-}

卡量产烧入sdcard启动会有进度条。。等进度条完了拔卡重启就行或者phonixsuite按住板子上的升级键。。然后连接电脑用phonixsuite工具烧写，有些板子没升级键，比如PC PLUS/ZERO PLUS2系列，要么自己找原理图找出UBOOT脚，把它连接到GND让其低电平就能进入刷写模式，还有一个方法是刷特制的sd卡镜像进入刷写模式。

# linux {#linux}

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

### 线刷LINUX（仅适用H3/H5）



