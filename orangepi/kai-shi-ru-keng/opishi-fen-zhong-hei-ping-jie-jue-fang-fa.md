# OPI十分钟黑屏解决方法

装了ubuntu server和x图形，十分钟后就黑屏了，于是解决方法如下

执行setterm -blank 0如果失效则在cmdline定义consoleblank=0 即可。

H5系列可以在boot分区下有uEnv.txt，加入一句，如果已有optargs参数，去掉这句optargs在uEnv的optargs已有参数后面加上，以空格隔开：

```
optargs=consoleblank=0
```

x图形黑屏的解决方法，执行

```
xset -dpms
```

要每次开机都应用，加入到/etc/rc.local的exit 0前的随意起一行。

