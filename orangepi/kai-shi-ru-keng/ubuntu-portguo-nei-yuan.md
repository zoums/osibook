# ubuntu-port国内源

ubuntu把arm等源移到ubuntu-port去了，官方的源鬼死慢，于是来分享个国内源

```
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ wily main multiverse restricted universe
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ wily-backports main multiverse restricted universe
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ wily-proposed main multiverse restricted universe
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ wily-security main multiverse restricted universe
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ wily-updates main multiverse restricted universe
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ wily main multiverse restricted universe
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ wily-backports main multiverse restricted universe
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ wily-proposed main multiverse restricted universe
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ wily-security main multiverse restricted universe
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ wily-updates main multiverse restricted universe
```

其中wily是ubuntu版本号根据自己使用的版本替换，以root权限改 /etc/apt/sources.list 即可

```
ubuntu14.04: trusty

ubuntu15.04: wily

ubuntu16.04:xenial
```



顺带一提。。清华源也有。。

