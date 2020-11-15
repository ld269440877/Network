# Networkstart

# 网络-UDP

## 网络通信概述

### 1. 什么是网络

- 网络就是一种辅助双方或者多方能够连接在一起的工具
- 如果没有网络可想`单机`的世界是多么的孤单

### 2. 使用网络的目的

就是为了联通多方然后进行通信用的，即把数据从一方传递给另外一方

前面的学习编写的程序都是单机的，即不能和其他电脑上的程序进行通信

为了让在不同的电脑上运行的软件，之间能够互相传递数据，就需要借助网络的功能

#### 小总结

- 使用网络能够把多方链接在一起，然后可以进行数据传递
- 所谓的网络编程就是，让在不同的电脑上的软件能够进行数据传递，即进程之间的通信

![image-20201115182401182](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115182458.png)

## ip地址

### 1. 什么是地址

地址就是用来标记地点的

![image-20201115182453274](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115182453.png)

### 2. ip地址的作用

![image-20201115182518893](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115182519.png)

#### ip地址：用来在网络中标记一台电脑，比如192.168.1.1；在本地局域网上是唯一的。

### 3. ip地址的分类（了解）

每一个IP地址包括两部分：网络地址和主机地址

![image-20201115182546450](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115182546.png)3.1 A类IP地址

一个A类IP地址由1字节的网络地址和3字节主机地址组成，网络地址的最高位必须是“0”，

地址范围1.0.0.1-126.255.255.254

二进制表示为：00000001 00000000 00000000 00000001 - 01111110 11111111 11111111 11111110

可用的A类网络有126个，每个网络能容纳1677214个主机

#### 3.2 B类IP地址

一个B类IP地址由2个字节的网络地址和2个字节的主机地址组成，网络地址的最高位必须是“10”，

地址范围128.1.0.1-191.255.255.254

二进制表示为：10000000 00000001 00000000 00000001 - 10111111 11111111 11111111 11111110

可用的B类网络有16384个，每个网络能容纳65534主机

#### 3.3 C类IP地址

一个C类IP地址由3字节的网络地址和1字节的主机地址组成，网络地址的最高位必须是“110”

范围192.0.1.1-223.255.255.254

二进制表示为: 11000000 00000000 00000001 00000001 - 11011111 11111111 11111110 11111110

C类网络可达2097152个，每个网络能容纳254个主机

#### 3.4 D类地址用于多点广播

D类IP地址第一个字节以“1110”开始，它是一个专门保留的地址。

它并不指向特定的网络，目前这一类地址被用在多点广播（Multicast）中

多点广播地址用来一次寻址一组计算机 s 地址范围224.0.0.1-239.255.255.254

#### 3.5 E类IP地址

以“1111”开始，为将来使用保留

E类地址保留，仅作实验和开发用

#### 3.6 私有ip

在这么多网络IP中，国际规定有一部分IP地址是用于我们的局域网使用，也就

是属于私网IP，不在公网中使用的，它们的范围是：

```
10.0.0.0～10.255.255.255

172.16.0.0～172.31.255.255

192.168.0.0～192.168.255.255
```

#### 3.7 注意

IP地址127．0．0．1~127．255．255．255用于回路测试，

如：127.0.0.1可以代表本机IP地址，用`http://127.0.0.1`就可以测试本机中配置的Web服务器。

## Linux命令(ping, ifconfig)

### 查看或配置网卡信息：ifconfig

如果，我们只是敲：ifconfig，它会显示所有网卡的信息：

![image-20201115182641030](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115182641.png)

![image-20201115182657050](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115182657.png)

### 测试远程主机连通性：ping

通常用ping来检测网络是否正常

![image-20201115182716821](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115182716821.png)

## 端口

### 1. 什么是端口

![image-20201115182741302](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115182741302.png)

端口就好一个房子的门，是出入这间房子的必经之路。

![image-20201115182759397](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115182759397.png)

如果一个程序需要收发网络数据，那么就需要有这样的端口

在linux系统中，端口可以有65536（2的16次方）个之多！

既然有这么多，操作系统为了统一管理，所以进行了编号，这就是`端口号`

### 2. 端口号

端口是通过端口号来标记的，端口号只有整数，范围是从0到65535

注意：端口数不一样的*nix系统不一样，还可以手动修改

### 3. 端口是怎样分配的

端口号不是随意使用的，而是按照一定的规定进行分配。

端口的分类标准有好几种，我们这里不做详细讲解，只介绍一下知名端口和动态端口

#### 3.1 知名端口（Well Known Ports）

知名端口是众所周知的端口号，范围从0到1023

```
80端口分配给HTTP服务
21端口分配给FTP服务
```

可以理解为，一些常用的功能使用的号码是估计的，好比 电话号码110、10086、10010一样

![image-20201115182833289](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115182833289.png)

一般情况下，如果一个程序需要使用知名端口的需要有root权限

#### 3.2 动态端口（Dynamic Ports）

动态端口的范围是从1024到65535

之所以称为动态端口，是因为它一般不固定分配某种服务，而是动态分配。

动态分配是指当一个系统程序或应用程序程序需要网络通信时，它向主机申请一个端口，主机从可用的端口号中分配一个供它使用。

当这个程序关闭时，同时也就释放了所占用的端口号

#### 3.3 怎样查看端口 ？

- 用“netstat －an”查看端口状态
- lsof -i [tcp/udp]:2425

### 4. 小总结

端口有什么用呢 ？ 我们知道，一台拥有IP地址的主机可以提供许多服务，比如HTTP（万维网服务）、FTP（文件传输）、SMTP（电子邮件）等，这些服务完全可以通过1个IP地址来实现。那么，主机是怎样区分不同的网络服务呢？显然不能只靠IP地址，因为IP地址与网络服务的关系是一对多的关系。实际上是通过“IP地址+端口号”来区分不同的服务的。 需要注意的是，端口并不是一一对应的。比如你的电脑作为客户机访问一台WWW服务器时，WWW服务器使用“80”端口与你的电脑通信，但你的电脑则可能使用“3457”这样的端口。

## socket简介

### 1. 不同电脑上的进程之间如何通信

首要解决的问题是如何唯一标识一个进程，否则通信无从谈起！

在1台电脑上可以通过进程号（PID）来唯一标识一个进程，但是在网络中这是行不通的。

其实TCP/IP协议族已经帮我们解决了这个问题，网络层的“ip地址”可以唯一标识网络中的主机，而传输层的“协议+端口”可以唯一标识主机中的应用进程（进程）。

这样利用<font color=red>ip地址，协议，端口</font>就可以标识网络的进程了，网络中的进程通信就可以利用这个标志与其它进程进行交互

##### 注意：

> - 所谓`进程`指的是：运行的程序以及运行时用到的资源这个整体称之为进程（在讲解多任务编程时进行详细讲解）
> - 所谓`进程间通信`指的是：运行的程序之间的数据共享
> - 后面课程中会详细说到，像网络层等知识，不要着急

### 2. 什么是socket

socket(简称 `套接字`) 是进程间通信的一种方式，它与其他进程间通信的一个主要不同是：

它能实现不同主机间的进程间通信，我们网络上各种各样的服务大多都是基于 Socket 来完成通信的

例如我们每天浏览网页、QQ 聊天、收发 email 等等

### 3. 创建socket

在 Python 中 使用socket 模块的函数 socket 就可以完成：

```python
import socket
socket.socket(AddressFamily, Type)
```

#### 说明：

函数 socket.socket 创建一个 socket，该函数带有两个参数：

- Address Family：可以选择 AF_INET（用于 Internet 进程间通信） 或者 AF_UNIX（用于同一台机器进程间通信）,实际工作中常用AF_INET
- Type：套接字类型，可以是 SOCK_STREAM（流式套接字，主要用于 TCP 协议）或者 SOCK_DGRAM（数据报套接字，主要用于 UDP 协议）

创建一个tcp socket（tcp套接字）

```python
import socket

# 创建tcp的套接字
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# ...这里是使用套接字的功能（省略）...

# 不用的时候，关闭套接字
s.close()
```

创建一个udp socket（udp套接字）

```python
import socket

# 创建udp的套接字
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# ...这里是使用套接字的功能（省略）...

# 不用的时候，关闭套接字
s.close()
```

##### 说明

- 套接字使用流程 与 文件的使用流程很类似
  1. 创建套接字
  2. 使用套接字收/发数据
  3. 关闭套接字

