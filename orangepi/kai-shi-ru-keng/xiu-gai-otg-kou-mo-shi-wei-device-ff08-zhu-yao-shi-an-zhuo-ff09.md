# 修改OTG口模式为device

执行

```
echo "2" > /sys/bus/platform/devices/sunxi_usb_udc/otg_role
```

你得先看看有没有这个文件，没有的话，那就试试这个路径

```
echo "2" > /sys/devices/platform/sunxi_otg/otg_role
```



