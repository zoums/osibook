# 制作initrd注意的

##### 制作initrd后发现。。各种Initrd里面的东西没执行权限之类。。。原来是用了旧的格式。

cpio -c选项的是旧的ASCII码方式

cpio -H newc的是新的格式

