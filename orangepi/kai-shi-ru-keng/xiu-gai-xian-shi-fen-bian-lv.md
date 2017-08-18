# OrangePi 修改显示分辨率

## H3

H3系列的大部分已经有修改好分辨率的script.bin，把相应分辨率的script.bin改名script.bin放到boot分区相应位置，官方系统一般放到/media/boot

script.bin 链接: [http://pan.baidu.com/s/1kUCtAkf](http://pan.baidu.com/s/1kUCtAkf) 密码: 9u66

Armbian的可以用H3disp切换分辨率。

## H3/H5/A64

H3没有对应分辨率的script.bin,去下一章看相应教程，H5及A64看下一章转换dts和dtb的教程，修改如下参数

```
screen0_output_mode
```

可能screen不同，是screen\*的去看hdmi\_channel=\* 。

分辨率参数如下

```
0:480i 1:576i 2:480p 3:576p 4:720p50 5:720p60 6:1080i50 7:1080i60 8:1080p24 9:1080p50 10:1080p60
```

script.bin直接改数字。

找不到script.fex的可以去[https://github.com/armbian/build/tree/master/config/fex](https://github.com/armbian/build/tree/master/config/fex)

dtb文件得把参数转换为16进制数。

H5/A64还可以装sunxi-disp-tool看看（虽然官方H5的测试失败）

```
sunxi-disp-tool switch -mode 0xa
sunxi-disp-tool switch -mode 0x5
sunxi-disp-tool switch -name 720p
sunxi-disp-tool switch -name 1080p
sunxi-disp-tool switch -name 1280x720p60
```

装了sunxi-disp-tool后可以修改/boot/uEnv.txt中添加参数，如果已有optargs参数，去掉这句optargs在uEnv的optargs已有参数后面加上，以空格隔开：

```
optargs=disp.screen0_output_mode=720p60
```

找不到sunxi-disp-tool的可以去 [https://launchpad.net/~longsleep/+archive/ubuntu/ubuntu-pine64-flavour-makers 或](https://launchpad.net/~longsleep/+archive/ubuntu/ubuntu-pine64-flavour-makers)者自己编译 [https://github.com/longsleep/sunxi-disp-tool](https://github.com/longsleep/sunxi-disp-tool)



