# Serial\(Python\)

### 安装模块

```
pip install pyserial
```

### 基本用法

#### 定义端口

```
ser = serial.Serial(port, 115200)
```

例如ser = serial.Serial\(/dev/ttyS2\) 是使用/dev/ttyS2这个串口，OrangePi一般有uart1-3分别对应/dev/ttyS1-3。

#### 操作串口

```
print ser.portstr #串口名
ser.write(“hello") #往串口里面写数据
ser.close() #关闭ser表示的串口
ser.open() #打开定义的串口
ser = serial.Serial('COM1', 115200) #定义串口并设定波特率
data = ser.read() #读1个字符
data = ser.read(20) #读20个字符
data = ser.readline() #读一行，以/n结束，要是没有/n就一直读，阻塞。
data = ser.readlines()和ser.xreadlines() #都需要设置超时时间
ser.timeout=1 #设置超时时间
ser.baudrate = 9600 #设置波特率
ser #查看当前串口的状态
ser.isOpen() #查看这个串口是否已经被打开
```

### 参考链接

[http://shenwang.blog.ustc.edu.cn/python-%E4%B8%B2%E5%8F%A3%E6%A8%A1%E5%9D%97pyserial/](http://shenwang.blog.ustc.edu.cn/python-串口模块pyserial/)

[https://github.com/fsilvasampaio/py\_read\_serial/blob/master/readserial.py](https://github.com/fsilvasampaio/py_read_serial/blob/master/readserial.py)

[http://pythonhosted.org/pyserial/](http://pythonhosted.org/pyserial/)

[http://blog.csdn.net/xhao014/article/details/7640568](http://blog.csdn.net/xhao014/article/details/7640568)

