# 【唐老狮】Unity网络开发基础

2023年7月，盘子ssa，QQ：2426966358

# 任务21-1：IP地址和端口类 知识点

## 知识点一 IP类和端口类用来干什么？

通过之前的理论知识学习，我们知道想要进行网络通信，进行网络连接。

首先我们需要找到对应设备，IP和端口号是定位网络中设备必不可少的关键元素。

C#中提供了对应的IP和端口相关的类，来声明对应信息，对于之后的网络通信是必不可少的内容。

## 知识点二 IPAddress类

命名空间：System.Net;
类名：IPAddress

初始化IP信息的方式

1. 用byte数组进行初始化

   ```C#
   byte[] ipAddress = new byte[] { 118, 102, 111, 11 };
   IPAddress ip1 = new IPAddress(ipAddress);
   ```

2. 用long长整型进行初始化

   ```c#
    IPAddress ip2 = new IPAddress(0x79666F0B);
   ```

3. 推荐使用的方式 使用字符串转换

   ```C#
   IPAddress ip3 = IPAddress.Parse("118.102.111.11");
   ```

### 特殊IP地址

`127.0.0.1`代表本机地址

### 一些静态成员

获取可用的IPv6地址：`IPAddress.IPv6Any`

## 知识点三 IPEndPoint类

命名空间：`System.Net;`

类名：`IPEndPoint`

`IPEndPoint`类将网络端点表示为IP地址和端口号，表现为IP地址和端口号的组合

初始化方式

```C#
IPEndPoint ipPoint = new IPEndPoint(0x79666F0B, 8080);
IPEndPoint ipPoint2 = new IPEndPoint(IPAddress.Parse("118.102.111.11"), 8080);
```

## 总结

程序表示IP信息

```C#
IPAddress ip = IPAddress.Parse("IPv4地址");
```

程序表示通信目标

```C#
IPEndPoint point = new IPEndPoint(ip, 8080);
```

# 任务23-1：域名解析 知识点

## 知识点一 什么是域名解析？

域名解析也叫域名指向、服务器设置、域名配置以及反向IP登记等等。

说得简单点就是将好记的域名解析成IP
IP地址是网络上标识站点的数字地址，但是IP地址相对来说记忆困难
所以为了方便记忆，采用域名来代替IP地址标识站点地址。
比如 我们要登录一个网页 www.baidu.com 这个就是域名 我们可以通过记忆域名来记忆一个远端服务器的地址，而不是记录一个复杂的IP地址

域名解析就是域名到IP地址的转换过程。域名的解析工作由DNS服务器完成
我们在进行通信时有时会有需求通过域名获取IP
所以这节课我们就来学习C#提供的域名解析相关的类

域名系统（英文：Domain Name System，缩写：DNS）是互联网的一项服务
它作为将域名和IP地址相互映射的一个分布式数据库，能够使人更方便地访问互联网
是因特网上解决网上机器命名的一种系统，因为IP地址记忆不方便，就采用了域名系统来管理名字和IP的对应关系

## 知识点二 IPHostEntry类

命名空间：System.Net
类名：IPHostEntry
主要作用：域名解析后的返回值 可以通过该对象获取IP地址、主机名等等信息
该类不会自己声明，都是作为某些方法的返回值返回信息，我们主要通过该类对象获取返回的信息

- 获取关联IP       成员变量:`AddressList`
- 获取主机别名列表  成员变量:`Aliases`
- 获取DNS名称      成员变量:`HostName`

## 知识点三 Dns类

命名空间：System.Net
类名：Dns
主要作用：Dns是一个静态类，提供了很多静态方法，可以使用它来根据域名获取IP地址

常用方法

1. 获取本地系统的主机名

   ```C#
   print(Dns.GetHostName());
   ```

2. 获取指定域名的IP信息

   根据域名获取
   同步获取
   注意：由于获取远程主机信息是需要进行网路通信，所以可能会阻塞主线程

   ```C#
   IPHostEntry entry = Dns.GetHostEntry("www.baidu.com");
   for (int i = 0; i < entry.AddressList.Length; i++)
   {
       print("IP地址：" + entry.AddressList[i]);
   }
   for (int i = 0; i < entry.Aliases.Length; i++)
   {
       print("主机别名" + entry.Aliases[i]);
   }
   print("DNS服务器名称" + entry.HostName);
   ```

   异步获取

   ```C#
   GetHostEntry();
   ```

## 总结

如果你不知道对方的IP地址，想通过域名和对方进行通信。

我们可以通过Dns类通过域名得到IP地址后再和对方建立连接并通信。

