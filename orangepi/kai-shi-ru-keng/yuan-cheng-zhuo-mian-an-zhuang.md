# OrangePi远程桌面安装

软件有很多，VNC、XRDP、X2GO等,X2GO功能多些，桌面色彩还原很好不 需要多少配置，其次XRDP、VNC，xrdp比vnc更安全些。

1、安装vnc

```
sudo apt-get install tightvncserver
```

![](file:///D:/Temp/msohtmlclip1/01/clip_image001.jpg)

2、vncpasswd设置密码 ；不运行此命令，直接运行vncserver也会提示你 输入密码,一共两次，当提示是否需要只读密码时选N即可。

![](file:///D:/Temp/msohtmlclip1/01/clip_image004.jpg)

3、通过vncserver或者vncserver:1\(vncserver:2\)……等开启一个或多个桌面， 也可以通过完整的命令传送更多参数，如

vncserver :1 -geometry 1024x768 -depth 16 -pixelformat rgb565

（注意，如果安装时提示找不到字体，可以参考本章第二篇，如果还有错误，请运行sudo apt-get update更新下软件源再尝试安装）

