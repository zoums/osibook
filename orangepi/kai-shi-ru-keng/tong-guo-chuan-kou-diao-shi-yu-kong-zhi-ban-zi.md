# 通过串口调试与控制板子

&lt;!--  
 /\* Font Definitions \*/  
 @font-face  
	{font-family:宋体;  
	panose-1:2 1 6 0 3 1 1 1 1 1;  
	mso-font-alt:SimSun;  
	mso-font-charset:134;  
	mso-generic-font-family:auto;  
	mso-font-pitch:variable;  
	mso-font-signature:3 680460288 22 0 262145 0;}  
@font-face  
	{font-family:"Cambria Math";  
	panose-1:2 4 5 3 5 4 6 3 2 4;  
	mso-font-charset:0;  
	mso-generic-font-family:roman;  
	mso-font-pitch:variable;  
	mso-font-signature:-536870145 1107305727 0 0 415 0;}  
@font-face  
	{font-family:"\@宋体";  
	panose-1:2 1 6 0 3 1 1 1 1 1;  
	mso-font-charset:134;  
	mso-generic-font-family:auto;  
	mso-font-pitch:variable;  
	mso-font-signature:3 680460288 22 0 262145 0;}  
 /\* Style Definitions \*/  
 p.MsoNormal, li.MsoNormal, div.MsoNormal  
	{mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-qformat:yes;  
	mso-style-parent:"";  
	margin:0cm;  
	margin-bottom:.0001pt;  
	mso-pagination:none;  
	font-size:11.0pt;  
	font-family:"Times New Roman",serif;  
	mso-fareast-font-family:"Times New Roman";  
	mso-fareast-language:EN-US;}  
h1  
	{mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-qformat:yes;  
	mso-style-link:"标题 1 字符";  
	margin-top:0cm;  
	margin-right:0cm;  
	margin-bottom:0cm;  
	margin-left:7.0pt;  
	margin-bottom:.0001pt;  
	mso-pagination:none;  
	mso-outline-level:1;  
	font-size:22.0pt;  
	font-family:宋体;  
	mso-bidi-font-family:宋体;  
	mso-font-kerning:0pt;  
	mso-fareast-language:EN-US;}  
h2  
	{mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-qformat:yes;  
	mso-style-link:"标题 2 字符";  
	margin-top:.05pt;  
	margin-right:0cm;  
	margin-bottom:0cm;  
	margin-left:7.0pt;  
	margin-bottom:.0001pt;  
	mso-pagination:none;  
	mso-outline-level:2;  
	font-size:16.0pt;  
	font-family:"Times New Roman",serif;  
	mso-fareast-font-family:"Times New Roman";  
	mso-fareast-language:EN-US;}  
h5  
	{mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-qformat:yes;  
	mso-style-link:"标题 5 字符";  
	margin-top:0cm;  
	margin-right:0cm;  
	margin-bottom:0cm;  
	margin-left:7.0pt;  
	margin-bottom:.0001pt;  
	mso-pagination:none;  
	mso-outline-level:5;  
	font-size:14.0pt;  
	font-family:宋体;  
	mso-bidi-font-family:宋体;  
	mso-fareast-language:EN-US;}  
h6  
	{mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-qformat:yes;  
	mso-style-link:"标题 6 字符";  
	margin-top:.7pt;  
	margin-right:0cm;  
	margin-bottom:0cm;  
	margin-left:7.0pt;  
	margin-bottom:.0001pt;  
	mso-pagination:none;  
	mso-outline-level:6;  
	font-size:14.0pt;  
	font-family:"Times New Roman",serif;  
	mso-fareast-font-family:"Times New Roman";  
	mso-fareast-language:EN-US;  
	font-weight:normal;}  
p.MsoHeading7, li.MsoHeading7, div.MsoHeading7  
	{mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-qformat:yes;  
	mso-style-link:"标题 7 字符";  
	margin-top:0cm;  
	margin-right:0cm;  
	margin-bottom:0cm;  
	margin-left:7.0pt;  
	margin-bottom:.0001pt;  
	mso-pagination:none;  
	mso-outline-level:7;  
	font-size:13.5pt;  
	font-family:宋体;  
	mso-bidi-font-family:宋体;  
	mso-fareast-language:EN-US;  
	font-weight:bold;}  
p.MsoBodyText, li.MsoBodyText, div.MsoBodyText  
	{mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-qformat:yes;  
	mso-style-link:"正文文本 字符";  
	margin:0cm;  
	margin-bottom:.0001pt;  
	mso-pagination:none;  
	font-size:12.0pt;  
	font-family:"Times New Roman",serif;  
	mso-fareast-font-family:"Times New Roman";  
	mso-fareast-language:EN-US;}  
