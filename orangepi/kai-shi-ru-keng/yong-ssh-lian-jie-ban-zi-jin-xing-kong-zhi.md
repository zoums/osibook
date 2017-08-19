# 用SSH连接板子进行控制

板子在装完系统后没有显示器，可以用SSH连接板子进行控制。

#### 获得板子IP

板子确保与客户端在同一网络下，如果在同一路由器下可以去路由器DHCP页面查看，或者板子连接显示器和键鼠进行查看，用内网扫描工具进行扫描（NetX或者_Fing_-Network Tools），或者板子设定固定IP等方法，这里演示通过路由器查看的方法。

打开网页浏览器，访问路由器管理页IP，具体是哪个IP看路由器说明书或标签或网上查等进行查看，登陆密码同上方法查询，路由器品种繁多，不能一一演示，不会的可以上网/看说明书查询。

![](/assets/ssh-1.png)

找到DHCP服务页面

![](/assets/ssh-2.png)

查看客户端列表

![](/assets/ssh-3.png)

由于我的PI用了DietPi系统，所以这里的主机名是DietPi，具体修改主机名的方法可以自己判断，如果主机名不知道的，可以在PI连接路由器前查看DHCP的列表，然后再连接上去稍等一下再查看。查不到的可以尝试重启PI和配置PI网络。

#### 连接

获取到IP后使用支持SSH的客户端进行连接，这里我用Putty

![](/assets/ssh-5.png)

配置好IP，如果你喜欢用密钥连接，还可以进行更深入的配置。选择打开进行连接。

![](/assets/ssh-6.png)

第一次连接会提示如下信息，略过即可。

会提示让你输入登录的用户及密码。

![](/assets/ssh-7.png)![](/assets/ssh-8.png)

输入密码时不会显示出来。

登陆成功，可以用ssh对板子进行控制了。

![](/assets/ssh-9.png)

---

有关SSH的更多资料

> SSH 为[Secure Shell](https://baike.baidu.com/item/Secure%20Shell)的缩写，由 IETF 的网络小组（Network Working Group）所制定；SSH 为建立在应用层基础上的安全协议。SSH 是目前较可靠，专为[远程登录](https://baike.baidu.com/item/%E8%BF%9C%E7%A8%8B%E7%99%BB%E5%BD%95)会话和其他网络服务提供安全性的协议。利用 SSH 协议可以有效防止远程管理过程中的信息泄露问题。SSH最初是UNIX系统上的一个程序，后来又迅速扩展到其他操作平台。SSH在正确使用时可弥补网络中的漏洞。SSH客户端适用于多种平台。几乎所有UNIX平台—包括[HP-UX](https://baike.baidu.com/item/HP-UX)、[Linux](https://baike.baidu.com/item/Linux)、[AIX](https://baike.baidu.com/item/AIX)、[Solaris](https://baike.baidu.com/item/Solaris/3517)、[Digital](https://baike.baidu.com/item/Digital) [UNIX](https://baike.baidu.com/item/UNIX)、[Irix](https://baike.baidu.com/item/Irix)，以及其他平台，都可运行SSH。

引用自百度百科 [https://baike.baidu.com/item/ssh/10407?fr=aladdin](https://baike.baidu.com/item/ssh/10407?fr=aladdin)  