## udp网络程序-发送、接收数据

### 1. udp网络程序-发送数据

创建一个基于udp的网络程序流程很简单，具体步骤如下：

1. 创建客户端套接字
2. 发送/接收数据
3. 关闭套接字

![image-20201115183045810](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115183045.png)

```python
#coding=utf-8

from socket import *

# 1. 创建udp套接字
udp_socket = socket(AF_INET, SOCK_DGRAM)

# 2. 准备接收方的地址
# '192.168.1.103'表示目的ip地址
# 8080表示目的端口
dest_addr = ('192.168.1.103', 8080)  # 注意 是元组，ip是字符串，端口是数字

# 3. 从键盘获取数据
send_data = input("请输入要发送的数据:")

# 4. 发送数据到指定的电脑上的指定程序中
udp_socket.sendto(send_data.encode('utf-8'), dest_addr)

# 5. 关闭套接字
udp_socket.close()
```

![image-20201115183231293](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115183231293.png)

![image-20201115183243941](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115183243941.png)

### 2. udp网络程序-发送、接收数据

```python
#coding=utf-8

from socket import *

# 1. 创建udp套接字
udp_socket = socket(AF_INET, SOCK_DGRAM)

# 2. 准备接收方的地址
dest_addr = ('192.168.236.129', 8080)

# 3. 从键盘获取数据
send_data = input("请输入要发送的数据:")

# 4. 发送数据到指定的电脑上
udp_socket.sendto(send_data.encode('utf-8'), dest_addr)

# 5. 等待接收对方发送的数据
recv_data = udp_socket.recvfrom(1024)  # 1024表示本次接收的最大字节数

# 6. 显示对方发送的数据
# 接收到的数据recv_data是一个元组
# 第1个元素是对方发送的数据
# 第2个元素是对方的ip和端口
print(recv_data[0].decode('gbk'))
print(recv_data[1])

# 7. 关闭套接字
udp_socket.close()
```

![image-20201115183309966](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115183310.png)

![image-20201115183321466](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115183321466.png)

## python3编码转换

```python
str->bytes:encode编码
bytes->str:decode解码
```

字符串通过编码成为字节码，字节码通过解码成为字符串。

```python
>>> text = '我是文本'
>>> text
'我是文本'
>>> print(text)
我是文本
>>> bytesText = text.encode()
>>> bytesText
b'\xe6\x88\x91\xe6\x98\xaf\xe6\x96\x87\xe6\x9c\xac'
>>> print(bytesText)
b'\xe6\x88\x91\xe6\x98\xaf\xe6\x96\x87\xe6\x9c\xac'
>>> type(text)
<class 'str'>
>>> type(bytesText)
<class 'bytes'>
>>> textDecode = bytesText.decode()
>>> textDecode
'我是文本'
>>> print(textDecode)
我是文本
```

其中decode()与encode()方法可以接受参数，其声明分别为:

```python
bytes.decode(encoding="utf-8", errors="strict")
str.encode(encoding="utf-8", errors="strict")
```

其中的encoding是指在解码编码过程中使用的编码(此处指“编码方案”是名词)，errors是指错误的处理方案。

详细的可以参照官方文档：