p.MsoListParagraph, li.MsoListParagraph, div.MsoListParagraph  
	{mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-qformat:yes;  
	margin-top:0cm;  
	margin-right:0cm;  
	margin-bottom:0cm;  
	margin-left:27.45pt;  
	margin-bottom:.0001pt;  
	text-indent:-21.0pt;  
	mso-pagination:none;  
	font-size:11.0pt;  
	font-family:"Times New Roman",serif;  
	mso-fareast-font-family:"Times New Roman";  
	mso-fareast-language:EN-US;}  
span.1  
	{mso-style-name:"标题 1 字符";  
	mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-locked:yes;  
	mso-style-link:"标题 1";  
	mso-ansi-font-size:22.0pt;  
	mso-bidi-font-size:22.0pt;  
	font-family:宋体;  
	mso-ascii-font-family:宋体;  
	mso-fareast-font-family:宋体;  
	mso-hansi-font-family:宋体;  
	mso-bidi-font-family:宋体;  
	font-weight:bold;}  
span.2  
	{mso-style-name:"标题 2 字符";  
	mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-locked:yes;  
	mso-style-link:"标题 2";  
	mso-ansi-font-size:16.0pt;  
	mso-bidi-font-size:16.0pt;  
	font-family:"Times New Roman",serif;  
	mso-ascii-font-family:"Times New Roman";  
	mso-fareast-font-family:"Times New Roman";  
	mso-hansi-font-family:"Times New Roman";  
	mso-bidi-font-family:"Times New Roman";  
	font-weight:bold;}  
span.5  
	{mso-style-name:"标题 5 字符";  
	mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-locked:yes;  
	mso-style-link:"标题 5";  
	mso-ansi-font-size:14.0pt;  
	mso-bidi-font-size:14.0pt;  
	font-family:宋体;  
	mso-ascii-font-family:宋体;  
	mso-fareast-font-family:宋体;  
	mso-hansi-font-family:宋体;  
	mso-bidi-font-family:宋体;  
	font-weight:bold;}  
span.6  
	{mso-style-name:"标题 6 字符";  
	mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-locked:yes;  
	mso-style-link:"标题 6";  
	mso-ansi-font-size:14.0pt;  
	mso-bidi-font-size:14.0pt;  
	font-family:"Times New Roman",serif;  
	mso-ascii-font-family:"Times New Roman";  
	mso-fareast-font-family:"Times New Roman";  
	mso-hansi-font-family:"Times New Roman";  
	mso-bidi-font-family:"Times New Roman";}  
span.7  
	{mso-style-name:"标题 7 字符";  
	mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-locked:yes;  
	mso-style-link:"标题 7";  
	mso-ansi-font-size:13.5pt;  
	mso-bidi-font-size:13.5pt;  
	font-family:宋体;  
	mso-ascii-font-family:宋体;  
	mso-fareast-font-family:宋体;  
	mso-hansi-font-family:宋体;  
	mso-bidi-font-family:宋体;  
	font-weight:bold;}  
span.a  
	{mso-style-name:"正文文本 字符";  
	mso-style-priority:1;  
	mso-style-unhide:no;  
	mso-style-locked:yes;  
	mso-style-link:正文文本;  
	mso-ansi-font-size:12.0pt;  
	mso-bidi-font-size:12.0pt;  
	font-family:"Times New Roman",serif;  
	mso-ascii-font-family:"Times New Roman";  
	mso-fareast-font-family:"Times New Roman";  
	mso-hansi-font-family:"Times New Roman";  
	mso-bidi-font-family:"Times New Roman";}  
.MsoChpDefault  
	{mso-style-type:export-only;  
	mso-default-props:yes;  
	font-size:11.0pt;  
	mso-ansi-font-size:11.0pt;  
	font-family:"Calibri",sans-serif;  
	mso-bidi-font-family:"Times New Roman";  
	mso-bidi-theme-font:minor-bidi;  
	mso-font-kerning:0pt;  
	mso-fareast-language:EN-US;}  
.MsoPapDefault  
	{mso-style-type:export-only;  
	mso-pagination:none;}  
 /\* Page Definitions \*/  
 @page  
	{mso-page-border-surround-header:no;  
	mso-page-border-surround-footer:no;}  
@page WordSection1  
	{size:612.0pt 792.0pt;  
	margin:68.0pt 83.0pt 47.0pt 83.0pt;  
	mso-header-margin:36.0pt;  
	mso-footer-margin:37.05pt;  
	mso-paper-source:0;}  
div.WordSection1  
	{page:WordSection1;}  
@page WordSection2  
	{size:612.0pt 792.0pt;  
	margin:68.0pt 78.0pt 47.0pt 83.0pt;  
	mso-header-margin:36.0pt;  
	mso-footer-margin:37.05pt;  
	mso-paper-source:0;}  
div.WordSection2  
	{page:WordSection2;}  
