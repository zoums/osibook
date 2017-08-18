# Linux下3.5mm口tv输出支持

1、按照本章第二篇修改boot分区的script.bin。

2、修改参数：

```
output_type=2
cvbs_channel=1
cvbs_mode=11
screen1_output_type=2
screen1_output_mode=11
tv_used=1
```

3、按教程转换回来script.bin替换原来的。

4、如果还不能输出请在linux的/etc/modules加一行tv

##### 注：cvbs\_channel可以是1和0，分别对应FB1和0，如果是0，则其他参数是screen0\_output\_mode和screen0\_output\_type