- [str.encode()](https://docs.python.org/3/library/stdtypes.html?highlight=decode#str.encode)
- [bytes.decode()](https://docs.python.org/3/library/stdtypes.html?highlight=decode#bytes.decode)

## udp绑定信息

### 1. udp网络程序-端口问题

- 会变的端口号

重新运行多次脚本，然后在“网络调试助手”中，看到的现象如下：

![image-20201115183421149](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115183421.png)

说明：

- 每重新运行一次网络程序，上图中红圈中的数字，不一样的原因在于，这个数字标识这个网络程序，当重新运行时，如果没有确定到底用哪个，系统默认会随机分配
- 记住一点：这个网络程序在运行的过程中，这个就唯一标识这个程序，所以如果其他电脑上的网络程序如果想要向此程序发送数据，那么就需要向这个数字（即端口）标识的程序发送即可

### 2. udp绑定信息

#### <1>. 绑定信息

一般情况下，在一台电脑上运行的网络程序有很多，为了不与其他的网络程序占用同一个端口号，往往在编程中，udp的端口号一般不绑定

但是如果需要做成一个服务器端的程序的话，是需要绑定的，想想看这又是为什么呢？

如果报警电话每天都在变，想必世界就会乱了，所以一般服务性的程序，往往需要一个固定的端口号，这就是所谓的端口绑定

![image-20201115183444764](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115183444.png)

#### <2>. 绑定示例

```python
#coding=utf-8

from socket import *

# 1. 创建套接字
udp_socket = socket(AF_INET, SOCK_DGRAM)

# 2. 绑定本地的相关信息，如果一个网络程序不绑定，则系统会随机分配
local_addr = ('', 7788) #  ip地址和端口号，ip一般不用写，表示本机的任何一个ip
udp_socket.bind(local_addr)

# 3. 等待接收对方发送的数据
recv_data = udp_socket.recvfrom(1024) #  1024表示本次接收的最大字节数

# 4. 显示接收到的数据
print(recv_data[0].decode('gbk'))

# 5. 关闭套接字
udp_socket.close()
```

![image-20201115183506123](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115183506.png)

#### <3>. 总结

- 一个udp网络程序，可以不绑定，此时操作系统会随机进行分配一个端口，如果重新运行此程序端口可能会发生变化
- 一个udp网络程序，也可以绑定信息（ip地址，端口号），如果绑定成功，那么操作系统用这个端口号来进行区别收到的网络数据是否是此进程的

## 网络通信过程(简单版)

![image-20201115183531738](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115183531.png)

### 说明

- 网络通信过程中，之所需要ip、port等，就是为了能够将一个复杂的通信过程进行任务划分，从而保证数据准确无误的传递

## 应用：udp聊天器

#### 说明

> - 在一个电脑中编写1个程序，有2个功能
> - 1.获取键盘数据，并将其发送给对方
> - 2.接收数据并显示
> - 并且功能数据进行选择以上的2个功能调用

#### 要求

> 1. 实现上述程序

#### 参考代码

```python
import socket


def send_msg(udp_socket):
    """获取键盘数据，并将其发送给对方"""
    # 1. 从键盘输入数据
    msg = input("\n请输入要发送的数据:")
    # 2. 输入对方的ip地址
    dest_ip = input("\n请输入对方的ip地址:")
    # 3. 输入对方的port
    dest_port = int(input("\n请输入对方的port:"))
    # 4. 发送数据
    udp_socket.sendto(msg.encode("utf-8"), (dest_ip, dest_port))


def recv_msg(udp_socket):
    """接收数据并显示"""
    # 1. 接收数据
    recv_msg = udp_socket.recvfrom(1024)
    # 2. 解码
    recv_ip = recv_msg[1]
    recv_msg = recv_msg[0].decode("utf-8")
    # 3. 显示接收到的数据
    print(">>>%s:%s" % (str(recv_ip), recv_msg))


def main():
    # 1. 创建套接字
    udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    # 2. 绑定本地信息
    udp_socket.bind(("", 7890))
    while True:
        # 3. 选择功能
        print("="*30)
        print("1:发送消息")
        print("2:接收消息")
        print("="*30)
        op_num = input("请输入要操作的功能序号:")

        # 4. 根据选择调用相应的函数
        if op_num == "1":
            send_msg(udp_socket)
        elif op_num == "2":
            recv_msg(udp_socket)
        else:
            print("输入有误，请重新输入...")

if __name__ == "__main__":
    main()
```

#### 想一想

- 以上的程序如果选择了接收数据功能，并且此时没有数据，程序会堵塞在这，那么怎样才能让这个程序收发数据一起进行呢？别着急，学习完多任务知识之后就解决了O(∩_∩)O...

# 网络-TCP

## TCP简介

### TCP介绍

**TCP协议，传输控制协议（英语：Transmission Control Protocol，缩写为 TCP）**是一种面向连接的、可靠的、基于字节流的传输层通信协议，由IETF的RFC 793定义。

TCP通信需要经过**创建连接、数据传送、终止连接**三个步骤。

TCP通信模型中，在通信开始之前，一定要先建立相关的链接，才能发送数据，类似于生活中，"打电话""

### TCP特点

#### 1. 面向连接

通信双方必须先建立连接才能进行数据的传输，双方都必须为该连接分配必要的系统内核资源，以管理连接的状态和连接上的传输。

双方间的数据传输都可以通过这一个连接进行。

完成数据交换后，双方必须断开此连接，以释放系统资源。

这种连接是一对一的，因此TCP不适用于广播的应用程序，基于广播的应用程序请使用UDP协议。

#### 2. 可靠传输

1）**TCP采用发送应答机制**

TCP发送的每个报文段都必须得到接收方的应答才认为这个TCP报文段传输成功

2）**超时重传**

发送端发出一个报文段之后就启动定时器，如果在定时时间内没有收到应答就重新发送这个报文段。

TCP为了保证不发生丢包，就给每个包一个序号，同时序号也保证了传送到接收端实体的包的按序接收。然后接收端实体对已成功收到的包发回一个相应的确认（ACK）；如果发送端实体在合理的往返时延（RTT）内未收到确认，那么对应的数据包就被假设为已丢失将会被进行重传。

3）**错误校验**

TCP用一个校验和函数来检验数据是否有错误；在发送和接收时都要计算校验和。

4) **流量控制和阻塞管理**

流量控制用来避免主机发送得过快而使接收方来不及完全收下。

### TCP与UDP的不同点

- 面向连接（确认有创建三方交握，连接已创建才作传输。）
- 有序数据传输
- 重发丢失的数据包
- 舍弃重复的数据包
- 无差错的数据传输
- 阻塞/流量控制

## udp通信模型

udp通信模型中，在通信开始之前，不需要建立相关的链接，只需要发送数据即可，类似于生活中，"写信""

![image-20201115183703172](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115183703172.png)

![image-20201115183717643](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115183717643.png)

## TCP通信模型

udp通信模型中，在通信开始之前，一定要先建立相关的链接，才能发送数据，类似于生活中，"打电话""

![image-20201115183740914](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115183741.png)

## tcp客户端

tcp客户端，并不是像之前一个段子：一个顾客去饭馆吃饭，这个顾客要点菜，就问服务员咱们饭店有客户端么，然后这个服务员非常客气的说道：先生 我们饭店不用客户端，我们直接送到您的餐桌上

如果，不学习网络的知识是不是 说不定也会发生那样的笑话 ，哈哈

所谓的服务器端：就是提供服务的一方，而客户端，就是需要被服务的一方

### tcp客户端构建流程

tcp的客户端要比服务器端简单很多，如果说服务器端是需要自己买手机、查手机卡、设置铃声、等待别人打电话流程的话，那么客户端就只需要找一个电话亭，拿起电话拨打即可，流程要少很多

示例代码：

```python
from socket import *

# 创建socket
tcp_client_socket = socket(AF_INET, SOCK_STREAM)

# 目的信息
server_ip = input("请输入服务器ip:")
server_port = int(input("请输入服务器port:"))

# 链接服务器
tcp_client_socket.connect((server_ip, server_port))

# 提示用户输入数据
send_data = input("请输入要发送的数据：")

tcp_client_socket.send(send_data.encode("gbk"))

# 接收对方发送过来的数据，最大接收1024个字节
recvData = tcp_client_socket.recv(1024)
print('接收到的数据为:', recvData.decode('gbk'))

# 关闭套接字
tcp_client_socket.close()
```

### 运行流程：

#### <1>tcp客户端

```python
请输入服务器ip:10.10.0.47
请输入服务器port:8080
请输入要发送的数据：你好啊
接收到的数据为: 我很好，你呢
```

#### <2>网络调试助手：

![image-20201115183805466](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115183805.png)

## tcp服务器

### 生活中的电话机

如果想让别人能更够打通咱们的电话获取相应服务的话，需要做以下几件事情：

1. 买个手机
2. 插上手机卡
3. 设计手机为正常接听状态（即能够响铃）
4. 静静的等着别人拨打

### tcp服务器

如同上面的电话机过程一样，在程序中，如果想要完成一个tcp服务器的功能，需要的流程如下：

1. socket创建一个套接字
2. bind绑定ip和port
3. listen使套接字变为可以被动链接
4. accept等待客户端的链接
5. recv/send接收发送数据

一个很简单的tcp服务器如下：

```python
from socket import *

# 创建socket
tcp_server_socket = socket(AF_INET, SOCK_STREAM)

# 本地信息
address = ('', 7788)

# 绑定
tcp_server_socket.bind(address)

# 使用socket创建的套接字默认的属性是主动的，使用listen将其变为被动的，这样就可以接收别人的链接了
tcp_server_socket.listen(128)

# 如果有新的客户端来链接服务器，那么就产生一个新的套接字专门为这个客户端服务
# client_socket用来为这个客户端服务
# tcp_server_socket就可以省下来专门等待其他新客户端的链接
client_socket, clientAddr = tcp_server_socket.accept()

# 接收对方发送过来的数据
recv_data = client_socket.recv(1024)  # 接收1024个字节
print('接收到的数据为:', recv_data.decode('gbk'))

# 发送一些数据到客户端
client_socket.send("thank you !".encode('gbk'))

# 关闭为这个客户端服务的套接字，只要关闭了，就意味着为不能再为这个客户端服务了，如果还需要服务，只能再次重新连接
client_socket.close()
```

### 运行流程：

#### <1>tcp服务器

```python
接收到的数据为: 你在么？
```

#### <2>网络调试助手：

![image-20201115183835271](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115183835.png)

## tcp注意点

1. tcp服务器一般情况下都需要绑定，否则客户端找不到这个服务器
2. tcp客户端一般不绑定，因为是主动链接服务器，所以只要确定好服务器的ip、port等信息就好，本地客户端可以随机
3. tcp服务器中通过listen可以将socket创建出来的主动套接字变为被动的，这是做tcp服务器时必须要做的
4. 当客户端需要链接服务器时，就需要使用connect进行链接，udp是不需要链接的而是直接发送，但是tcp必须先链接，只有链接成功才能通信
5. 当一个tcp客户端连接服务器时，服务器端会有1个新的套接字，这个套接字用来标记这个客户端，单独为这个客户端服务
6. listen后的套接字是被动套接字，用来接收新的客户端的链接请求的，而accept返回的新套接字是标记这个新客户端的
7. 关闭listen后的套接字意味着被动套接字关闭了，会导致新的客户端不能够链接服务器，但是之前已经链接成功的客户端正常通信。
8. 关闭accept返回的套接字意味着这个客户端已经服务完毕
9. 当客户端的套接字调用close后，服务器端会recv解堵塞，并且返回的长度为0，因此服务器可以通过返回数据的长度来区别客户端是否已经下线

## 案例:文件下载器

#### 服务器 参考代码如下:

```python
from socket import *
import sys


def get_file_content(file_name):
    """获取文件的内容"""
    try:
        with open(file_name, "rb") as f:
            content = f.read()
        return content
    except:
        print("没有下载的文件:%s" % file_name)


def main():

    if len(sys.argv) != 2:
        print("请按照如下方式运行：python3 xxx.py 7890")
        return
    else:
        # 运行方式为python3 xxx.py 7890
        port = int(sys.argv[1])


    # 创建socket
    tcp_server_socket = socket(AF_INET, SOCK_STREAM)
    # 本地信息
    address = ('', port)
    # 绑定本地信息
    tcp_server_socket.bind(address)
    # 将主动套接字变为被动套接字
    tcp_server_socket.listen(128)

    while True:
        # 等待客户端的链接，即为这个客户端发送文件
        client_socket, clientAddr = tcp_server_socket.accept()
        # 接收对方发送过来的数据
        recv_data = client_socket.recv(1024)  # 接收1024个字节
        file_name = recv_data.decode("utf-8")
        print("对方请求下载的文件名为:%s" % file_name)
        file_content = get_file_content(file_name)
        # 发送文件的数据给客户端
        # 因为获取打开文件时是以rb方式打开，所以file_content中的数据已经是二进制的格式，因此不需要encode编码
        if file_content:
            client_socket.send(file_content)
        # 关闭这个套接字
        client_socket.close()

    # 关闭监听套接字
    tcp_server_socket.close()


if __name__ == "__main__":
    main()
```

#### 客户端 参考代码如下:

```python
from socket import *


def main():

    # 创建socket
    tcp_client_socket = socket(AF_INET, SOCK_STREAM)

    # 目的信息
    server_ip = input("请输入服务器ip:")
    server_port = int(input("请输入服务器port:"))

    # 链接服务器
    tcp_client_socket.connect((server_ip, server_port))

    # 输入需要下载的文件名
    file_name = input("请输入要下载的文件名：")

    # 发送文件下载请求
    tcp_client_socket.send(file_name.encode("utf-8"))

    # 接收对方发送过来的数据，最大接收1024个字节（1K）
    recv_data = tcp_client_socket.recv(1024)
    # print('接收到的数据为:', recv_data.decode('utf-8'))
    # 如果接收到数据再创建文件，否则不创建
    if recv_data:
        with open("[接收]"+file_name, "wb") as f:
            f.write(recv_data)

    # 关闭套接字
    tcp_client_socket.close()


if __name__ == "__main__":
    main()
```

## tcp的3次握手

![image-20201115183918091](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115183918091.png)

## tcp的4次挥手

![image-20201115183945812](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115183946.png)

## tcp长连接和短连接

TCP在真正的读写操作之前，server与client之间必须建立一个连接，

当读写操作完成后，双方不再需要这个连接时它们可以释放这个连接，

连接的建立通过三次握手，释放则需要四次握手，

所以说每个连接的建立都是需要资源消耗和时间消耗的。

### TCP通信的整个过程，如下图:

![image-20201115184007510](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184007.png)

## 1. TCP短连接

模拟一种TCP短连接的情况:

1. client 向 server 发起连接请求
2. server 接到请求，双方建立连接
3. client 向 server 发送消息
4. server 回应 client
5. 一次读写完成，此时双方任何一个都可以发起 close 操作

在步骤5中，一般都是 client 先发起 close 操作。当然也不排除有特殊的情况。

从上面的描述看，短连接一般只会在 client/server 间传递一次读写操作！

## 2. TCP长连接

再模拟一种长连接的情况:

1. client 向 server 发起连接
2. server 接到请求，双方建立连接
3. client 向 server 发送消息
4. server 回应 client
5. 一次读写完成，连接不关闭
6. 后续读写操作...
7. 长时间操作之后client发起关闭请求

## 3. TCP长/短连接操作过程

### 3.1 短连接的操作步骤是：

建立连接——数据传输——关闭连接...建立连接——数据传输——关闭连接

![image-20201115184026563](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184026.png)

### 3.2 长连接的操作步骤是：

建立连接——数据传输...（保持连接）...数据传输——关闭连接

![image-20201115184042383](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184042.png)

## 4. TCP长/短连接的优点和缺点

- 长连接可以省去较多的TCP建立和关闭的操作，减少浪费，节约时间。

  对于频繁请求资源的客户来说，较适用长连接。

- client与server之间的连接如果一直不关闭的话，会存在一个问题，

  随着客户端连接越来越多，server早晚有扛不住的时候，这时候server端需要采取一些策略，

  如关闭一些长时间没有读写事件发生的连接，这样可以避免一些恶意连接导致server端服务受损；

  如果条件再允许就可以以客户端机器为颗粒度，限制每个客户端的最大长连接数，

  这样可以完全避免某个蛋疼的客户端连累后端服务。

- 短连接对于服务器来说管理较为简单，存在的连接都是有用的连接，不需要额外的控制手段。

- 但如果客户请求频繁，将在TCP的建立和关闭操作上浪费时间和带宽。

## 5. TCP长/短连接的应用场景

- 长连接多用于操作频繁，点对点的通讯，而且连接数不能太多情况。

  每个TCP连接都需要三次握手，这需要时间，如果每个操作都是先连接，

  再操作的话那么处理速度会降低很多，所以每个操作完后都不断开，

  再次处理时直接发送数据包就OK了，不用建立TCP连接。

  例如：数据库的连接用长连接，如果用短连接频繁的通信会造成socket错误，

  而且频繁的socket 创建也是对资源的浪费。

- 而像WEB网站的http服务一般都用短链接，因为长连接对于服务端来说会耗费一定的资源，

  而像WEB网站这么频繁的成千上万甚至上亿客户端的连接用短连接会更省一些资源，

  如果用长连接，而且同时有成千上万的用户，如果每个用户都占用一个连接的话，

  那可想而知吧。所以并发量大，但每个用户无需频繁操作情况下需用短连好。

# wireshark抓包工具使用

## 1. 安装wireshark

![image-20201115184115817](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184115817.png)

![image-20201115184131376](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184131376.png)

![image-20201115184143134](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184143134.png)

![image-20201115184153581](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184153581.png)

![image-20201115184202696](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184202.png)

![image-20201115184212932](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184213.png)

## 2. wireshark的使用

![image-20201115184228253](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184228.png)

![image-20201115184238084](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184238.png)

![image-20201115184247017](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184247.png)

![image-20201115184257845](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184258.png)

![image-20201115184311048](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184311.png)

![image-20201115184319700](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184319.png)

![image-20201115184327969](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184328.png)

![image-20201115184337479](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184337.png)

![image-20201115184346147](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184346.png)

![image-20201115184354821](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184354821.png)

## tcp-ip简介

作为新时代标杆的我们，已经离不开手机、离不开网络，对于互联网大家可能耳熟能详，但是计算机网络的出现比互联网要早很多

## 1. 什么是协议

![image-20201115184413710](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184413710.png)

有的说英语，有的说中文，有的说德语，说同一种语言的人可以交流，不同的语言之间就不行了

为了解决不同种族人之间的语言沟通障碍，现规定国际通用语言是英语，这就是一个规定，这就是协议

## 2. 计算机网络沟通用什么

现在的生活中，不同的计算机只需要能够联网（有线无线都可以）那么就可以相互进行传递数据

![image-20201115184445478](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184445478.png)

那么不同种类之间的计算机到底是怎么进行数据传递的呢？

就像说不同语言的人沟通一样，只要有一种大家都认可都遵守的协议即可，那么这个计算机都遵守的网络通信协议叫做`TCP/IP协议`

## 3. TCP/IP协议(族)

早期的计算机网络，都是由各厂商自己规定一套协议，IBM、Apple和Microsoft都有各自的网络协议，互不兼容

为了把全世界的所有不同类型的计算机都连接起来，就必须规定一套全球通用的协议，为了实现互联网这个目标，互联网协议族（Internet Protocol Suite）就是通用协议标准。

因为互联网协议包含了上百种协议标准，但是最重要的两个协议是TCP和IP协议，所以，大家把互联网的协议简称TCP/IP协议(族)

常用的网络协议如下图所示：

![image-20201115184549656](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184549656.png)

![image-20201115184605363](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184605363.png)

说明：

```
网际层也称为：网络层
网络接口层也称为：链路层
```

#### 另外一套标准

![image-20201115184622851](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184622851.png)

# http协议、web服务器-并发服务器-1

## 1. 使用谷歌/火狐浏览器分析

在Web应用中，服务器把网页传给浏览器，实际上就是把网页的HTML代码发送给浏览器，让浏览器显示出来。而浏览器和服务器之间的传输协议是HTTP，所以：

- HTML是一种用来定义网页的文本，会HTML，就可以编写网页；
- HTTP是在网络上传输HTML的协议，用于浏览器和服务器的通信。

Chrome浏览器提供了一套完整地调试工具，非常适合Web开发。

安装好Chrome浏览器后，打开Chrome，在菜单中选择“视图”，“开发者”，“开发者工具”，就可以显示开发者工具：

![image-20201115184809527](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184809.png)

#### 说明

- Elements显示网页的结构
- Network显示浏览器和服务器的通信

我们点Network，确保第一个小红灯亮着，Chrome就会记录所有浏览器和服务器之间的通信：

![image-20201115184829417](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115184829.png)

## 2. http协议的分析

当我们在地址栏输入www.sina.com时，浏览器将显示新浪的首页。在这个过程中，浏览器都干了哪些事情呢？通过Network的记录，我们就可以知道。在Network中，找到www.sina.com那条记录，点击，右侧将显示Request Headers，点击右侧的view source，我们就可以看到浏览器发给新浪服务器的请求：

### 2.1 浏览器请求

![image-20201115184855016](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184855016.png)

![image-20201115184904582](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184904582.png)

#### 说明

最主要的头两行分析如下，第一行：

```
    GET / HTTP/1.1
```

GET表示一个读取请求，将从服务器获得网页数据，/表示URL的路径，URL总是以/开头，/就表示首页，最后的HTTP/1.1指示采用的HTTP协议版本是1.1。目前HTTP协议的版本就是1.1，但是大部分服务器也支持1.0版本，主要区别在于1.1版本允许多个HTTP请求复用一个TCP连接，以加快传输速度。

从第二行开始，每一行都类似于Xxx: abcdefg：

```
    Host: www.sina.com
```

表示请求的域名是www.sina.com。如果一台服务器有多个网站，服务器就需要通过Host来区分浏览器请求的是哪个网站。

### 2.2 服务器响应

继续往下找到Response Headers，点击view source，显示服务器返回的原始响应数据：

![image-20201115184923998](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184923998.png)

HTTP响应分为Header和Body两部分（Body是可选项），我们在Network中看到的Header最重要的几行如下：

```
    HTTP/1.1 200 OK
```

200表示一个成功的响应，后面的OK是说明。

如果返回的不是200，那么往往有其他的功能，例如

- 失败的响应有404 Not Found：网页不存在
- 500 Internal Server Error：服务器内部出错
- ...等等...

```
    Content-Type: text/html
```

Content-Type指示响应的内容，这里是text/html表示HTML网页。

> 请注意，浏览器就是依靠Content-Type来判断响应的内容是网页还是图片，是视频还是音乐。浏览器并不靠URL来判断响应的内容，所以，即使URL是`http://www.baidu.com/meimei.jpg`，它也不一定就是图片。

HTTP响应的Body就是HTML源码，我们在菜单栏选择“视图”，“开发者”，“查看网页源码”就可以在浏览器中直接查看HTML源码：

![image-20201115184942515](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184942515.png)

#### 浏览器解析过程

> **当浏览器读取到新浪首页的HTML源码后，它会解析HTML，显示页面，然后，根据HTML里面的各种链接，再发送HTTP请求给新浪服务器，拿到相应的图片、视频、Flash、JavaScript脚本、CSS等各种资源，最终显示出一个完整的页面。所以我们在Network下面能看到很多额外的HTTP请求。**

![image-20201115184959368](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115184959368.png)

## 3. 总结

### 3.1 HTTP请求

跟踪了新浪的首页，我们来总结一下HTTP请求的流程：

#### 3.1.1 步骤1：浏览器首先向服务器发送HTTP请求，请求包括：

> 方法：GET还是POST，GET仅请求资源，POST会附带用户数据；
>
> 路径：/full/url/path；
>
> 域名：由Host头指定：Host: www.sina.com
>
> 以及其他相关的Header；
>
> 如果是POST，那么请求还包括一个Body，包含用户数据

#### 3.1.1 步骤2：服务器向浏览器返回HTTP响应，响应包括：

> 响应代码：200表示成功，3xx表示重定向，4xx表示客户端发送的请求有错误，5xx表示服务器端处理时发生了错误；
>
> 响应类型：由Content-Type指定；
>
> 以及其他相关的Header；
>
> 通常服务器的HTTP响应会携带内容，也就是有一个Body，包含响应的内容，网页的HTML源码就在Body中。

#### 3.1.1 步骤3：如果浏览器还需要继续向服务器请求其他资源，比如图片，就再次发出HTTP请求，重复步骤1、2。

> Web采用的HTTP协议采用了非常简单的请求-响应模式，从而大大简化了开发。当我们编写一个页面时，我们只需要在HTTP请求中把HTML发送出去，不需要考虑如何附带图片、视频等，浏览器如果需要请求图片和视频，它会发送另一个HTTP请求，因此，一个HTTP请求只处理一个资源(此时就可以理解为TCP协议中的短连接，每个链接只获取一个资源，如需要多个就需要建立多个链接)

HTTP协议同时具备极强的扩展性，虽然浏览器请求的是`http://www.sina.com`的首页，但是新浪在HTML中可以链入其他服务器的资源，比如`<img src="http://i1.sinaimg.cn/home/2013/1008/U8455P30DT20131008135420.png">`，从而将请求压力分散到各个服务器上，并且，一个站点可以链接到其他站点，无数个站点互相链接起来，就形成了World Wide Web，简称WWW。

![image-20201115185017581](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115185017.png)

### 3.2 HTTP格式

每个HTTP请求和响应都遵循相同的格式，一个HTTP包含Header和Body两部分，其中Body是可选的。

HTTP协议是一种文本协议，所以，它的格式也非常简单。

#### 3.2.1 HTTP GET请求的格式：

```
    GET /path HTTP/1.1
    Header1: Value1
    Header2: Value2
    Header3: Value3
```

每个Header一行一个，换行符是\r\n。

#### 3.2.2 HTTP POST请求的格式：

```
    POST /path HTTP/1.1
    Header1: Value1
    Header2: Value2
    Header3: Value3

    body data goes here...
```

当遇到连续两个\r\n时，Header部分结束，后面的数据全部是Body。

#### 3.2.3 HTTP响应的格式：

````
    200 OK
    Header1: Value1
    Header2: Value2
    Header3: Value3

    body data goes here...
```

HTTP响应如果包含body，也是通过\r\n\r\n来分隔的。

请再次注意，Body的数据类型由Content-Type头来确定，如果是网页，Body就是文本，如果是图片，Body就是图片的二进制数据。

当存在Content-Encoding时，Body数据是被压缩的，最常见的压缩方式是gzip，所以，看到Content-Encoding: gzip时，需要将Body数据先解压缩，才能得到真正的数据。压缩的目的在于减少Body的大小，加快网络传输。

## Web静态服务器-1-显示固定的页面

```python
#coding=utf-8
import socket


def handle_client(client_socket):
    "为一个客户端进行服务"
    recv_data = client_socket.recv(1024).decode("utf-8")
    request_header_lines = recv_data.splitlines()
    for line in request_header_lines:
        print(line)

    # 组织相应 头信息(header)
    response_headers = "HTTP/1.1 200 OK\r\n"  # 200表示找到这个资源
    response_headers += "\r\n"  # 用一个空的行与body进行隔开
    # 组织 内容(body)
    response_body = "hello world"

    response = response_headers + response_body
    client_socket.send(response.encode("utf-8"))
    client_socket.close()


def main():
    "作为程序的主控制入口"

    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    # 设置当服务器先close 即服务器端4次挥手之后资源能够立即释放，这样就保证了，下次运行程序时 可以立即绑定7788端口
    server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    server_socket.bind(("", 7788))
    server_socket.listen(128)
    while True:
        client_socket, client_addr = server_socket.accept()
        handle_client(client_socket)


if __name__ == "__main__":
    main()
```

### 服务器端

![image-20201115185055545](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115185055.png)

### 客户端

![image-20201115185113361](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115185113361.png)

## Web静态服务器-2-显示需要的页面

```python
#coding=utf-8
import socket
import re


def handle_client(client_socket):
    "为一个客户端进行服务"
    recv_data = client_socket.recv(1024).decode('utf-8', errors="ignore")
    request_header_lines = recv_data.splitlines()
    for line in request_header_lines:
        print(line)

    http_request_line = request_header_lines[0]
    get_file_name = re.match("[^/]+(/[^ ]*)", http_request_line).group(1)
    print("file name is ===>%s" % get_file_name)  # for test

    # 如果没有指定访问哪个页面。例如index.html
    # GET / HTTP/1.1
    if get_file_name == "/":
        get_file_name = DOCUMENTS_ROOT + "/index.html"
    else:
        get_file_name = DOCUMENTS_ROOT + get_file_name

    print("file name is ===2>%s" % get_file_name) #for test

    try:
        f = open(get_file_name, "rb")
    except IOError:
        # 404表示没有这个页面
        response_headers = "HTTP/1.1 404 not found\r\n"
        response_headers += "\r\n"
        response_body = "====sorry ,file not found===="
    else:
        response_headers = "HTTP/1.1 200 OK\r\n"
        response_headers += "\r\n"
        response_body = f.read()
        f.close()
    finally:
        # 因为头信息在组织的时候，是按照字符串组织的，不能与以二进制打开文件读取的数据合并，因此分开发送
        # 先发送response的头信息
        client_socket.send(response_headers.encode('utf-8'))
        # 再发送body
        client_socket.send(response_body)
        client_socket.close()


def main():
    "作为程序的主控制入口"
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    server_socket.bind(("", 7788))
    server_socket.listen(128)
    while True:
        client_socket, clien_cAddr = server_socket.accept()
        handle_client(client_socket)


#这里配置服务器
DOCUMENTS_ROOT = "./html"

if __name__ == "__main__":
    main()
```

### 服务器端

![image-20201115185133096](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115185133096.png)

### 客户端

![image-20201115185146913](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115185146913.png)

## Web静态服务器-3-多进程

```python
#coding=utf-8
import socket
import re
import multiprocessing


class WSGIServer(object):

    def __init__(self, server_address):
        # 创建一个tcp套接字
        self.listen_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        # 允许立即使用上次绑定的port
        self.listen_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        # 绑定
        self.listen_socket.bind(server_address)
        # 变为被动，并制定队列的长度
        self.listen_socket.listen(128)

    def serve_forever(self):
        "循环运行web服务器，等待客户端的链接并为客户端服务"
        while True:
            # 等待新客户端到来
            client_socket, client_address = self.listen_socket.accept()
            print(client_address)  # for test
            new_process = multiprocessing.Process(target=self.handleRequest, args=(client_socket,))
            new_process.start()

            # 因为子进程已经复制了父进程的套接字等资源，所以父进程调用close不会将他们对应的这个链接关闭的
            client_socket.close()

    def handleRequest(self, client_socket):
        "用一个新的进程，为一个客户端进行服务"
        recv_data = client_socket.recv(1024).decode('utf-8')
        print(recv_data)
        requestHeaderLines = recv_data.splitlines()
        for line in requestHeaderLines:
            print(line)

        request_line = requestHeaderLines[0]
        get_file_name = re.match("[^/]+(/[^ ]*)", request_line).group(1)
        print("file name is ===>%s" % get_file_name) # for test

        if get_file_name == "/":
            get_file_name = DOCUMENTS_ROOT + "/index.html"
        else:
            get_file_name = DOCUMENTS_ROOT + get_file_name

        print("file name is ===2>%s" % get_file_name) # for test

        try:
            f = open(get_file_name, "rb")
        except IOError:
            response_header = "HTTP/1.1 404 not found\r\n"
            response_header += "\r\n"
            response_body = "====sorry ,file not found===="
        else:
            response_header = "HTTP/1.1 200 OK\r\n"
            response_header += "\r\n"
            response_body = f.read()
            f.close()
        finally:
            client_socket.send(response_header.encode('utf-8'))
            client_socket.send(response_body)
            client_socket.close()


# 设定服务器的端口
SERVER_ADDR = (HOST, PORT) = "", 8888
# 设置服务器服务静态资源时的路径
DOCUMENTS_ROOT = "./html"


def main():
    httpd = WSGIServer(SERVER_ADDR)
    print("web Server: Serving HTTP on port %d ...\n" % PORT)
    httpd.serve_forever()

if __name__ == "__main__":
    main()
```

## Web静态服务器-4-多线程

```python
#coding=utf-8
import socket
import re
import threading


class WSGIServer(object):

    def __init__(self, server_address):
        # 创建一个tcp套接字
        self.listen_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        # 允许立即使用上次绑定的port
        self.listen_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        # 绑定
        self.listen_socket.bind(server_address)
        # 变为被动，并制定队列的长度
        self.listen_socket.listen(128)

    def serve_forever(self):
        "循环运行web服务器，等待客户端的链接并为客户端服务"
        while True:
            # 等待新客户端到来
            client_socket, client_address = self.listen_socket.accept()
            print(client_address)
            new_process = threading.Thread(target=self.handleRequest, args=(client_socket,))
            new_process.start()

            # 因为线程是共享同一个套接字，所以主线程不能关闭，否则子线程就不能再使用这个套接字了
            # client_socket.close() 

    def handleRequest(self, client_socket):
        "用一个新的进程，为一个客户端进行服务"
        recv_data = client_socket.recv(1024).decode('utf-8')
        print(recv_data)
        requestHeaderLines = recv_data.splitlines()
        for line in requestHeaderLines:
            print(line)

        request_line = requestHeaderLines[0]
        get_file_name = re.match("[^/]+(/[^ ]*)", request_line).group(1)
        print("file name is ===>%s" % get_file_name) # for test

        if get_file_name == "/":
            get_file_name = DOCUMENTS_ROOT + "/index.html"
        else:
            get_file_name = DOCUMENTS_ROOT + get_file_name

        print("file name is ===2>%s" % get_file_name) # for test

        try:
            f = open(get_file_name, "rb")
        except IOError:
            response_header = "HTTP/1.1 404 not found\r\n"
            response_header += "\r\n"
            response_body = "====sorry ,file not found===="
        else:
            response_header = "HTTP/1.1 200 OK\r\n"
            response_header += "\r\n"
            response_body = f.read()
            f.close()
        finally:
            client_socket.send(response_header.encode('utf-8'))
            client_socket.send(response_body)
            client_socket.close()


# 设定服务器的端口
SERVER_ADDR = (HOST, PORT) = "", 8888
# 设置服务器服务静态资源时的路径
DOCUMENTS_ROOT = "./html"


def main():
    httpd = WSGIServer(SERVER_ADDR)
    print("web Server: Serving HTTP on port %d ...\n" % PORT)
    httpd.serve_forever()

if __name__ == "__main__":
    main()
```

# http协议、web服务器-并发服务器-2

## Web静态服务器-5-非堵塞模式

### 单进程非堵塞 模型

```python
#coding=utf-8
from socket import *
import time

# 用来存储所有的新链接的socket
g_socket_list = list()

def main():
    server_socket = socket(AF_INET, SOCK_STREAM)
    server_socket.setsockopt(SOL_SOCKET, SO_REUSEADDR  , 1)
    server_socket.bind(('', 7890))
    server_socket.listen(128)
    # 将套接字设置为非堵塞
    # 设置为非堵塞后，如果accept时，恰巧没有客户端connect，那么accept会
    # 产生一个异常，所以需要try来进行处理
    server_socket.setblocking(False)

    while True:

        # 用来测试
        time.sleep(0.5)

        try:
            newClientInfo = server_socket.accept()
        except Exception as result:
            pass
        else:
            print("一个新的客户端到来:%s" % str(newClientInfo))
            newClientInfo[0].setblocking(False)  # 设置为非堵塞
            g_socket_list.append(newClientInfo)

        for client_socket, client_addr in g_socket_list:
            try:
                recvData = client_socket.recv(1024)
                if recvData:
                    print('recv[%s]:%s' % (str(client_addr), recvData))
                else:
                    print('[%s]客户端已经关闭' % str(client_addr))
                    client_socket.close()
                    g_socket_list.remove((client_socket,client_addr))
            except Exception as result:
                pass

        print(g_socket_list)  # for test

if __name__ == '__main__':
    main()
```

### web静态服务器-单进程非堵塞

```python
import time
import socket
import sys
import re


class WSGIServer(object):
    """定义一个WSGI服务器的类"""

    def __init__(self, port, documents_root):

        # 1. 创建套接字
        self.server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        # 2. 绑定本地信息
        self.server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self.server_socket.bind(("", port))
        # 3. 变为监听套接字
        self.server_socket.listen(128)

        self.server_socket.setblocking(False)
        self.client_socket_list = list()

        self.documents_root = documents_root

    def run_forever(self):
        """运行服务器"""

        # 等待对方链接
        while True:

            # time.sleep(0.5)  # for test

            try:
                new_socket, new_addr = self.server_socket.accept()
            except Exception as ret:
                print("-----1----", ret)  # for test
            else:
                new_socket.setblocking(False)
                self.client_socket_list.append(new_socket)

            for client_socket in self.client_socket_list:
                try:
                    request = client_socket.recv(1024).decode('utf-8')
                except Exception as ret:
                    print("------2----", ret)  # for test
                else:
                    if request:
                        self.deal_with_request(request, client_socket)
                    else:
                        client_socket.close()
                        self.client_socket_list.remove(client_socket)

            print(self.client_socket_list)


    def deal_with_request(self, request, client_socket):
        """为这个浏览器服务器"""
        if not request:
            return

        request_lines = request.splitlines()
        for i, line in enumerate(request_lines):
            print(i, line)

        # 提取请求的文件(index.html)
        # GET /a/b/c/d/e/index.html HTTP/1.1
        ret = re.match(r"([^/]*)([^ ]+)", request_lines[0])
        if ret:
            print("正则提取数据:", ret.group(1))
            print("正则提取数据:", ret.group(2))
            file_name = ret.group(2)
            if file_name == "/":
                file_name = "/index.html"


        # 读取文件数据
        try:
            f = open(self.documents_root+file_name, "rb")
        except:
            response_body = "file not found, 请输入正确的url"
            response_header = "HTTP/1.1 404 not found\r\n"
            response_header += "Content-Type: text/html; charset=utf-8\r\n"
            response_header += "Content-Length: %d\r\n" % (len(response_body))
            response_header += "\r\n"

            # 将header返回给浏览器
            client_socket.send(response_header.encode('utf-8'))

            # 将body返回给浏览器
            client_socket.send(response_body.encode("utf-8"))
        else:
            content = f.read()
            f.close()

            response_body = content
            response_header = "HTTP/1.1 200 OK\r\n"
            response_header += "Content-Length: %d\r\n" % (len(response_body))
            response_header += "\r\n"

            # 将header返回给浏览器
            client_socket.send( response_header.encode('utf-8') + response_body)


# 设置服务器服务静态资源时的路径
DOCUMENTS_ROOT = "./html"


def main():
    """控制web服务器整体"""
    # python3 xxxx.py 7890
    if len(sys.argv) == 2:
        port = sys.argv[1]
        if port.isdigit():
            port = int(port)
    else:
        print("运行方式如: python3 xxx.py 7890")
        return

    print("http服务器使用的port:%s" % port)
    http_server = WSGIServer(port, DOCUMENTS_ROOT)
    http_server.run_forever()


if __name__ == "__main__":
    main()
```

## Web静态服务器-6-epoll

### IO 多路复用

就是我们说的select，poll，epoll，有些地方也称这种IO方式为event driven IO。

select/epoll的好处就在于单个process就可以同时处理多个网络连接的IO。

它的基本原理就是select，poll，epoll这个function会不断的轮询所负责的所有socket，当某个socket有数据到达了，就通知用户进程。

### epoll简单模型

```python
import socket
import select

# 创建套接字
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 设置可以重复使用绑定的信息
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR,1)

