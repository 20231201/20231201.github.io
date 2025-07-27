---
title: 网安基础知识（shell,ip,osi,vm联网,proxifer等）python基础
---

# 网安基础知识（shell,ip,osi,vm联网,proxifer等）python基础

​      December 04, 2023            10150    

[TOC]

## shell的方式

在实战中，大多数采用反向shell，因为正向shell有很多因素导致连接失败，
比如说硬件设备有防火墙，入侵防御系统等，还有网站防火墙，端口占用，权限不足等场景，特别是硬件设备如果你正向连接被防火墙拦截导致打草惊蛇，后期攻击相当繁琐。
反向shell：而被控制端主动向外发送的数据包通常都不会被拦截。

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)点击查看图片来源

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)shell

### 1.反弹shell

反向shell：服务端想要获得客户端的shell（也就是反弹shell），被控制端主动连接控制端

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)反弹shell

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)反弹

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)反弹shell过程

### 2.正向shell

正向shell：客户端想要获得服务端的shell，控制端主动发起连接去连接被控制端

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)正向

## IP

ping 其它主机

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)ping

防火墙问题

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)防火墙

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)防火墙1

### IP格式

IPv4和IPv6是Internet Protocol version 4和Internet Protocol version 6的简称。它们都是Internet上用于标识和定位设备的IP地址格式。

IPv4是较早的IP协议版本，它使用一个32位二进制数字来表示IP地址。也就是说，一个IPv4地址，通常呈现为4个由点分开的十进制整数，每个整数取值范围为0到255。例如，192.168.1.1就是一个常见的IPv4地址。这种格式的IP地址已经被广泛应用于现代互联网，但是IPv4地址的可用数量有限，只有约42亿个地址是可用的。由于互联网的快速发展，IPv4地址空间在数年内就被耗尽。8.8.8.8/n

IPv6是IPv4的继任者，它使用一个128位的二进制数字来表示IP地址。IPv6的地址长度远比IPv4更长，其地址格式通常呈现为8个由冒号分开的十六进制整数，每个整数取值范围为0到FFFF。例如，2001:0db8:85a3:0000:0000:8a2e:0370:7334就是一个IPv6地址。IPv6比IPv4支持更多的地址，其可用的地址数量可以达到3402的39次方，远远超过了IPv4地址空间的极限。IPv6的地址格式通常为8组由冒号分隔的16位十六进制数

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)IPv46

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)IP地址

### [子网掩码](https://so.csdn.net/so/search?q=子网掩码&spm=1001.2101.3001.7020)

子网掩码是用来划分网络地址和主机地址的一种二进制值。它是由32 bits或128  bits二进制数字组成。在TCP/IP网络中，网络地址和主机地址是由IP地址组成的。子网掩码定义了一个网络中的主机地址和网络地址之间的边界，通常用于划分网络和主机地址。子网掩码和IP地址一起用于标识网络中的主机。子网掩码通常用点分十进制形式表示，例如255.255.255.0。在划分网络时，子网掩码可以被修改，以便分配更多或更少的IP地址给不同的子网。这对于组织内部或大型网络来说是非常有用的，因为它能够更有效地分配IP地址，并提高网络的性能和管理能力。

### 网络地址

网络地址是一种IP地址，用于标识网络中的一个节点或子网。在IPv4协议中，网络地址通常由一个32位的二进制数表示，通常用四个十进制数字表示，每个数字之间由句点（.）隔开，如192.168.1.0。

网络地址通常是由网络管理员或ISP分配给网络中的所有设备和主机使用。他们将拥有相同的网络地址，但是在同一个网络中的每个设备和主机都需要一个唯一的主机地址。这个唯一的主机地址可以通过给每个设备和主机分配不同的IP地址来完成。

网络地址在子网中起到重要作用。它定义了子网的范围和边界，并对子网中的主机地址进行了控制。当主机试图发送数据到其他子网或互联网时，它们需要将数据包发送到网关（也称为路由器），由网关对数据包进行转发。

需要注意的是，网络地址本身不能用于唯一标识特定的设备或主机。一个网络地址可以被分配给多个设备或主机，这些设备或主机通过使用不同的主机地址来区分彼此。

### 广播地址

广播地址是指一种特殊的IP地址，用于将数据包从一个网络中的所有主机传递到另一个网络中的所有主机。在IPv4协议中，广播地址通常是由网络地址和一个全网掩码组成，其中主机部分全部为1。

例如，在192.168.1.0/24子网中，广播地址为192.168.1.255，这意味着当一个数据包被发送到这个地址时，它将被发送到这个子网中的所有主机。

