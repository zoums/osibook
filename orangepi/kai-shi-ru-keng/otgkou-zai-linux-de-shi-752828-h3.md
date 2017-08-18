# OTG口在Linux的使用\(H3\)

不多说。。。直接上图。。

![](/assets/3-1.png)

---

#### 还是多说几下好了。。。

打开serial串口模式在opi以便直接连micro usb口调试

先

```
mkdir -p /etc/systemd/system/serial-getty@ttyGS0.service.d
```

然后

```
sudo nano /etc/systemd/system/serial-getty@ttyGS0.service.d/10-switch-role.conf
```

加入

```
[Service]
ExecStartPre=-/bin/sh -c "echo 2 > /sys/bus/platform/devices/sunxi_usb_udc/otg_role"
```

用Ctrl-O回车保存，Ctrl-X键退出。。（其他文本编辑器自便）

最后

```
sudo systemctl --no-reload enable serial-getty@ttyGS0.service
sudo echo "ttyGS0" >> $SDCARD/etc/securetty
```

还不行加载模块

```
sudo modprobe g_serial
sudo echo g_serial >> /etc/modules
```



