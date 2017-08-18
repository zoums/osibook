# 将操作系统写入 TF 卡 {#-tf-}

---

## 1、怎样将操作系统（除 Android 系统外）写入 TF 卡中 {#1-android-tf-}

---

### Windows: {#windows-}

#### a. 把 TF 卡插入电脑中，TF 卡的容量必须比操作系统镜像大，通常需要 4GB 或更大的容量 {#a-tf-tf-4gb-}

#### b. 格式化 TF 卡 {#b-tf-}

##### i. 下载 TF 卡格式化工具，例如 TF Formatter，下载地址 {#i-tf-tf-formatter-}

###### [https://www.sdcard.org/downloads/formatter\_4/eula\_windows/](https://www.sdcard.org/downloads/formatter_4/eula_windows/) {#https-www-sdcard-org-downloads-formatter_4-eula_windows-}

##### ii. 解压下载的文件，并运行 setup.exe {#ii-setup-exe}

##### iii. 在 "选项设置" 选项里, 设置 "格式化类型" 选项为快速格式化, "逻辑大 小调整" 选项为 "开启\(ON\)" {#iii-on-}

![](https://zoums.github.io/amWiki/images/001-01/image001.jpg "格式化选项")

##### iv. 确认插入的 TF 卡盘符和选择的盘符一致 {#iv-tf-}

##### v. 点击 “格式化” 按钮 {#v-}

#### c. 从下载页面下载操作系统镜像文件，页面地址如下： {#c-}

##### [http://www.orangepi.cn/downloadresourcescn/](http://www.orangepi.cn/downloadresourcescn/) {#http-www-orangepi-cn-downloadresourcescn-}

#### d. 解压下载的文件（除 Android 系统外的系统可用该方法来烧写，Android 系 统需要另外的模式来烧录，下面会有介绍） {#d-android-android-}

#### e. 右键单击下载的文件，选择 “解压文件” {#e-}

#### f. 写入镜像文件到 TF 卡 {#f-tf-}

##### i. 下载镜像写入工具，例如 Win32Diskimager，下载页面 {#i-win32diskimager-}

###### [http://sourceforge.net/projects/win32diskimager/files/Archive/，](http://sourceforge.net/projects/win32diskimager/files/Archive/，)安装并打开该工具 {#http-sourceforge-net-projects-win32diskimager-files-archive-}

##### ii. 选择已经解压的镜像文件路径 {#ii-}

![](https://zoums.github.io/amWiki/images/001-01/image004.jpg "烧写Linux")

##### iii. 点击 “Write” 按钮，耐心等待镜像写入 {#iii-write-}

##### iv. 镜像写入完成后，点击“Exit”按钮 {#iv-exit-}

---

### Linux: {#linux-}

#### a. 把 TF 卡插入电脑中，TF卡的容量必须比操作系统镜像大，通常需要 4GB或 更大的容量 {#a-tf-tf-4gb-}

#### b. 格式化 TF 卡 {#b-tf-}

##### i. 运行 fdisk –l 命令确认 TF 卡的盘符 {#i-fdisk-l-tf-}

##### ii. 运行 umount /dev/sdx 去卸载 TF 卡的所有分区 {#ii-umount-dev-sdx-tf-}

##### iii.运行 sudo fdisk /dev/sdx 命令. 使用 o 命令去删除 TF 卡的所有分区， 然后使用 n 命令去添加一个新的分区，最后使用 w 命令保存退出 {#iii-sudo-fdisk-dev-sdx-o-tf-n-w-}

##### iv. 运行 sudo mkfs.vfat /dev/sdx1 命令去格式化刚生成的 TF 卡分区为 FAT32 格式 {#iv-sudo-mkfs-vfat-dev-sdx1-tf-fat32-}

**\(根据你的 TF 卡盘符来替换x \)**_你也可以跳过这一步，因为 Linux 下的 dd 命令会自动格式化 TF 卡 也可以使用 PhoenixCard 工具”恢复卡”来格式化 TF 卡_

#### c. 从下载页面下载操作系统镜像文件，页面地址如下： {#c-}

###### [http://www.orangepi.cn/downloadresourcescn/](http://www.orangepi.cn/downloadresourcescn/) {#http-www-orangepi-cn-downloadresourcescn-}

#### d. 解压下载的文件（除 Android 系统外的系统可用该方法来烧写，Android 系 统需要另外的模式来烧写，下面会有介绍）右键单击下载的文件，选择 “解压文 件” {#d-android-android-}

#### e. 写入镜像文件到 TF 卡。 {#e-tf-}

##### i. 运行 sudo fdisk –l 命令确认 TF 卡的盘符 {#i-sudo-fdisk-l-tf-}

##### ii. 确认镜像文件的 hash key 和下载页面提供的一致（可选） sha1sum \[path\]/\[imagename\] 这将会输出一长串数字，应该和你下载的镜像页面的"SHA-1" 那一行匹配 {#ii-hash-key-sha1sum-path-imagename-sha-1-}

##### iii. 运行 umount /dev/sdxx 命令卸载 TF 卡的所有分区 {#iii-umount-dev-sdxx-tf-}

##### iv. 运行 sudo dd bs=4M if=\[path\]/\[imagename\] of=/dev/sdx 命令去写入镜像文件。 耐心等待镜像写入。你可以使用 sudo pkill –USR1 –n –x dd 命令去查看烧写进度 {#iv-sudo-dd-bs-4m-if-path-imagename-of-dev-sdx-sudo-pkill-usr1-n-x-dd-}

---

## 2、Android 系统镜像文件写入 TF 卡 {#2-android-tf-}

### Android 系统镜像文件不能在 Linux 环境下使用 dd 命令或者在 Window 环境用 Win32 Diskimager 工具来写入 TF 卡。需要使用工具 PhoenixCard 来写入。 {#android-linux-dd-window-win32-diskimager-tf-phoenixcard-}

### a. 下载 Android 系统和 PhoenixCard 烧写工具 {#a-android-phoenixcard-}

#### PhoenixCard 从下面网页中下载：[http://pan.baidu.com/share/link?shareid=2785461830&uk=1077680202](http://pan.baidu.com/share/link?shareid=2785461830&uk=1077680202)Android 系统从下面的网页中下载： {#phoenixcard-http-pan-baidu-com-share-link-shareid-2785461830-uk-1077680202-android-}

##### [http://www.orangepi.cn/downloadresourcescn/](http://www.orangepi.cn/downloadresourcescn/) {#http-www-orangepi-cn-downloadresourcescn-}

### b. 格式化 TF 卡 {#b-tf-}

### c. 检查插入的 TF 卡是否与选择的盘符一致，单击“恢复卡”按钮，开始格式 TF {#c-tf-tf}

![](https://zoums.github.io/amWiki/images/001-01/image006.jpg "恢复卡")

#### 格式化 TF 卡成功后，单击“确定”按钮。 {#-tf-}

![](https://zoums.github.io/amWiki/images/001-01/image008.jpg "恢复卡完毕")

### c. 然后开始将 Android 系统写入 TF 卡中，请注意下图红色标记的地方。 {#c-android-tf-}

![](https://zoums.github.io/amWiki/images/001-01/image010.jpg "烧写准备")

#### 单击“烧录”按钮，开始写入 TF 卡，等待烧录完成。 {#-tf-}

#### Android 系统成功烧写完成后。单击“退出” 按钮，弹出 TF 卡。 {#android-tf-}

![](https://zoums.github.io/amWiki/images/001-01/image012.jpg "烧写完毕")

---

## 3、 Armbian 镜像文件写入 TF 卡 {#3-armbian-tf-}

### a. TF 卡插入电脑中，TF 卡的容量必须比操作系统镜像大，通常需要 8GB 或更 大的容量。 {#a-tf-tf-8gb-}

### b. 下载操作系统镜像文件，页面地址如下： {#b-}

#### [http://www.armbian.com/download/](http://www.armbian.com/download/)c. 烧录至 TF 卡\(镜像\) {#http-www-armbian-com-download-c-tf-}

#### i. 下载镜像写入工具，例如 Rufus ，下载页面:[https://rufus.akeo.ie/](https://rufus.akeo.ie/) {#i-rufus-https-rufus-akeo-ie-}

#### 打开工具 {#-}

#### ii. 选择已经解压的镜像文件路径。 {#ii-}

![](https://zoums.github.io/amWiki/images/001-01/image015.png "选择镜像")![](https://zoums.github.io/amWiki/images/001-01/image017.png "选择镜像")

#### ii. 点击开始按钮，耐心等待镜像写入 {#ii-}

![](https://zoums.github.io/amWiki/images/001-01/image019.png "开始烧写")

#### iv. 镜像写入完成后，点击“关闭”按钮。 {#iv-}



