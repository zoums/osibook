# OrangePi远程桌面安装

软件有很多，VNC、XRDP、X2GO等,X2GO功能多些，桌面色彩还原很好不 需要多少配置，其次XRDP、VNC，xrdp比vnc更安全些。

1、安装vnc

```
sudo apt-get install tightvncserver
```

![](/assets/clip_image001.jpg)

2、vncpasswd设置密码 ；不运行此命令，直接运行vncserver也会提示你 输入密码,一共两次，当提示是否需要只读密码时选N即可。

![](/assets/clip_image004.jpg)

3、通过vncserver或者vncserver :1\(vncserver :2\)……等开启一个或多个桌面， 也可以通过完整的命令传送更多参数，如

vncserver :1 -geometry 1024x768 -depth 16 -pixelformat rgb565

（注意，如果安装时提示找不到字体，可以参考本章第二篇，如果还有错误，请运行sudo apt-get update更新下软件源再尝试安装）

4、如果连接VNC灰屏，一般是桌面环境挂了或者没法启动。。可以配置~/.vnc/xstartup文件，再其后修改添加桌面环境的启动参数，下面列出一些桌面环境的启动参数。

LXDE

```
startlxde &
```

GNOME

```
gnome-session &
```

或者

```
gnome-panel &

gnome-settings-daemon &

metacity &

nautilus &
```

XFCE4

```
startxfce4 &
```

或者

```
x-session-manager & xfdesktop & xfce4-panel &  
xfce4-menu-plugin &  
xfsettingsd &  
xfconfd &  
xfwm4 &
```

KDE

```
startkde &
```

上面都不行也可以试试

```
sudochmod a+x /etc/X11/xinit/xinitrc
sudo chmod +x ~/.vnc/xstartup
```

修改完毕后可以执行如下命令关闭VNC再执行第三步的相应命令启动vnc再连接上去看看。

```
vncserver -kill :1
```

##### 其他桌面的配置可以去网上查或者看这种桌面的说明文档

##### 还是失败你可以试试换个系统，或者换张卡，或者换个板子，或者换个电源适配器，或者换人，或者来波修复工具得了/。。。比如锤子。。。。当然。。这是个玩笑。。。不过真的很有用。