广播地址常用于一些网络协议和应用程序中，比如DHCP、ARP、TCP/IP等，可以用来发送请求或通知所有的主机。但需要注意的是，在企业网络中，为了安全和性能方面的考虑，广播地址通常是被禁止的，只有在特定的情况下才会被允许使用。

### 网关

在计算机网络中，网关（Gateway）是连接不同网络之间的一个网络节点，即两个或多个网络的交汇处，负责将数据包转发到目标网络。网关通常是一台路由器，具有路由选择、地址转换等功能。

在本地网络中，网关通常指本地网络到其他网络之间的连接设备，比如路由器或者交换机。当本地网络中的计算机需要访问其他网络时，必须通过网关来进行数据包的转发和接收。同时，网关也可以作为出入本地网络的”关卡”，对网络流量进行监控和管理，控制从本地网络向其他网络的数据流量。

网关通常需要配置一个IP地址，该地址应该和本地网络中的IP地址在同一个网段，并且不和其他已有的IP地址冲突。当网络流量需要转发至其他网络时，数据包会被发送至网关的IP地址，然后网关会根据路由表，将数据包转发到目标网络。

例题：

192.168.1.1/30有多少个可供分配的IP地址

在IP子网划分中，一个/30的子网掩码意味着该子网中有4个IP地址。这是因为子网掩码/30将IP地址分为四个部分，其中包括：

1. 网络地址：这是子网的第一个IP地址，用于标识整个子网。在这个例子中，它是192.168.1.0。
2. 网关地址：这是子网的第二个IP地址，通常分配给网关或路由器。在这个例子中，它是192.168.1.1。
3. 可用主机地址1：这是子网的第三个IP地址，可用于分配给网络中的设备。在这个例子中，它是192.168.1.2。
4. 可用主机地址2：这是子网的第四个IP地址，同样可用于分配给网络中的设备。在这个例子中，它是192.168.1.3。
5. 广播地址：这是子网的最后一个IP地址，用于向子网内所有设备发送广播消息。在这个例子中，它是192.168.1.4。

因此，在192.168.1.1/30子网中，有2个可供分配的IP地址（192.168.1.2和192.168.1.3），其中192.168.1.1通常是分配给网关的，而其他的地址都有特定的用途。注意，不同的设备和操作系统可能会对这些地址有不同的使用限制和配置要求。

### 传统的用户IP分配方式

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)网络过程

一般用户所能分配的IP（私网）

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)私网IP

### 公网IP的分配

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)路由器内网pc通过公网ip访问映射的内网server案例

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

## 培训学习注意事项

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)规则

## 动态静态路由与动态静态IP及osi

### 动态静态路由

动态IP服务器分配，静态手动输入

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)静态与动态IP路由

### osi7层协议

OSI7层参考模型的各个层面的划定遵循下列原则：

　　1、同一层中的各节点都是有相同的层次模型，具备相同的功效。

　　2、相同节点内邻近层间根据接口（可以是逻辑接口）展开通信。

　　3、7层结构中的每一层采用下一层带来的服务，同时向其上层带来服务。

　　4、各个节点的相同层依照协议完成对等层间的通信。

　　第一层：物理层（PhysicalLayer)

　　要求通讯设备的机械的、电气的、功效的和流程的特点，用于创建、维护和拆卸物理链路连接。详细地讲，机械特点要求了网络连接时所需接插件的标准规格、引脚个数和排布情况等；电气特点要求了在物理连接上传送bit流时线路上讯号电平的高低、阻抗匹配、传输速度距离规定等；功效特点是指对各个讯号先分配确切的讯号含义，即界定了DTE和DCE间各个线路的功效；规程特性界定了运用信号线展开bit流传送的一组操作流程，是指在物理连接的创建、维护、互换信息是，DTE和DCE双放在各电路上的行为系列。在这一层，数据的单位被称作比特（bit）。是属于物理层界定的典型要求代表包括：EIA/TIARS-232、EIA/TIARS-449、V.35、RJ-45等。

　　第二层：数据链路层（DataLinkLayer)

　　在物理层带来比特流服务的前提上，创建邻近结点间的数据链路，根据差错控制带来数据帧（Frame）在信道上无差错的传送，并展开各电路上的行为系列。数据链路层在不稳定的物理介质上带来稳定的传送。该层的作用包括：物理地址寻址、数据的成帧、流量监控、数据的检错、重发等。在这一层，数据的单位被称作帧（frame）。数据链路层协议的代表包括：SDLC、HDLC、PPP、STP、帧中继等。

