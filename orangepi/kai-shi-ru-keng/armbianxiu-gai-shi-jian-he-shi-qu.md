# armbian修改时间和时区

##### 收录自 [http://www.cnblogs.com/xwdreamer/archive/2013/11/06/3409947.html](http://www.cnblogs.com/xwdreamer/archive/2013/11/06/3409947.html)

##### [xwdreamer]

##### 有删改

文章应该适合Ubuntu和Debian两个系统，如果你的时间有问题，可以参照本文

## 修改时区

### 查询时间

**连接SSH或者打开终端，执行：**
```
data -R
Tue, 29 Aug 2017 00:20:02 +0000
```
结果时区是+000

在中国一般需要的需要的是东八区，这里如果不是，需要重新设置

### 查询时区

**连接SSH或者打开终端，执行：**
```
data -R
```
结果时区是+000

在中国一般需要的需要的是东八区，这里如果不是，需要重新设置

### 修改时区

**执行：（root用户就不要加sudo了）**
```
sudo tzselect
```
**选择区域：亚洲**
```
Please identify a location so that time zone rules can be set correctly.
Please select a continent, ocean, "coord", or "TZ".
 1) Africa
 2) Americas
 3) Antarctica
 4) Asia
 5) Atlantic Ocean
 6) Australia
 7) Europe
 8) Indian Ocean
 9) Pacific Ocean
10) coord - I want to use geographical coordinates.
11) TZ - I want to specify the time zone using the Posix TZ format.
#? 4
```
**选择国家：中国**
```
Please select a country whose clocks agree with yours.
 1) Afghanistan		  18) Israel		    35) Palestine
 2) Armenia		  19) Japan		    36) Philippines
 3) Azerbaijan		  20) Jordan		    37) Qatar
 4) Bahrain		  21) Kazakhstan	    38) Russia
 5) Bangladesh		  22) Korea (North)	    39) Saudi Arabia
 6) Bhutan		  23) Korea (South)	    40) Singapore
 7) Brunei		  24) Kuwait		    41) Sri Lanka
 8) Cambodia		  25) Kyrgyzstan	    42) Syria
 9) China		  26) Laos		    43) Taiwan
10) Cyprus		  27) Lebanon		    44) Tajikistan
11) East Timor		  28) Macau		    45) Thailand
12) Georgia		  29) Malaysia		    46) Turkmenistan
13) Hong Kong		  30) Mongolia		    47) United Arab Emirates
14) India		  31) Myanmar (Burma)	    48) Uzbekistan
15) Indonesia		  32) Nepal		    49) Vietnam
16) Iran		  33) Oman		    50) Yemen
17) Iraq		  34) Pakistan
#? 9
```
**选择时区：北京时间**
```
Please select one of the following time zone regions.
1) Beijing Time
2) Xinjiang Time
#? 1
```
**确认验证：**
```
Therefore TZ='Asia/Shanghai' will be used.
Local time is now:	Tue Aug 29 08:19:36 CST 2017.
Universal Time is now:	Tue Aug 29 00:19:36 UTC 2017.
Is the above information OK?
1) Yes
2) No
#? 1

You can make this change permanent for yourself by appending the line
	TZ='Asia/Shanghai'; export TZ
to the file '.profile' in your home directory; then log out and log in again.

Here is that TZ value again, this time on standard output so that you
can use the /usr/bin/tzselect command in shell scripts:
Asia/Shanghai
```
**复制文件到/etc目录下**
```
sudo cp /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime
```
**更新时间**
```
sudo ntpdate time.windows.com
```
有时候会提示
```
ntpdate: command not found
```
我是在使用pi one armbian时出现的，那么执行
```
ntpd time.windows.com
```
**验证时间**
```
data -R
Tue, 29 Aug 2017 08:22:15 +0800
```
一切正常，补充一点，更改了时间尽快重启，或者强制更新下定时任务，此时定时任务并没有按照现在时间执行，而是按原来时间执行的

##修改时间

**修改时间**
```
sudo date -s MM/DD/YY //修改日期
sudo date -s hh:mm:ss //修改时间
```
**在修改时间以后，修改硬件CMOS的时间**
```
sudo hwclock --systohc //非常重要，如果没有这一步的话，后面时间还是不准
```