@page WordSection3  
	{size:612.0pt 792.0pt;  
	margin:68.0pt 83.0pt 47.0pt 83.0pt;  
	mso-header-margin:36.0pt;  
	mso-footer-margin:37.05pt;  
	mso-paper-source:0;}  
div.WordSection3  
	{page:WordSection3;}  
@page WordSection4  
	{size:612.0pt 792.0pt;  
	margin:66.0pt 83.0pt 47.0pt 83.0pt;  
	mso-header-margin:36.0pt;  
	mso-footer-margin:37.05pt;  
	mso-paper-source:0;}  
div.WordSection4  
	{page:WordSection4;}  
@page WordSection5  
	{size:612.0pt 792.0pt;  
	margin:68.0pt 83.0pt 47.0pt 83.0pt;  
	mso-header-margin:36.0pt;  
	mso-footer-margin:37.05pt;  
	mso-paper-source:0;}  
div.WordSection5  
	{page:WordSection5;}  
@page WordSection6  
	{size:612.0pt 792.0pt;  
	margin:68.0pt 83.0pt 47.0pt 83.0pt;  
	mso-header-margin:36.0pt;  
	mso-footer-margin:37.05pt;  
	mso-paper-source:0;}  
div.WordSection6  
	{page:WordSection6;}  
@page WordSection7  
	{size:612.0pt 792.0pt;  
	margin:66.0pt 83.0pt 47.0pt 83.0pt;  
	mso-header-margin:36.0pt;  
	mso-footer-margin:37.05pt;  
	mso-paper-source:0;}  
div.WordSection7  
	{page:WordSection7;}  
@page WordSection8  
	{size:612.0pt 792.0pt;  
	margin:66.0pt 83.0pt 47.0pt 83.0pt;  
	mso-header-margin:36.0pt;  
	mso-footer-margin:37.05pt;  
	mso-paper-source:0;}  
div.WordSection8  
	{page:WordSection8;}  
@page WordSection9  
	{size:612.0pt 792.0pt;  
	margin:66.0pt 83.0pt 47.0pt 83.0pt;  
	mso-header-margin:36.0pt;  
	mso-footer-margin:37.05pt;  
	mso-paper-source:0;}  
div.WordSection9  
	{page:WordSection9;}  
 /\* List Definitions \*/  
 @list l0  
	{mso-list-id:2030788992;  
	mso-list-type:hybrid;  
	mso-list-template-ids:1817765138 1713007924 -392258400 720503646 -1498634472 -1038426690 1418911014 -1800891092 1331199248 726199006;}  
@list l0:level1  
	{mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	margin-left:27.45pt;  
	text-indent:-20.5pt;  
	mso-ansi-font-size:13.5pt;  
	mso-bidi-font-size:13.5pt;  
	font-family:宋体;  
	mso-bidi-font-family:宋体;  
	mso-font-width:99%;  
	mso-ansi-font-weight:bold;  
	mso-bidi-font-weight:bold;}  
@list l0:level2  
	{mso-level-number-format:alpha-lower;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	margin-left:55.0pt;  
	text-align:right;  
	text-indent:-18.0pt;  
	mso-font-width:100%;}  
@list l0:level3  
	{mso-level-start-at:0;  
	mso-level-number-format:bullet;  
	mso-level-text:•;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	margin-left:99.0pt;  
	text-indent:-18.0pt;}  
@list l0:level4  
	{mso-level-start-at:0;  
	mso-level-number-format:bullet;  
	mso-level-text:•;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	margin-left:143.0pt;  
	text-indent:-18.0pt;}  
@list l0:level5  
	{mso-level-start-at:0;  
	mso-level-number-format:bullet;  
	mso-level-text:•;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	margin-left:187.0pt;  
	text-indent:-18.0pt;}  
@list l0:level6  
	{mso-level-start-at:0;  
	mso-level-number-format:bullet;  
	mso-level-text:•;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	margin-left:231.0pt;  
	text-indent:-18.0pt;}  
@list l0:level7  
	{mso-level-start-at:0;  
	mso-level-number-format:bullet;  
	mso-level-text:•;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	margin-left:275.0pt;  
	text-indent:-18.0pt;}  
@list l0:level8  
	{mso-level-start-at:0;  
	mso-level-number-format:bullet;  
	mso-level-text:•;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	margin-left:319.0pt;  
	text-indent:-18.0pt;}  
@list l0:level9  
	{mso-level-start-at:0;  
	mso-level-number-format:bullet;  
	mso-level-text:•;  
	mso-level-tab-stop:none;  
	mso-level-number-position:left;  
	margin-left:363.0pt;  
	text-indent:-18.0pt;}  
ol  
	{margin-bottom:0cm;}  
ul  
	{margin-bottom:0cm;}  
--&gt;  


# 串口调试工具介绍



##### 硬件



