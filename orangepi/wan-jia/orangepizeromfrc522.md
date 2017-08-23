# OrangePiZeroMFRC522

### 安装

```
git clone https://github.com/BiTinerary/OrangePiZeroMFRC522.git && bash ./OrangePiZeroMFRC522/getAllTheStuff.sh
```

或者自己动手

```
apt-get install python-dev -y
apt-get install python-pip -y
pip install --upgrade pip
pip install setuptools

git clone https://github.com/rm-hull/OPi.GPIO.git
cd OPi.GPIO
pip install .

cd ..
git clone https://github.com/lthiery/SPI-Py.git
cd SPI-Py
pip install .

cd ..
git clone https://github.com/BiTinerary/OrangePiZeroMFRC522.git
python ./OrangePiZeroMFRC522/MFRC522-python/Read.py
```

### 连接

OrangePi Zero的接法（用SPI1，因为SPI0被nor flash占用）

| MFRC522 | OPi Zero Pin Number | Pin Function |
| :--- | :--- | :--- |
| SDA | Pin 24 | SPI1\_CS/PA13 |
| SCK | Pin 23 | SPI1CLK/PA14 |
| RST | Pin 22 | UART2\_RTS/PA02 |
| MISO | Pin 21 | SPI1\_MISO/PA16 |
| MOSI | Pin 19 | SPI1\_MOSI/PA15 |
| GND | Pin 6 | GND |
| 3.3v | Pin 12 | 3.3v |

其他OPI H2+/H3 系列板子自行查看SPI1接口定义连接，想用SPI0去MFRC522-python目录找到**MFRC522.py**文件在第110行把spidev1.0改成spidev0.0。

#### 获取数据

```
python ./OrangePiZeroMFRC522/MFRC522-python/Read.py
```

##### ![](https://github.com/BiTinerary/OrangePiZeroMFRC522/raw/master/gitImgs/821.jpg)

---

##### 更多信息可访问

[https://github.com/BiTinerary/OrangePiZeroMFRC522](https://github.com/BiTinerary/OrangePiZeroMFRC522)