# 绑定本机信息
s.bind(("",7788))

# 变为被动
s.listen(10)

# 创建一个epoll对象
epoll = select.epoll()

# 测试，用来打印套接字对应的文件描述符
# print(s.fileno())
# print(select.EPOLLIN|select.EPOLLET)

# 注册事件到epoll中
# epoll.register(fd[, eventmask])
# 注意，如果fd已经注册过，则会发生异常
# 将创建的套接字添加到epoll的事件监听中
epoll.register(s.fileno(), select.EPOLLIN|select.EPOLLET)

connections = {}
addresses = {}

# 循环等待客户端的到来或者对方发送数据
while True:

    # epoll 进行 fd 扫描的地方 -- 未指定超时时间则为阻塞等待
    epoll_list = epoll.poll()

    # 对事件进行判断
    for fd, events in epoll_list:

        # print fd
        # print events

        # 如果是socket创建的套接字被激活
        if fd == s.fileno():
            new_socket, new_addr = s.accept()

            print('有新的客户端到来%s' % str(new_addr))

            # 将 conn 和 addr 信息分别保存起来
            connections[new_socket.fileno()] = new_socket
            addresses[new_socket.fileno()] = new_addr

            # 向 epoll 中注册 新socket 的 可读 事件
            epoll.register(new_socket.fileno(), select.EPOLLIN|select.EPOLLET)

        # 如果是客户端发送数据
        elif events == select.EPOLLIN:
            # 从激活 fd 上接收
            recvData = connections[fd].recv(1024).decode("utf-8")

            if recvData:
                print('recv:%s' % recvData)
            else:
                # 从 epoll 中移除该 连接 fd
                epoll.unregister(fd)

                # server 侧主动关闭该 连接 fd
                connections[fd].close()
                print("%s---offline---" % str(addresses[fd]))
                del connections[fd]
                del addresses[fd]
