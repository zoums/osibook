# script.bin的配置与转换

本文出自哪就不知道了。。反正我自己根据OPI改改内容

---

#### 你是否经常看见其他帖子里或者其他人提到要修改script.bin或script.fex ，但你又不知道怎么改。

#### 其实 script.bin就是script.fex通过 fex2bin生成的，script.fex是文本格式，方便人修改，修改好之后转换为script.bin二进制格式方便机器读取。

本文是假设 用户的orangepi是安装的ubuntu/debian 而且 已连接上网、已安装编译工具、已安装git的情况下。

如果没安装的，可以先执行这句来安装编译工具和git:

```
sudo apt-get install build-essential make gcc g++ git-core libusb-1.0-0-dev
```

我们就说说在哪里修改这个文件，一般在在第一个分区\(/dev/mmcblk0p1\)中，这是boot分区，一些系统挂载在/media/boot下。。特指官方大部分系统。。。/boot下是备份，。不过armbian是在/boot下的。

如果是sd卡，你可以用读卡器在PC上面把script.bin 拷贝出来修改，不过armbian不能在win上读取。。。我建议直接在板子上修改，很方便。

我以修改SD卡上的linux系统的script.bin配置为例：

1. 首先把fex2bin和bin2fex工具下载编译好：

```
git clone git://github.com/linux-sunxi/sunxi-tools.git
cd sunxi-tools
make
```

再ls查看你就会看见fex2bin 和 bin2fex了

注：Ubuntu的中已有sunxi-tools包，可直接通过sudo apt-get install sunxi-tools安装，附件中有Windows版sunxi-tools

2.将你要修改的script.bin拷贝出来。。。然而官方和大部分系统已经挂载在/media/boot下了。。这步挂载部分可以跳过。

```
mkdir /mnt/mmcp1
mount /dev/mmcblk0p1 /mnt/mmcp1
cp /mnt/mmcp1/script.bin ./
```

注：Windows上可直接插卡读取，或者windows版sunxi-tools附件中有现成的fex文件，论坛的系统大多挂载在/media/boot ，armbian在/boot 但是无法通过win读取

3.将刚刚拷贝过来的script.bin转为script.fex,然后修改script.fex

```
./bin2fex script.bin > ./script.fex
#将bin转为fex并写入到当前目录的script.fex文件注：如果输出的script.fex为空或者提示错误（据说官方系统都有这问题），请下载windows版的sunxi-tools，内附有script.fex
```

安装版的可以

```
bin2fex script.bin > ./script.fex
```

然后

```
nano ./script.fex   #编辑里面的内容，然后保存退出
```

各种文本编辑器自便，nano是Ctrl-O回车保存，Ctrl-X退出

\#比如我要HDMI转dvi支持

\[hdmi\_para\]那项加这两行

```
hdcp_enable = 0
hdmi_cts_compatibility = 1
```

4.将修改过的script.fex转回script.bin并放回原处

```
#编译版：
./fex2bin script.fex > ./script.bin
#安装版：
fex2bin script.fex > ./script.bin
```

放回原位

```
cp ./script.bin /media/boot
umount /mnt/mmcp1
```

然后重启动系统，你的新script配置就生效了

#### 附件

找不到script.fex的或者原来script.bin损坏的可以去[https://github.com/armbian/build/tree/master/config/fex](https://github.com/armbian/build/tree/master/config/fex)

链接: [http://pan.baidu.com/s/1gf4A73H](http://pan.baidu.com/s/1gf4A73H) 密码: rgfh

