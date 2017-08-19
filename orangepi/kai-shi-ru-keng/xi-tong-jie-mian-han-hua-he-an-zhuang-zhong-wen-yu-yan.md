# 系统界面汉化和安装中文语言

打开终端terminal,输入如下命令后回车，

```
sudo apt-get install --reinstall locales
```

然后打开System-Adminstration-Language support，选Language选项卡然后按Install/Remove Language，将Chinese\(China\)中文简体打钩然后按Apply，安装结束后，将汉语Chinese，拖到English上面重启即可。可参照下面这个链接

[http://jingyan.baidu.com/article/36d6ed1f2e95f61bce488353.html](http://jingyan.baidu.com/article/36d6ed1f2e95f61bce488353.html)

执行

```
sudo nano /etc/default/locale
```

修改

```
LANG="zh_CN.UTF-8"
LANGUAGE="zh_CN"
LC_NUMERIC="zh_CN.UTF-8"
LC_TIME="zh_CN.UTF-8"
LC_MONETARY="zh_CN.UTF-8"
LC_PAPER="zh_CN.UTF-8"
LC_IDENTIFICATION="zh_CN.UTF-8"
LC_NAME="zh_CN.UTF-8"
LC_ADDRESS="zh_CN.UTF-8"
LC_TELEPHONE="zh_CN.UTF-8"
LC_MEASUREMENT="zh_CN.UTF-8"
```

nano是Ctrl-O然后回车保存，Crtl-x退出。

如需HOME文件夹也为中文，可以删除/home/orangepi/.config下面文件夹中文件

**user-dirs.dirs**

和user-dirs.locale然后重启。