###### OrangePi开发板

![](file:///D:/Temp/msohtmlclip1/01/clip_image002.gif)  






![](file:///D:/Temp/msohtmlclip1/01/clip_image004.jpg)  
TTL 转 USB 线

  










## Windows平台



在使用 OrangePi 做项目开发过程中，为了获得更多的调试信息，OrangePi 默认支 持串口信息调试。对于开发者而言，只需准备上面提到的材料，即可简单的获得串 口调试信息。不同的上位机使用的串口调试工具大同小异，基本可以参考下文的方 法进行部署。使用 Windows 平台进行串口调试的工具很多，通常使用的工具是 putty。本节以 putty 作为例子进行部署讲解。



1.Windows 下 USB 驱动安装



![](file:///D:/Temp/msohtmlclip1/01/clip_image006.jpg)  
a.目前最新版的驱动PL2303\_Prolific\_DriverInstaller\_v130.zip，下载解压。



![](file:///D:/Temp/msohtmlclip1/01/clip_image008.jpg)b. 以管理员身份选择应用程序安装















![](file:///D:/Temp/msohtmlclip1/01/clip_image010.jpg)  
c.等待安装完成

2.Windows 下 Putty 安装



a.下载 putty 安装包

  




![](file:///D:/Temp/msohtmlclip1/01/clip_image012.jpg)



b. 解压安装

![](file:///D:/Temp/msohtmlclip1/01/clip_image014.jpg)  




c. 安装好之后打开程序如下图所示

![](file:///D:/Temp/msohtmlclip1/01/clip_image016.jpg)  


3.**调试的连接方式**



![](file:///D:/Temp/msohtmlclip1/01/clip_image018.jpg)  




使用 TTL 转串口线，一端连接 OrangePi，另一端连接 PC

  




![](file:///D:/Temp/msohtmlclip1/01/clip_image019.gif)

4. 设备信息的获取



a. 开始菜单 选择控制面板

![](file:///D:/Temp/msohtmlclip1/01/clip_image021.jpg)  




![](file:///D:/Temp/msohtmlclip1/01/clip_image023.jpg)  




b. 点击设备管理器，查看端口号



![](file:///D:/Temp/msohtmlclip1/01/clip_image025.jpg)  


  








![](file:///D:/Temp/msohtmlclip1/01/clip_image027.jpg)





##### 5.Putty 的配置

![](file:///D:/Temp/msohtmlclip1/01/clip_image029.jpg)  




串行口设置成相应的端口号\(COM5\)，速度设置成 115200



6.开始调试串口



OrangePi上电开机，串口自动打印串口log

  




![](file:///D:/Temp/msohtmlclip1/01/clip_image031.jpg)







## Linux平台





使用Linux平台进行串口调试工具有minicom和kermit。本文以kermit作为例子进行讲解。



**1.Kermit 的安装**

a.使用命令进行安装：



$ sudo apt-get install ckermit



![](file:///D:/Temp/msohtmlclip1/01/clip_image033.jpg)  




b.配置kermit



$ sudo vi /etc/kermit/kermrc



![](file:///D:/Temp/msohtmlclip1/01/clip_image034.jpg)  




c.添加行：



set line /dev/ttyUSB1

set speed115200 set carrier-watch off

set handshake none set flow-control none

  




![](file:///D:/Temp/msohtmlclip1/01/clip_image035.gif)

robust

set file type bin

set file name lit

set rec pack 1000

set send pack 1000

set window 5

c

![](file:///D:/Temp/msohtmlclip1/01/clip_image037.jpg)





**2.调试的连接方式**



![](file:///D:/Temp/msohtmlclip1/01/clip_image039.jpg)  


  




![](file:///D:/Temp/msohtmlclip1/01/clip_image040.gif)

使用 TTL 转串口线，一端连接 OrangePi，另一端连接 PC







3.**设备信息的获取**



$ ls /dev/ \(在 PC 终端输入命令，查询 TTL 转串口 线的设备号\)



![](file:///D:/Temp/msohtmlclip1/01/clip_image042.jpg)  




a.从图中可以看出，“TTL转串口”线被识别为“ttyUSB0”,配置

/ect/kermit/kermitc文件，更新串口信息。



$ sudo vi /etc/kermit/kermitc



b.将setline的值设置为/dev/ttyUSB0

![](file:///D:/Temp/msohtmlclip1/01/clip_image043.jpg)  


  




![](file:///D:/Temp/msohtmlclip1/01/clip_image035.gif)

**4.开始调试串口**

a.在上位机终端输入命令，进入kermit模式：



$ sudo kermit –c



![](file:///D:/Temp/msohtmlclip1/01/clip_image045.jpg)  




b. OrangePi上电开机，串口自动打印串口log。

![](file:///D:/Temp/msohtmlclip1/01/clip_image047.jpg)