```

#### 说明

- EPOLLIN （可读）
- EPOLLOUT （可写）
- EPOLLET （ET模式）

epoll对文件描述符的操作有两种模式：LT（level trigger）和ET（edge trigger）。LT模式是默认模式，LT模式与ET模式的区别如下：

```
LT模式：当epoll检测到描述符事件发生并将此事件通知应用程序，应用程序可以不立即处理该事件。下次调用epoll时，会再次响应应用程序并通知此事件。

ET模式：当epoll检测到描述符事件发生并将此事件通知应用程序，应用程序必须立即处理该事件。如果不处理，下次调用epoll时，不会再次响应应用程序并通知此事件。
```

### web静态服务器-epool

以下代码，支持http的长连接，即使用了`Content-Length`

```python
import socket
import time
import sys
import re
import select


class WSGIServer(object):
    """定义一个WSGI服务器的类"""

    def __init__(self, port, documents_root):

        # 1. 创建套接字
        self.server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        # 2. 绑定本地信息
        self.server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self.server_socket.bind(("", port))
        # 3. 变为监听套接字
        self.server_socket.listen(128)

        self.documents_root = documents_root

        # 创建epoll对象
        self.epoll = select.epoll()
        # 将tcp服务器套接字加入到epoll中进行监听
        self.epoll.register(self.server_socket.fileno(), select.EPOLLIN|select.EPOLLET)

        # 创建添加的fd对应的套接字
        self.fd_socket = dict()

    def run_forever(self):
        """运行服务器"""

        # 等待对方链接
        while True:
            # epoll 进行 fd 扫描的地方 -- 未指定超时时间则为阻塞等待
            epoll_list = self.epoll.poll()

            # 对事件进行判断
            for fd, event in epoll_list:
                # 如果是服务器套接字可以收数据，那么意味着可以进行accept
                if fd == self.server_socket.fileno():
                    new_socket, new_addr = self.server_socket.accept()
                    # 向 epoll 中注册 连接 socket 的 可读 事件
                    self.epoll.register(new_socket.fileno(), select.EPOLLIN | select.EPOLLET)
                    # 记录这个信息
                    self.fd_socket[new_socket.fileno()] = new_socket
                # 接收到数据
                elif event == select.EPOLLIN:
                    request = self.fd_socket[fd].recv(1024).decode("utf-8")
                    if request:
                        self.deal_with_request(request, self.fd_socket[fd])
                    else:
                        # 在epoll中注销客户端的信息
                        self.epoll.unregister(fd)
                        # 关闭客户端的文件句柄
                        self.fd_socket[fd].close()
                        # 在字典中删除与已关闭客户端相关的信息
                        del self.fd_socket[fd]

    def deal_with_request(self, request, client_socket):
        """为这个浏览器服务器"""

        if not request:
            return

        request_lines = request.splitlines()
        for i, line in enumerate(request_lines):
            print(i, line)

        # 提取请求的文件(index.html)
        # GET /a/b/c/d/e/index.html HTTP/1.1
        ret = re.match(r"([^/]*)([^ ]+)", request_lines[0])
        if ret:
            print("正则提取数据:", ret.group(1))
            print("正则提取数据:", ret.group(2))
            file_name = ret.group(2)
            if file_name == "/":
                file_name = "/index.html"


        # 读取文件数据
        try:
            f = open(self.documents_root+file_name, "rb")
        except:
            response_body = "file not found, 请输入正确的url"

            response_header = "HTTP/1.1 404 not found\r\n"
            response_header += "Content-Type: text/html; charset=utf-8\r\n"
            response_header += "Content-Length: %d\r\n" % len(response_body)
            response_header += "\r\n"

            # 将header返回给浏览器
            client_socket.send(response_header.encode('utf-8'))

            # 将body返回给浏览器
            client_socket.send(response_body.encode("utf-8"))
        else:
            content = f.read()
            f.close()

            response_body = content

            response_header = "HTTP/1.1 200 OK\r\n"
            response_header += "Content-Length: %d\r\n" % len(response_body)
            response_header += "\r\n"

            # 将数据返回给浏览器
            client_socket.send(response_header.encode("utf-8")+response_body)