　　第三层：网络层（NetworkLayer)

　　在通信网络中开展通讯的两个计算机相互之间或许会历经许多个数据链路，也可能还需要历经许多通信子网。网络层的工作就是挑选适宜的网间路由和交换结点，保证数据及时数据传输。网络层将数据链路层带来的帧构成数据包，包中封装有网络层包头，当中含有逻辑地址数据–源站点和目标站点地址的网络地址。假如你在讨论一个IP地址，那你是在处理第3层的问题，这是“数据包”问题，而不是第2层的“帧”。IP是第3层问题的其中一部分，除此之外也有一部分路由协议和地址解析协议（ARP）。关于路由的所有问题都是在这第3层处理。地址解析和路由是3层的重要目标。网络层还可以实现拥塞控制、网际互连等用途。在这一层，数据的单位被称作数据包（packet）。网络层协议的代表包含：IP、IPX、RIP、OSPF等。

　　第四层：处理数据的传输层（TransimissionLayer)

　　第4层的数据单元也称作数据包（packets）。可是，如果你讨论TCP等详细的协议时又有特殊的称呼，TCP的数据单元被称作段（segments）而UDP协议的数据单元被称作“数据报（datagrams）”。这个层承担抓取所有数据，因此，它必须追踪数据单元碎片、乱序抵达的数据包和其余在数据传输过程中或许发生的风险。第4层为上层带来端到端（最终用户到最终用户）的透明的、可靠的数据传输服务。所为透明的数据传输是指在通讯过程中传输层对上层屏蔽了通讯数据传输系统的详细细节。传输层协议的代表包含：TCP、UDP、SPX等。

　　第五层：会话层（SessionLayer)

　　这一层还可以被称作会晤层或对话层，在会话层及以上的高层次中，数据数据传输的单位不会再另外命名，往往是统称为报文。会话层不参与详细的数据传输，它带来包含访问认证和会话管理以内的建立和维护应用相互之间通讯的机制。如服务器认证用户登入便是由会话层完成的。

　　第六层：表示层（PresentationLayer)

　　这一层主要是处理拥护数据的语法表达问题。它将欲交换的数据从合适于某个用户的抽象语法，变换为合适于OSI系统内部使用的数据传输语法。即带来格式化的表达和变换数据服务。数据的压缩和解压缩，加密和解密等工作都由表示层承担。

　　第七层：应用层（ApplicationLayer)

　　应用层为操作系统或网络应用程序带来访问网络服务的接口。应用层协议的代表包含：Telnet、FTP、HTTP、SNMP等。

### socks5传播

套接字（socket）是通信的基石，是支持TCP/IP协议的网络通信的基本操作单元。

它是网络通信过程中端点的抽象表示，包含进行网络通信必须的五种信息：

① 连接使用的协议；

② 本地主机的IP地址；

③ 本地进程的协议端口；

④ 远地主机的IP地址；

⑤ 远地进程的协议端口。

应用层通过传输层进行数据通信时，TCP会遇到同时为多个应用程序进程提供并发服务的问题。多个TCP连接或多个应用程序进程可能需要通过同一个
TCP协议端口传输数据。为了区别不同的应用程序进程和连接，许多计算机操作系统为应用程序与TCP／IP协议交互提供了套接字(Socket)接口。应
用层可以和传输层通过Socket接口，区分来自不同应用程序进程或网络连接的通信，实现数据传输的并发服务。

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)socksosi传递

### 路由器 ping的过程

