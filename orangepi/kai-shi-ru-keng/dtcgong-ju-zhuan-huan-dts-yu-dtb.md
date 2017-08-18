# dtc工具转换dts与dtb

在OPI的H5板子上虽然转换成了，似乎没卵用。。不过有时用主线内核的时候还是有点用的。。

dts转dtb:

```
dtc -I dts -O dtb -o xxx.dtb xxx.dts
```

dtb转dts

```
dtc -I dtb -O dts -o xxx.dts xxx.dtb
```

至于dtb文件在哪。。。一般在boot分区或者/boot下。