# 设置服务器服务静态资源时的路径
DOCUMENTS_ROOT = "./html"


def main():
    """控制web服务器整体"""
    # python3 xxxx.py 7890
    if len(sys.argv) == 2:
        port = sys.argv[1]
        if port.isdigit():
            port = int(port)
    else:
        print("运行方式如: python3 xxx.py 7890")
        return

    print("http服务器使用的port:%s" % port)
    http_server = WSGIServer(port, DOCUMENTS_ROOT)
    http_server.run_forever()


if __name__ == "__main__":
    main()
```

### 小总结

I/O 多路复用的特点：

通过一种机制使一个进程能同时等待多个文件描述符，而这些文件描述符（套接字描述符）其中的任意一个进入读就绪状态，epoll()函数就可以返回。 所以, IO多路复用，本质上不会有并发的功能，因为任何时候还是只有一个进程或线程进行工作，它之所以能提高效率是因为select\epoll 把进来的socket放到他们的 '监视' 列表里面，当任何socket有可读可写数据立马处理，那如果select\epoll 手里同时检测着很多socket， 一有动静马上返回给进程处理，总比一个一个socket过来,阻塞等待,处理高效率。

当然也可以多线程/多进程方式，一个连接过来开一个进程/线程处理，这样消耗的内存和进程切换页会耗掉更多的系统资源。 所以我们可以结合IO多路复用和多进程/多线程 来高性能并发，IO复用负责提高接受socket的通知效率，收到请求后，交给进程池/线程池来处理逻辑。

### 参考资料

- 如果想了解下epoll在Linux中的实现过程可以参考：http://blog.csdn.net/xiajun07061225/article/details/9250579

## Web静态服务器-7-gevent版

```python
from gevent import monkey
import gevent
import socket
import sys
import re

