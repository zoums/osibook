# OrangePi网线直连电脑（windows）

### 1. 打开控制面板\网络和 Internet\网络连接

![](/assets/wanjia/wanxian/import1.png)

### 2. 选中无线网络连接，右键选择属性

![](/assets/wanjia/wanxian/import2.png)

### 3. 选择 共享

![](/assets/wanjia/wanxian/import3.png)

### 4.点击 允许其他网络用户通过此计算机的 Internet 连接来连接 后，点击确定

![](/assets/wanjia/wanxian/import4.png)

### 5. 打开命令行，输入 arp -a ,回车，得到

![](/assets/wanjia/wanxian/import5.png)

#### 这个192.168.137.1下的动态ip即为pi的地址，不同的电脑分配的ip是不一样的

### 6. 使用 putty 或 x shell 连接

![](/assets/wanjia/wanxian/import6.png)

#### 点击 是

##### 输入 用户名（默认）（root/orangepi） 回车\(用户密码根据自己的系统来决定\)

##### 输入 密码 （默认）（root/orangepi） 回车

![](/assets/wanjia/wanxian/import7.png)

### 7. 连接完成

###### By 约瑟夫，大蚂蟥 test-2



