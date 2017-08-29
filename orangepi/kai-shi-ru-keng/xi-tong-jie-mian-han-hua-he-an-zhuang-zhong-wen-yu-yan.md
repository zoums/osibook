# 系统界面汉化和安装中文语言

##### 收录自 [http://www.orangepi.cn/orangepibbscn/forum.php?mod=viewthread&tid=42&extra=page%3D1](http://www.orangepi.cn/orangepibbscn/forum.php?mod=viewthread&tid=42&extra=page%3D1)

##### [jacer](http://www.orangepi.cn/orangepibbscn/home.php?mod=space&uid=4428)

##### 有删改

### 适用于Ubuntu:

然后打开System-Adminstration\(或者settings\)-Language support，选Language选项卡然后按Install/Remove Language，将Chinese\(China\)中文简体打钩然后按Apply，安装结束后，将汉语Chinese，拖到English上面重启即可。可参照下面这个链接

[http://jingyan.baidu.com/article/36d6ed1f2e95f61bce488353.html](http://jingyan.baidu.com/article/36d6ed1f2e95f61bce488353.html)

### 适用于Debian系:

```
sudo dpkp-reconfigure locales
```

空格选择，回车确定，两次都选择zh\_CN.UTF-8 。

### 上面不行的可以试试这样：

打开终端terminal,输入如下命令后回车，

```
sudo apt-get install --reinstall locales
```

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

nano是Ctrl-O然后回车保存，Crtl-x退出。其他文本编辑器自便。

然后安装中文字体

```
sudo apt-get install ttf-wqy-zenhei
```

需要其他字体的自己找。

如需HOME文件夹也为中文，可以删除/home/orangepi/.config下面文件夹中文件user-dirs.dirs和user-dirs.locale然后重启。

### 附：

在Linux中通过locale来设置程序运行的不同语言环境，locale由 ANSI C提供支持。locale的命名规则为\_.，如zh\_CN.GBK，zh代表中文， CN代表大陆地区，GBK表示字符集。在locale环境中，有一组变量，代表国际化环境中的不同设置：

```
LC_COLLATE，定义该环境的排序和比较规则
LC_CTYPE，用于字符分类和字符串处理，控制所有字符的处理方式，包括字符编码，字符是单字节还是多字节，如何打印等。是最重要的一个环境变量。 LC_MONETARY，货币格式
LC_NUMERIC，非货币的数字显示格式
LC_TIME，时间和日期格式
LC_MESSAGES，提示信息的语言。
另外还有一个LANGUAGE参数，它与LC_MESSAGES相似，但如果该参数一旦设置，则LC_MESSAGES参数就会失效。 LANGUAGE参数可同时设置多种语言信息，如LANGUAGE="zh_CN.GB18030:zh_CN.GB2312:zh_CN"。
LANG，LC_*的默认值，是最低级别的设置，如果LC_*没有设置，则使用该值。类似于 LC_ALL
LC_ALL，它是一个宏，如果该值设置了，则该值会覆盖所有LC_*的设置值。注意，LANG的值不受该宏影响
```