monkey.patch_all()


class WSGIServer(object):
    """定义一个WSGI服务器的类"""

    def __init__(self, port, documents_root):

        # 1. 创建套接字
        self.server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        # 2. 绑定本地信息
        self.server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self.server_socket.bind(("", port))
        # 3. 变为监听套接字
        self.server_socket.listen(128)

        self.documents_root = documents_root

    def run_forever(self):
        """运行服务器"""

        # 等待对方链接
        while True:
            new_socket, new_addr = self.server_socket.accept()
            gevent.spawn(self.deal_with_request, new_socket)  # 创建一个协程准备运行它

    def deal_with_request(self, client_socket):
        """为这个浏览器服务器"""
        while True:
            # 接收数据
            request = client_socket.recv(1024).decode('utf-8')
            # print(gevent.getcurrent())
            # print(request)

            # 当浏览器接收完数据后，会自动调用close进行关闭，因此当其关闭时，web也要关闭这个套接字
            if not request:
                new_socket.close()
                break

            request_lines = request.splitlines()
            for i, line in enumerate(request_lines):
                print(i, line)

            # 提取请求的文件(index.html)
            # GET /a/b/c/d/e/index.html HTTP/1.1
            ret = re.match(r"([^/]*)([^ ]+)", request_lines[0])
            if ret:
                print("正则提取数据:", ret.group(1))
                print("正则提取数据:", ret.group(2))
                file_name = ret.group(2)
                if file_name == "/":
                    file_name = "/index.html"

            file_path_name = self.documents_root + file_name
            try:
                f = open(file_path_name, "rb")
            except:
                # 如果不能打开这个文件，那么意味着没有这个资源，没有资源 那么也得需要告诉浏览器 一些数据才行
                # 404
                response_body = "没有你需要的文件......".encode("utf-8")

                response_headers = "HTTP/1.1 404 not found\r\n"
                response_headers += "Content-Type:text/html;charset=utf-8\r\n"
                response_headers += "Content-Length:%d\r\n" % len(response_body)
                response_headers += "\r\n"

                send_data = response_headers.encode("utf-8") + response_body

                client_socket.send(send_data)

            else:
                content = f.read()
                f.close()

                # 响应的body信息
                response_body = content
                # 响应头信息
                response_headers = "HTTP/1.1 200 OK\r\n"
                response_headers += "Content-Type:text/html;charset=utf-8\r\n"
                response_headers += "Content-Length:%d\r\n" % len(response_body)
                response_headers += "\r\n"
                send_data = response_headers.encode("utf-8") + response_body
                client_socket.send(send_data)

