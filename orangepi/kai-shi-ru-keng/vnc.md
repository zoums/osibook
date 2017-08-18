# Raspberry Pi：设置 tight VNC Server 为开机启动￼ 

别人的文章。。。放这里没毛病吧。。。

原文链接：http://blog.swineson.tk/raspberry-pi%ef%bc%9a%e8%ae%be%e7%bd%ae-tight-vnc-server-%e4%b8%ba%e5%bc%80%e6%9c%ba%e5%90%af%e5%8a%a8/

#### Jamesits 2013-11-24 10:13:00

#### 网上看了自动启动 VNC Server 的方法，但是由于懒，脚本都不写 Init Info，导致更新启动项时出现 LSB Tags 等缺失的警告。现将必要的信息补充完整如下。

首先把以下内容写入 /etc/init.d/tightvncserver

```
#!/bin/sh
### BEGIN INIT INFO
# Provides: tightvncserver
# Required-Start: $syslog $remote_fs $network
# Required-Stop: $syslog $remote_fs $network
# Default-Start: 2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: Starts VNC Server on system start.
# Description: Starts tight VNC Server. Script written by James Swineson.
### END INIT INFO
# /etc/init.d/tightvncserver
VNCUSER='pi'
case "$1" in
 start)
 su $VNCUSER -c '/usr/bin/tightvncserver :1'
 echo "Starting TightVNC Server for $VNCUSER"
 ;;
 stop)
 pkill Xtightvnc
 echo "TightVNC Server stopped"
 ;;
 *)
 echo "Usage: /etc/init.d/tightvncserver {start|stop}"
 exit 1
 ;;
esac
exit 0
```



然后运行：

```
sudo chmod 755 /etc/init.d/tightvncserver
sudo update-rc.d tightvncserver defaults
```

重启看效果吧。

取消开机启动也很简单，就一行代码：

```
sudo update-rc.d -f tightvncserver remove
```

原文链接：http://blog.swineson.tk/raspberry-pi%ef%bc%9a%e8%ae%be%e7%bd%ae-tight-vnc-server-%e4%b8%ba%e5%bc%80%e6%9c%ba%e5%90%af%e5%8a%a8/

