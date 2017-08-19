# WiringOP

WiringOP是移植的WIringPi，基于WiringBP。

#### 安装和使用

a. 安装 WiringPi

i 安装源码需要的编译工具

```
sudo apt-get install gcc g++ make
```

ii 编译 GPIO 的 H5 的WiringOP库

```
git clone https: //github.com/kazukioishi/WiringOP.git -b h5
cd WiringOP
chmod +x . /build
sudo . /build
```

iii GPIO 打印信息

```
# gpio -v
gpio version: 2. 20
Copyright (c) 2012-2014 Gordon Henderson
This is free software with ABSOLUTELY NO WARRANTY.
For details type: gpio -warranty
Banana Pro Details:
Type: Banana Pro, Revision: 1. 2, Memory: 1024MB, Maker: LeMaker
```

iv 显示所有GPIO信息

```
gpio readall
```

```
+-----+-----+----------+------+---+-Orange Pi+---+---+------+---------+-----+--+
| BCM | wPi | Name | Mode | V | Physical | V | Mode | Name | wPi | BCM |
+-----+-----+----------+------+---+----++----+---+------+----------+-----+-----+
| | | 3. 3v | | | 1 | | 2 | | | 5v | | |
| 12 | 8 | SDA. 0 | ALT5 | 0 | 3 | | 4 | | | 5V | | |
| 11 | 9 | SCL. 0 | ALT5 | 0 | 5 | | 6 | | | 0v | | |
| 6 | 7 | GPIO. 7 | ALT3 | 0 | 7 | | 8 | 0 | ALT5 | TxD3 | 15 | 13 |
| | | 0v | | | 9 | | 10 | 0 | ALT5 | RxD3 | 16 | 14 |
| 1 | 0 | RxD2 | ALT5 | 0 | 11 | | 12 | 0 | ALT3 | GPIO. 1 | 1 | 110 |
| 0 | 2 | TxD2 | ALT5 | 0 | 13 | | 14 | | | 0v | | |
| 3 | 3 | CTS2 | ALT5 | 0 | 15 | | 16 | 0 | ALT3 | GPIO. 4 | 4 | 68 |
| | | 3. 3v | | | 17 | | 18 | 0 | ALT3 | GPIO. 5 | 5 | 71 |
| 64 | 12 | MOSI | ALT4 | 0 | 19 | | 20 | | | 0v | | |
| 65 | 13 | MISO | ALT0 | 0 | 21 | | 22 | 0 | ALT5 | RTS2 | 6 | 2 |
| 66 | 14 | SCLK | ALT4 | 0 | 23 | | 24 | 0 | ALT4 | CE0 | 10 | 67 |
| | | 0v | | | 25 | | 26 | 0 | ALT3 | GPIO. 11 | 11 | 21 |
| 19 | 30 | SDA. 1 | ALT4 | 0 | 27 | | 28 | 0 | ALT4 | SCL. 1 | 31 | 18 |
| 7 | 21 | GPIO. 21 | ALT3 | 0 | 29 | | 30 | | | 0v | | |
| 8 | 22 | GPIO. 22 | ALT3 | 0 | 31 | | 32 | 0 | ALT5 | RTS1 | 26 | 200 |
| 9 | 23 | GPIO. 23 | ALT3 | 0 | 33 | | 34 | | | 0v | | |
| 10 | 24 | GPIO. 24 | ALT3 | 0 | 35 | | 36 | 0 | ALT5 | CTS1 | 27 | 201 |
| 20 | 25 | GPIO. 25 | OUT | 1 | 37 | | 38 | 0 | ALT5 | TxD1 | 28 | 198 |
| | | 0v | | | 39 | | 40 | 0 | ALT5 | RxD1 | 29 | 199 |
+-----+-----+----------+------+---+----++----+---+------+----------+-----+-----+
| BCM | wPi | Name | Mode | V | Physical | V | Mode | Name | wPi | BCM |
+-----+-----+----------+------+---+-Orange Pi+---+------+----------+-----+-----+
```



