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
git clone https://github.com/kazukioishi/WiringOP.git -b h5
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
Type: Banana Pro, Revision: 1.2, Memory: 1024MB, Maker: LeMaker
```

iv 显示所有GPIO信息

```
gpio readall
```

```
 +-----+-----+----------+------+---+--OrangePiPC--+---+------+---------+-----+--+
 | BCM | wPi |   Name   | Mode | V | Physical | V | Mode | Name     | wPi | BCM |
 +-----+-----+----------+------+---+----++----+---+------+----------+-----+-----+
 |     |     |     3.3v |      |   |  1 || 2  |   |      | 5v       |     |     |
 |   2 |  -1 |    SDA.0 |      |   |  3 || 4  |   |      | 5V       |     |     |
 |   3 |  -1 |    SCL.0 |      |   |  5 || 6  |   |      | 0v       |     |     |
 |   4 |   6 | IO6 PA06 |  OUT | 0 |  7 || 8  |   |      | TxD3     |     |     |
 |     |     |       0v |      |   |  9 || 10 |   |      | RxD3     |     |     |
 |  17 |  -1 |     RxD2 |      |   | 11 || 12 | 0 | OUT  | IO1 PD14 | 1   | 18  |
 |  27 |  -1 |     TxD2 |      |   | 13 || 14 |   |      | 0v       |     |     |
 |  22 |  -1 |     CTS2 |      |   | 15 || 16 | 0 | OUT  | IO4 PC04 | 4   | 23  |
 |     |     |     3.3v |      |   | 17 || 18 | 0 | OUT  | IO5 PC07 | 5   | 24  |
 |  10 |  -1 |     MOSI |      |   | 19 || 20 |   |      | 0v       |     |     |
 |   9 |  -1 |     MISO |      |   | 21 || 22 |   |      | RTS2     |     |     |
 |  11 |  -1 |     SCLK |      |   | 23 || 24 |   |      | SPI-CE0  |     |     |
 |     |     |       0v |      |   | 25 || 26 |   |      | CE1      |     |     |
 |   0 |  -1 |    SDA.1 |      |   | 27 || 28 |   |      | SCL.1    |     |     |
 |   5 |   7 |  IO7 PA7 |  OUT | 0 | 29 || 30 |   |      | 0v       |     |     |
 |   6 |   8 |  IO8 PA8 |  OUT | 0 | 31 || 32 | 0 | OUT  | IO9 PG08 | 9   | 12  |
 |  13 |  10 | IO10 PA9 |  OUT | 0 | 33 || 34 |   |      | 0v       |     |     |
 |  19 |  12 | IO12PA10 |  OUT | 0 | 35 || 36 | 0 | OUT  | IO13PG09 | 13  | 16  |
 |  26 |  14 | IO14PA20 |  OUT | 0 | 37 || 38 | 0 | OUT  | IO15PG06 | 15  | 20  |
 |     |     |       0v |      |   | 39 || 40 | 0 | OUT  | IO16PG07 | 16  | 21  |
 +-----+-----+----------+------+---+----++----+---+------+----------+-----+-----+
 | BCM | wPi |   Name   | Mode | V | Physical | V | Mode | Name     | wPi | BCM |
 +-----+-----+----------+------+---+--OrangePIPC--+------+----------+-----+-----+
```



