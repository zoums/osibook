# WiringPi

OrangePi官方的WiringPi,看着写着支持全系列板子，具体不清楚，只在2G-IOT测试过。在我的Raspbian 2G-IOT上。

## 下载:

```
env GIT_SSL_NO_VERIFY=true
git clone https://github.com/OrangePiLibra/WiringPi.git
```

## 安装编译依赖：

```
i 安装源码需要的编译工具
sudo apt-get install gcc g++ make
```

## 编译安装WiringPi:

```
cd WiringPi
sudo ./build OrangePi_2G-IOT
sudo ./build OrangePi_2G-IOT install
```

## 尝试样例：

```
  cd WiringPi/example/OrangePi
  make OrangePi
  ./OrangePi
```