# 设置服务器服务静态资源时的路径
DOCUMENTS_ROOT = "./html"

def main():
    """控制web服务器整体"""
    # python3 xxxx.py 7890
    if len(sys.argv) == 2:
        port = sys.argv[1]
        if port.isdigit():
            port = int(port)
    else:
        print("运行方式如: python3 xxx.py 7890")
        return

    print("http服务器使用的port:%s" % port)
    http_server = WSGIServer(port, DOCUMENTS_ROOT")
    http_server.run_forever()


if __name__ == "__main__":
    main()
```

## 知识扩展-C10K问题

参考文章 :

《单台服务器并发TCP连接数到底可以有多少》 http://www.52im.net/thread-561-1-1.html

《上一个10年，著名的C10K并发连接问题》 http://www.52im.net/thread-566-1-1.html

#  网络通信过程

### 1. 2台电脑的网络

![image-20201115185411465](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115185411465.png)

#### 说明

> 1. 如果两台电脑之间通过网线连接是可以直接通信的，但是需要提前设置好ip地址以及网络掩码
> 2. 并且ip地址需要控制在同一网段内，例如 一台为`192.168.1.1`另一台为`192.168.1.2`则可以进行通信

### 2. 使用集线器组成一个网络

![image-20201115185430516](C:\Users\Dillon\AppData\Roaming\Typora\typora-user-images\image-20201115185430516.png)

#### 说明

> 1. 当有多态电脑需要组成一个网时，那么可以通过集线器（Hub）将其链接在一起
> 2. 一般情况下集线器的接口较少
> 3. 集线器有个缺点，它以广播的方式进行发送任何数据，即如果集线器接收到来自A电脑的数据本来是想转发给B电脑，如果此时它还连接着另外两台电脑C、D，那么它会把这个数据给每个电脑都发送一份，因此会导致网络拥堵

### 3. 使用交换机组成一个网络

![image-20201115185444344](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115185444.png)

#### 说明

> 1. 克服了集线器以广播发送数据的缺点，当需要广播的时候发送广播，当需要单播的时候又能够以单播的方式进行发送
> 2. 它已经替代了之前的集线器
> 3. 企业中就是用交换机来完成多态电脑设备的链接成网络的

### 4. 使用路由器连接多个网络

![image-20201115185509240](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115185509.png)

### 5. 通信过程（复杂）

较为复杂的通信过程如：访问 www.itheima.com

![image-20201115185525756](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115185525.png)

#### 说明

> 1. 在浏览器中输入一个网址时，需要将它先解析出ip地址来
> 2. 当得到ip地址之后，浏览器以tcp的方式3次握手链接服务器
> 3. 以tcp的方式发送http协议的请求数据 给 服务器
> 4. 服务器tcp的方式回应http协议的应答数据 给浏览器

总结

- MAC地址：在设备与设备之间数据通信时用来标记收发双方（网卡的序列号）
- IP地址：在逻辑上标记一台电脑，用来指引数据包的收发方向（相当于电脑的序列号）
- 网络掩码：用来区分ip地址的网络号和主机号
- 默认网关：当需要发送的数据包的目的ip不在本网段内时，就会发送给默认的一台电脑，成为网关
- 集线器：已过时，用来连接多态电脑，缺点：每次收发数据都进行广播，网络会变的拥堵
- 交换机：集线器的升级版，有学习功能知道需要发送给哪台设备，根据需要进行单播、广播
- 路由器：连接多个不同的网段，让他们之间可以进行收发数据，每次收到数据后，ip不变，但是MAC地址会变化
- DNS：用来解析出IP（类似电话簿）
- http服务器：提供浏览器能够访问到的数据

![image-20201115185546785](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115185546.png)



## NAT(网络地址转换器)

![image-20201115185603464](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/20201115185603.png)

#### 说明

1. 当在家里用宽带链接上网时，会把电话线(今天很多地方都是光纤)---->调制解调制(简称猫)------->电脑等设备

2. 电脑会得到来自电信服务商的一个公网ip地址（切记只有公网ip地址才能上网），此时可以直接上网happy...

3. 为了能够让多台设备都可以上网，需要将数据进行“分流” 电话线(今天很多地方都是光纤)---->调制解调制(简称猫)------->路由器------>电脑等设备

4. 此时路由器的一端有一个公网ip地址，剩下的4个（路由器型号不同个数不同）可以接入电脑等设备 并且 它们的ip是私有ip(例如 192.168.1.2)

5. 当一个电脑（192.168.1.2）上网时，先通过DNS协议解析出某个域名对应的ip，然后

   > - 发送数据时,在经过路由器时转换为公网ip以及路由器自己分配的临时端口
   >
   > 192.168.1.2:6789----->192.168.1.1 路由器 116.226.52.212:6539------->猫---->万维网
   >
   > - 接收数据时,在经过路由器时转换为路由器之前记录的ip以及port
   >
   > 万维网------->猫----->116.226.52.212:6539 路由器 192.168.1.1 ---->192.168.1.2:6789