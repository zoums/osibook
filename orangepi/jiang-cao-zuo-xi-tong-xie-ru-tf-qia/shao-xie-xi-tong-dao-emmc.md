# OrangePi烧写系统到EMMC\(全志\) {#-}

# 安卓 {#-}

卡量产烧入sdcard启动会有进度条。。等进度条完了拔卡重启就行或者phonixsuite按住板子上的升级键。。只有唯一的开机键的就是那开机键然后连接电脑用这个工具烧写

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
> `wget `[`https://raw.githubusercontent.com/zoums/osibook/master/assets/files/install_to_emmc.sh`](https://raw.githubusercontent.com/zoums/osibook/master/assets/files/install_to_emmc.sh)
>
> `chmod +x install__to__emmc.sh && ./install__to__emmc.sh`
>
> `(H5)`
>
> `wget `[`https://raw.githubusercontent.com/zoums/osibook/master/assets/files/OrangePi_install2EMMC.sh`](https://raw.githubusercontent.com/zoums/osibook/master/assets/files/OrangePi_install2EMMC.sh)
>
> `chmod +x OrangePi_install2EMMC.sh && ./OrangePi_install2EMMC.sh`

是armbian之类的可以执行nand-sata-install 实在不行又想尝试一下可以把卡或镜像dd到emmc

没图。。。没图。。。没图。。。。等哪天旁边有板子了就上图。。。。。

