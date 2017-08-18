# Orange pi使用1-Wire温度传感器DS18B20

#### 1、需要加载的模块

 ![](/assets/100852qq7rgrozif5ykceu.png)

可添加到/etc/modules中，或手动加载

```
sudo modprobe w1_therm w1_gpio w1_sunxi gpio_sunxi
```

#### 2、连接传感器

在script.bin中可找到

![](/assets/100847yl0lflcmcjh0cm08.png)

在GPIO中![](/assets/100850fcclk8e0kju00jud.jpg)

还有一个vcc随便找路5v连接就行。

![](/assets/100851mnq85ssp57h12p92.png)

由于我的是成品板，其他DS18B20 的IO口与VCC中间需接一个4.7K的上拉电阻。

#### 3、读取成功。

![](/assets/101240fodilml4y4xh6lyd.png)

![](/assets/101107cxin4rt44f5nirlu.png)

