# 扩展分区大小

#### 烧写OrangePi镜像后，发现可用空间太少怎么办？

于是查看磁盘状况发现有空闲空间没有被根分区使用，部分系统可以执行sudo fs\_resize来进行扩容，Armbian会自动扩容（发现没有扩容的可以重启再看看），还有部分系统可以执行sudo resize\_part，如上方法都失效则可以用分区工具手动扩容。先执行 wget https://raw.githubusercontent.com/OrangePiLibra/OrangePiH5\_scripts/master/platform-scripts/resize\_rootfs.sh，然后sh resize\_rootfs.sh