假设有A、B、C、D四台机器，一台路由RA，子网掩码均为255.255.255.0，默认网关是192.168.0.1
 　　1.同一网段
 　　我们来看一下在A主机上执行“Ping  192.168.0.5”后，都发生了些什么。首先，Ping会通知系统建立一个固定格式的ICMP请求数据包，然后由ICMP协议打包这个数据包和地址“192.168.0.5”转交给IP层协议（一组后台运行的进程，与ICMP类似），IP层协议将以地址“192.168.0.5”作为目的地址，本机IP地址作为源地址，加上一些其他的控制信息，构建一个IP数据包，并想办法得到192.168.0.5的MAC地址（物理地址，这是数据链路层协议构建数据链路层的传输单元——帧所必需的），以便交给数据链路层构建一个数据帧。关键就在这里，IP层协议通过机器B的IP地址和自己的子网掩码，发现它跟自己属同一网络，就直接在本网络内查找这台机器的MAC，如果以前两机有过通信，在A机的ARP缓存表应该有B机IP与其MAC的映射关系，如果没有，就发一个ARP请求广播，得到B机的MAC，一并交给数据链路层。后者构建一个数据帧，目的地址是IP层传过来的物理地址，源地址则是本机的物理地址，还要附加上一些控制信息，依据以太网的介质访问规则，将它们传送出去。
  　主机B收到这个数据帧后，先检查它的目的地址，并和本机的物理地址对比，如符合，则接收；否则丢弃。接收后检查该数据帧，将IP数据包从帧中提取出来，交给本机的IP层协议。同样，IP层检查后，将有用的信息提取后交给ICMP协议，后者处理后，马上构建一个ICMP应答包，发送给主机A，其过程和主机A发送ICMP请求包到主机B一模一样。
 　　2.不同网段
 　　在主机A上执行“Ping  192.168.1.4”后，开始跟上面一样，到了怎样得到MAC地址时，IP协议通过计算发现D机与自己不在同一网段内，就直接将交由路由处理，也就是将路由的MAC取过来，至于怎样得到路由的MAC，跟上面一样，先在ARP缓存表找，找不到可以利用广播。路由得到这个数据帧后，再跟主机D进行联系，如果找不到，就向主机A返回一个超时的信息。  

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)路由

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)pc1pingpc2经由路由12

## VMwareworkstation的联网

VMware虚拟网络各模式与路由的交互

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)虚拟机设置

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)桥接

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)nat

仅主机相当于断网了，此处不考虑

## proxifer

### 下载proxifer

### 代理服务器设置

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)Proxifier服务器

### 代理规则设置

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)Proxifier代理规则

### 验证

尝试ping其它主机并查看proxifer以验证是否成功

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)Proxifier3

### 工作方式

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)img

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)proxy

# python基础

## bytes

### 字符集和编码介绍

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)编码小结

### 编码与解码

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)例子：周杰伦用gbk编码是6个字节,btf-8是9个字节

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)解码

## python字典

### 字典的基本概念

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)表示方式

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)key和value的类型要求

### 基本字典操作

增加，修改

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)增加修改

删除

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)删除

查询

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)image-20231205215341101

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)查询

None元素

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)none

字典查询

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)查询

### 字典的key和value循环

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)字典的key和value循环

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)直接拿到key和value

元组和列表结构

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)元组和列表的结构

item是只有两项元素，通过a，b可直接指代

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)通过item直接拿到key和value

### 字典嵌套

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)字典嵌套

操作方式

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)对嵌套内操作

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)字典的循环删除

## 运算符

### 算术运算

+-*/%//

例如a=5,b=2

\+  两个对象相加               a+b=7

\-  两个对象相减               a-b=3

\*  两个对象相乘               a*b=10

/  两个数相除的结果（商）            a/b=2.5

//  两个数相除后取整（返回商的整数部分（**向下取整**））   a//b=2   -9//2=-5

%  两个数相除的余数　　　　　　　　　　　　　　　　　   a%b=1

**  a的多少次方　　　　　　　　　　　　　　　　　　　   a**b=25

### 比较运算

Python中的比较运算符包括：

1. 等于（==）：检查两个值是否相等。例如，3 == 3.0返回True。
2. 不等于（!=）：检查两个值是否不相等。例如，3 != 3.0返回False。
3. 大于（>）：检查左侧的值是否大于右侧的值。例如，3 > 2返回True。
4. 小于（<）：检查左侧的值是否小于右侧的值。例如，2 < 3返回True。
5. 大于或等于（>=）：检查左侧的值是否大于或等于右侧的值。例如，3 >= 2返回True。
6. 小于或等于（<=）：检查左侧的值是否小于或等于右侧的值。例如，2 <= 3返回True。

这些比较运算符可以用于任何数值类型，包括整数、浮点数和复数。此外，它们也可以用于字符串，但比较是基于字符的ASCII值进行的，而不是基于字符串的内容。例如，”abc” < “xyz”返回True，因为’a’的ASCII值小于’x’。

### 赋值运算

在Python中，赋值运算符用于将值赋给变量。最常用的赋值运算符是等于（=）。

下面是一些Python赋值运算符的例子：

1. 等于（=）：

```
x = 10  # 将10赋给变量x
```

1. 加等于（+=）：

```
x = 10
x += 5  # x = x + 5，所以 x 现在是15
```

1. 减等于（-=）：

```
x = 15
x -= 5  # x = x - 5，所以 x 现在是10
```

1. 乘等于（*=）：

```
x = 5
x *= 3  # x = x * 3，所以 x 现在是15
```

1. 除等于（/=）：

```
x = 15
x /= 3  # x = x / 3，所以 x 现在是5.0
```

