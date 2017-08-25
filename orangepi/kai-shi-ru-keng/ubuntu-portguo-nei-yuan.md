# ubuntu-port国内源

ubuntu把arm等源移到ubuntu-port去了，官方的源鬼死慢，于是来分享个国内源

注意，本人遇到更新卡在正在等待报头，后来把其中https改成http就好了。

## 中科大

```
# 默认注释了源码仓库，如有需要可自行取消注释
deb https://mirrors.ustc.edu.cn/ubuntu-ports/ xenial main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu-ports/ xenial main main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-updates main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-backports main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-security main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-proposed main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-proposed main restricted universe multiverse
```

其中wily是ubuntu版本号根据自己使用的版本替换，以root权限改 /etc/apt/sources.list 即可

```
ubuntu14.04: trusty

ubuntu15.04: wily

ubuntu16.04:xenial
```

出现访问不了的可以试试下面解决方法\(IPV6出问题用IPV4之类\)：

[mirrors.ustc.edu.cn](https://mirrors.ustc.edu.cn/)由中国科学技术大学、中国科学技术大学网络信息中心支持，USTC LUG 维护。

### 机器域名 {#机器域名}

IPv4/v6: mirrors.ustc.edu.cn （能解析出教育网/电信/移动/v6地址）  
v4only: mirrors4.ustc.edu.cn （能解析出教育网/电信/移动地址）  
v6only: mirrors6.ustc.edu.cn

在有些地方DNS会解析出电信地址，但使用教育网地址访问更快，这时可以通过修改 hosts 指定强制使用教育网地址访问。

教育网IP：202.38.95.110  
电　信IP：202.141.160.110  
移　动IP：202.141.176.110  
　IPv6：　2001:da8:d800:95::110

源帮助：[http://mirrors.ustc.edu.cn/help/ubuntu-ports.html](http://mirrors.ustc.edu.cn/help/ubuntu-ports.html)

## 清华源

```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ wily main multiverse restricted universe
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ wily-backports main multiverse restricted universe
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ wily-proposed main multiverse restricted universe
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ wily-security main multiverse restricted universe
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ wily-updates main multiverse restricted universe
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ wily main multiverse restricted universe
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ wily-backports main multiverse restricted universe
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ wily-proposed main multiverse restricted universe
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ wily-security main multiverse restricted universe
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ wily-updates main multiverse restricted universe
```

其中wily是ubuntu版本号根据自己使用的版本替换，以root权限改 /etc/apt/sources.list 即可

```
ubuntu14.04: trusty

ubuntu15.04: wily

ubuntu16.04:xenial
```