1. 取模等于（%=）：

```
x = 10
x %= 3  # x = x % 3，所以 x 现在是1，因为10除以3的余数是1
```

1. 幂等于（**=）：

```
x = 2
x **= 3  # x = x ** 3，所以 x 现在是8，因为2的3次方是8
```

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)互换操作

### 逻辑运算

Python中的逻辑运算符包括`and`、`or`和`not`。

以下是一些使用这些运算符的例子：

1. `and`运算符：

```
# 如果x大于0且小于10，返回True
x = 5
if x > 0 and x < 10:
    print("x 在 0 和 10 之间")
```

在这个例子中，如果`x`大于0且小于10，那么条件会返回True。
\2. `or`运算符：

```
# 如果x等于0或10，返回True
x = 5
if x == 0 or x == 10:
    print("x 等于 0 或 10")
```

在这个例子中，如果`x`等于0或者10，那么条件会返回True。
\3. `not`运算符：

```
# 如果x不等于0，返回True
x = 5
if not x == 0:
    print("x 不等于 0")
```

在这个例子中，如果`x`不等于0，那么条件会返回True。注意`not`运算符只对后面的条件进行否定。

以上就是Python中的逻辑运算符及其用法的简单示例。

**如果同时出现时，优先级括号>not>and>or**

### 成员运算

Python中的成员运算符是`in`和`not in`。这些运算符用于检查一个值是否存在于一个序列（如列表、元组、字典、集合或字符串）中。

以下是一些使用成员运算符的例子：

```
# 检查一个值是否在列表中
fruits = ['apple', 'banana', 'cherry']
if 'apple' in fruits:
    print('Apple is in the list.')

# 检查一个值是否在元组中
colors = ('red', 'green', 'blue')
if 'red' in colors:
    print('Red is in the tuple.')

# 检查一个值是否在字典中
person = {'name': 'Alice', 'age': 25}
if 'Alice' in person:
    print('Alice is in the dictionary.')

# 检查一个值是否在集合中
colors = {'red', 'green', 'blue'}
if 'red' in colors:
    print('Red is in the set.')

# 检查一个字符是否在字符串中
text = 'Hello, world!'
if 'l' in text:
    print('The letter "l" is in the string.')
```

对于字符串，`in`运算符检查一个字符是否存在于字符串中。对于其他序列类型（如列表、元组、字典和集合），`in`运算符检查一个值是否存在于序列中。

## python文件操作

### 打开文件

使用 Python 打开一个文件，我们需要用到 open() 函数：

```
f = open("FishC.txt", "w")
```

第一个参数指定的是文件路径和文件名，这里我们没有添加路径的话，那么默认是将文件创建在 Python 的主文件夹下面，因为执行 IDLE  的程序就放在那里嘛（同样的道理，如果我们在桌面创建一个 test.py 的源文件，然后输入打开文件的代码，那么它就会在桌面创建一个  FishC.txt 的文本文件）。
第二个参数是指定文件的打开模式：
![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)打开模式字符含义

### 文件对象方法详细解析

（1）有两个方法可以将字符串写入到文本对象种，一个是 write()，一个是 writelines()：

```
f.write("I love Python.")
```

使用 write() 方法，它有一个返回值，就是总共写入到文件对象中的字符个数。

使用 writelines() 方法，则可以将多个字符串同时写入：

```
f.writelines(["I love FishC.\n", "I love my wife."])
```

注意：虽然 writelines() 方法支持传入多个字符串，但它不会帮你添加换行符，所以我们要自己添加才行。[/code]

### 关闭文件

我们使用 close() 方法来关闭文件：

```
f.close()
```

注意，文件对象关闭之后，我们就没办法对它进行操作了。

如果想要继续操作文件，那么我们必须重新打开它。

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)注意事项

### 路径修改

不同操作系统，它的这个路径分隔符是不一样的，比如 Windows 系统是使用反斜杠，而其他大多数操作系统则是使用斜杠来分隔。

这个 Windows 采用的反斜杠，跟字符串中的转义字符的反斜杠是同一条杠，那么，如果你想要在 Windows 上使用反斜杠来分隔路径，你就不得不用另一条反斜杠来转移反斜杠，或者使用原始字符串，并不是说这么做有多困难吧，就是觉得这样做不是那么优雅……

### 相对路径和绝对路径

相对路径：以当前目录作为基准，进而逐级推导（. . 表示上级目录；. 当前目录）。
绝对路径：文件真正存在的路径，从根目录逐级推导到指定的文件 / 文件夹。