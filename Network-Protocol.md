---
title: 网络协议分析笔记
date: 2019-10-09 18:07:32
categories: 
    Network-Protocol
tags:
    网络协议分析
cover: http://r.photo.store.qq.com/psb?/V13Zm3q236IRIM/nVqiNm7f3qLkNJU1mnBNoWwrfQn9sJcV56ZX4xL3UY8!/r/dDQBAAAAAAAA
mp3: https://api.uomg.com/api/rand.music
---

# 网络协议



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/WcuhtEshLuy*FQ2PM4NOKVll8f*IgZXD4mHNYvisfB4!/r/dIMAAAAAAAAA)

# 1 TCP/IP概述

## osi模型（各层功能协议）

 应（针对特定应用的协议TELNET、FTP、SMTP、HTTP、DHCP、DNS、SSH）  

 表（数据格式转换ASCII、JPEG） 

 会（建立断开会话连接，数据分割传输管理NFS、SQL、RPC 、ASP）  

 传（两个节点之间的数据传输TCP、UDP）  

 网（地址管理路由选择IP、ICMP、RIP、OSPF(Open Shortest Path First））  

 数（建立维持释放链路连接，访问流量差错控制PPP、ARP（网络层也可以））  

 物（二进制bit流形式在物理媒体上传输数据RJ-45）



## tcp/ip协议栈与osi对比两个边界

 网络层以上使用IP地址，数据链路层以下使用mac地址

 传输层及以下OS内部实现，应用层OS外部实现

# 2 网络接口层协议

## 2.1 以太网协议

 应用环境

 链路层的数据传输和封装成帧

 无连接，不可靠  CSMA/CD协议检测冲突，多路访问  总线型，星型（交换机连接，工作在数据链路层，集线器是物理层）  透明传输：异步线路用字节填充，同步线路用比特填充。  因为是广播/共享信道，所以要使用MAC来寻址

 Ethernet 封装格式（各字段含义和字节数）

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/6VdX7rX3lmp.6haMeDoCdnAjetw2j4CdEmJ8.t6fuiY!/r/dLgAAAAAAAAA)

## 2.2 ppp

 应用环境

 通过调制解调器点对点拨号接入因特网

 ppp组成

 ppp封装

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/dFiLz9cWtYn9BVIt.dqJxj5BOjGs.3HVGP1HaDnYsQE!/r/dMMAAAAAAAAA)

 链路控制协议LCP||网络控制协议NCP

 链路静止（调制解调器发出载波信号，建立物理层连接）

 LCP链路建立（协商配置，LCP配置请求帧）

 进入认证（口令或挑战应答认证成功，进入网络层协议）

 网络层协议状态：分组交换，将数据包分组，实现并行发送。

 网络层配置完毕后，链路就进入可进行数据通信的链路打开状态，两个PPP端点可以彼此向对方发送分组

 链路的一端发出终止请求LCP分组请求终止链路连接

  

 ppp帧格式

 ppp工作流程（5个阶段）

 链路静止->链路建立->认证阶段->网络层协议->链路终止

 ppp两种认证

 口令PAP（两次握手，明文传输，安全低，速度快）

 挑战握手CHAP（三次握手，密文传输口令，单向散列函数安全性高）

# 3 地址解析协议ARP

## 3.1 ARP概述

 地址解析协议  实现从IP地址到MAC地址的映射  在TCP/IP模型中，ARP协议属于IP层；在OSI模型中，ARP协议属于链路层  ARP在Ethernet以上，归于网络层协议，在OSI中从下层为上层服务角度说属于数据链路层也可以

## 3.2 ARP原理

 广播请求，局域网中的所有主机接受ARP请求报文

 单播回应，接收方接收ARP请求后发现IP匹配，应答mac地址

## 3.3 代理ARP

 局域网内部主机发起跨网段的ARP请求时，出口路由器/网关设备将自身MAC地址回复请求时，该过程称为代理ARP  //跨网段时，主机通过出口路由器的默认网关地址解析出MAC地址，发给路由器左侧接口，路由器通过IP地址解析出目的主机的MAC地址，此时源和目的MAC都发生改变，IP地址不变。

 应用场景：没有路由功能的主机，有路由功能，目的地指向本地接口。

## 3.4 免费APR

 用于实现局域网内部IP地址冲突检测

 应用场景:IP地址修改，DHCP获取地址

## 3.5 逆向ARP

 帧中继环境下，用于实现IP和DLCI地址的映射。

## 3.6 翻转ARP

 无盘工作站通过RARP协议来获取IP地址。（通过MAC问IP）

## 3.7 ARP攻击与防护

 ARP欺骗：发送伪造的ARP应答包，更改攻击目标主机的ARP缓存表，实现网络监听

 防护:IP-MAC地址绑定，ARP个人防火墙，VLAN和交换机端口绑定，PPPoE拨号上网

# 4 互联网协议IP

## 4.1 IP概述

 定义：IP提供数据的无连接和不可靠传送功能，实现三层数据封装与IP寻址。

 两种服务:虚电路、数据报

 特点：不可靠，无连接，尽最大努力交付，点到点。

## 4.2 IP数据报

 IP数据报格式（固定首部的所有字段含义和字节数）

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/tbiaiawa99DUfaCDcYmmxE219g3w.Ozcw1ghne43vSY!/r/dFABAAAAAAAA)



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/46pAN0QJwLHROU5nhetQtY7V6YMBTaKoJHHK*nLc6Pk!/r/dLYAAAAAAAAA)



 IP头部变动（MAC地址改变，首部校验和改变，TTL改变，IP地址不变。）

 IP数据报分片  为什么需要分片？  何时需要分片？（IP数据报总长度大于MTU（网络最大传输单元））  分片后如何组装？（标识，标志 DF(0允许分片)MF(1还有分片)，片偏移8字节）  如何分片？  分片需要用到哪些字段，各字段的值分别代表什么含义？

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/bpcI.wf.JHTE5lLWTautcuSzjHpifVKCBjAwxbIKEAQ!/r/dLgAAAAAAAAA)

 



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/Spd.raeCnCnIZ8wFwaTgrnWeo3nw1PevcH2B3QfiWOo!/r/dFIBAAAAAAAA)

 IP数据报可选项（有哪些可选项？各可选项的作用和过程）  记录数据报经过的路由  记录数据报经过的路由和时间  源端指定必须经过的路由  路径MTU发现

 

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/TkxDqm7Hplz1P9zQcb31WMPDV3CnfEvBdsMPbI5Ujsw!/r/dE8BAAAAAAAA)

 

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/9Qx17FzHJb2WQhKxxnEPD57adQ7nQsEC*XxJNrHLbAQ!/r/dIMAAAAAAAAA)

 

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/iXIyhP*l7xMCAbBK3Cppbd3l*EsKSQD6Tud3w***HtQ!/r/dFMBAAAAAAAA)

# 5 Internet控制报文协议ICMP

## 5.1 ICMP概述

 用于实现链路连通性测试和链路追踪，可 以实现链路差错报告

 功能：数据报在传送中可能会遇到各种异常；   IP层需要控制功能（拥塞、差错控制）。 

## 5.2 ICMP数据报类型

 ICMP报文的封装

 

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/bK1WIgJFAoEPGZViJ7AX*xi8UO3IPqACIQ4k.1l73wg!/r/dAcBAAAAAAAA)

 

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/JJCgBh0hpnT1wshBq0i.QT.LSglHiO0kVuMJrUYGuLc!/r/dL4AAAAAAAAA)

 

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/aWSb4ZlyQW1dcXLiKbYDaqqX2ekSSv.D99fQ2yH0gRc!/r/dFQBAAAAAAAA)

 ICMP数据报类型

 ICMP不可达

 包含：类型值，代码值，校验

######  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/73lJjRe1z3leawLpmQ3M*0uIti2BUjKZOrcqaG.uj5U!/r/dFQBAAAAAAAA)

 

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/PkY.HTqCqHCh34RJr8j4XNuEjwZsmtJcEw9C4op5pwg!/r/dLYAAAAAAAAA)

 

 主机不可达（类型值:3，代码值1）

 端口不可达（类型值:3，代码值3）

 禁止不可达（类型值:3，代码值13）

 分片不可达（类型值:3，代码值4）

 ICMP重定向（类型值:5，代码值1）

 当本地收到IP数据包目的地下一跳IP地址与源发送者处于同网段时，则告知源发送者将路由重定向到邻居设备。

## 5.3 基于ICMP开发的工具

 ping命令

 测试网络连通性，以及延迟等

 原理都是基于ICMP回显和应答报文

 traceroute（unix）/tracert（win）命令

 最常用的链路追踪工具，探测源目双方沿途设备的IP地址

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/wahJ5wiWQJt6SF9kV23D.cKnbenmlF0D8hzOZ0bpHq4!/r/dLgAAAAAAAAA)

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/wQXUx4LO2CEWJsoPdBKZmKl*o32BxsPbk3YziYR77Ag!/r/dLgAAAAAAAAA)

## 5.4 ICMP的一些安全问题

 基于ICMP的Dos攻击

 广播发送ICMP回显请求报文（将源IP地址为被攻击者的IP）

 基于ICMP的重定向路由欺骗

 ICMP重定向报文是当主机采用非最优路由发送数据报时，路由器会发回ICMP重定向报文来通知主机最优路由的存在

 ICMP重定向攻击也可以达到类似ARP欺骗的攻击效果。假设主机A(IP地址为172.16.1.2)经默认路由器(IP地址为172.16.1.1)与另一个网络中的主机D(IP地址为172.16.2.2)通信，与主机A同属一个网络的攻击者(IP地址为172.16.1.4)，通过修改内核设置，充当与主机A直接相连的路由器。攻击者要想监听主机A 的通信内容，可以构造如图1所示的ICMP重定向报文，指示主机A将数据包转发到攻击者的机器上，攻击者对所有的数据进行过滤后再转发给默认路由器，这就是“中间人”攻击。同样，ICMP重定向攻击也可以达到拒绝服务(DoS)攻击的目的。

# 6 用户数据报协议UDP

## 6.1 udp概述

 端口理解，通讯五元组

 端口:为每个协议按用户可能 要求的服务种类设置一 些抽象的访问目的点  通讯五元组：源IP地址，目的IP地址，源端口号，目的端口号，协议

 udp定义

 用户数据报协议，提供面向无连接的不可靠传输服务，传输层协议

 udp特点

 无连接，不可靠，不分片，速度快，实时性（媒体流）

 基于udp传输协议

 DHCP，DNS,TFTP,OICQ

## 6.2 udp报文

 udp报文格式

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/r45H6QkRBLsVVDUGTxjUXrAOXDBWMRCH6zeXLE.vRLc!/r/dLgAAAAAAAAA)

 udp封装

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/rFfPClsDG1CwvYjpku*7IYKCptoNusNWpzCQP8KJSiU!/r/dE0BAAAAAAAA)

## 6.3 udp安全问题

 udp洪泛攻击

 攻击者通过向中间服务器发送伪造被攻击者的源IP和源端口请求报文，中间服务器应答报文转向被攻击者（要求：服务器对IP地址真实性不作检查）

# 7 传输协议TCP

## 7.1 TCP概述

 TCP功能

 提供面向连接的可靠传输服务，属于传输层协议（无差错，不丢失，不重复，按序到达）

 面向字节流传输服务，通过MSS字段对数据进行分段传输

 TCP协议通过确认机制、重传机制等方式保证数据可靠传输。  TCP协议通过滑动窗口、拥塞避免等机制实现流量控制。

## 7.2 TCP报文

 TCP报文的封装

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/hRIwMpx3QEtXco*7BW.cyKgozXy280iUCQmKFc57fro!/r/dFQBAAAAAAAA)

 TCP报文的格式（固定首部的所有字段含义和字节数）

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/9G5r.ixdNG2L0HHIDXeWDR1zSukVq8d6I1rcLXhhCvw!/r/dIMAAAAAAAAA)

## 7.3 TCP连接

 TCP三次握手

 A、B关闭状态CLOSED—>B收听状态LISTEN—>A同步已发送状态SYN-SENT  —>B同步收到状态SYN-RCVD—>A、B连接已建立状态ESTABLISHED

 TCP四次挥手

 A、B连接建立状态ESTABLISHED—>A终止等待1状态FIN-WAIT-1—>B关闭等待状态CLOSE-WAIT—>  A终止等待2状态FIN-WAIT-2—>B最后确认状态LAST-ACK—>A时间等待状态TIME-WAIT—>B、A关闭状态CLOSED

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/b5.1w2YilC08G3tueeApO7bVSmZvas1iZzUG5DH1Eb0!/r/dL8AAAAAAAAA)

 TCP连接关闭超时（半关闭）

 当TCP一方发送FIN位进行单方向会话关闭时，另一方仍然可以发送数据给对方，此状态称为TCP半关闭状态。

## 7.4 TCP可靠传输

 确认机制

 通过序列号、确认号、分组长度等字段，接收方对发送方的数据进行实时反馈  在不丢包的情况下，一般依据【ack(n+1)=seq(n)+len(n)】方式进行可靠确认  若返回ack<seq(n)+len(n)，说明数据包丢失(实际过程中不一定）此时发送方需要进行数据重传

 重传机制

 超时重传

 （被动式）发送方等待RTO时间，没有收到接收方的确认，就启动重传

 快速重传

 （主动式）接收方本身检测到数据包丢失了（如收到 1、2、3、5、6序号的包，说明序号为4的数据包丢失）， 接收方主动返回ACK信息告知接收方，要求重传，这是快速重传机制

 选择性重传

 发送方仅仅需要重新发送丢失序号的数据包，提高数据恢复的效率。

## 7.5 TCP流量控制

 TCP滑动窗口机制

 RTT:发送一个数据包到收到ACK应答时间

 RTO：重传时间间隔

 对端通告的接收窗口rwnd

 拥塞控制窗口cwnd

 发送窗口的上限值=min（rwnd-cwnd）

 慢启动门限ssthresh

 MMS:maximum segment size，最大分节大小

[原理视频](https://www.bilibili.com/video/av52231781"视频讲解")



 TCP端到端流量控制

 通过调节发送速度达到匹配收发双方处理速度，极端情况使用0窗口通告来停止输出

 接收方主机确认时，使用窗口通告向发送方主机告知自己接收缓冲区的大小，以便源主机扩大或缩小它的发送端口大小

 糊涂窗口综合征SWS

 SWS定义:接收方的小窗口通告导致发送方发送一系列的小的报文段，严重降低网络带宽利用率

 0窗口通告导致，有一个字节的空间就生成确认，发送方发送一字节，往复从而稳定形成浪费

 避免策略：等缓冲区可用空间至少达到总空间的一半或达到MSS之后才发送新的窗口通告；在窗口大小不足以达到避免该策略锁制定的限度时推迟发送确认

## 7.6 TCP拥塞控制

 拥塞控制（方法）

 成因：对时延增加的反应重传数据，重传可能进一步导致加剧拥塞，可能造成拥塞崩溃

 解决方法：慢启动+拥塞避免+快速重传+快速恢复

 慢启动与拥塞避免

 当cwnd<ssthresh时，使用慢启动算法;当cwnd>ssthresh时则使用拥塞避免算法

 慢启动：新链接开始或解除拥塞后，都仅以一个报文段作为拥塞窗口cwnd初始值，此后每收到一个ACK，cwnd增加1个MSS

 拥塞避免算法：窗口中所有报文段都被确认后才将cwnd增加一个MSS

 加速递减算法：出现超时重传时，立即将慢启动门限值ssthresh设置为出现拥塞时发送窗口大小的一半(指数级递减)对于保留在发送窗口中的报文段，将重传定时器的时限加倍

 快速重传与快速恢复

 不等重传定时器超时就可以重传看起来已经丢失的报文段，不是取消重传定时器是预判（连续收到三个或者三个以上重复的ACK）

 快速恢复算法：每当发送方收到一个重复的ACK就说明已经有一个报文段离开了网络并进入了接收方的缓存。于是TCP发送端可以继续发送新的报文段而不必使用慢启动来突然减少数据流

## 7.7 TCP定时器

 重传定时器（作用和应用场景）

 当 TCP发送报文段时，就创建重传计时器，为了控制丢失或丢弃报文段，计时器超时之前收到对报文段的确认，撤销计时器，否则重传报文

 重传定时器使用于当希望收到另一端的确认

 坚持定时器

 接收方发送0窗口通告，之后接收方发送新的窗口通告在途中丢失。为了避免死锁，  在发送方接收到0窗口通告后，就要启动坚持定时器，定时探查是否有新的窗口通告

 保活定时器

 保活两小时，服务器收到客户端信息后重新计数，超时发送10个探测报文段（美75秒发送一个），无响应终止连接  保活定时器可检测到一个空闲连接的另一端何时崩溃或重启

 时间等待定时器

 TCP连接关闭，在时间等待期间，连接还处于中间过度状态，让TCP有  时间发送最后一个ACK，防止该ACK丢失，等2MSL时间才真正关闭

# 8 路由协议概述

## 8.1 路由协议分类

 运行特征分类：  距离矢量协议(RIP,BGP)  链路状态协议(OSPF,ISIS)

 运行范围分类：  IGP内部网关协议  EGP外部网关协议

 有类无类分类：  有类RIPv1，IGRP  无类RIPv2,EIGRP,OSPF,ISIS,BGP

## 8.2 通用路由选择算法

 最长匹配原则

 将通信目的IP和本地路由条目进行对比，从左到右，若匹配的比特位越多，则越优先

 管理距离（优先级）

 网络中有多种路由协议时，路径选择0-255

 Connected 0 

 Static 1 

 RIP 120 

 EIGRP 90或170

 OSPF 110

 ISIS 115 

 BGP 20或200

 度量值

 只有一种路由协议时，可以用于执行 路径选择(RIP时跳数，OSPF开销cost100M/带宽)

# 9 选路信息协议RIP

## 9.1 RIP概述    

 特征:应用层，基于UDP协议520端口，IGP内，运行特征:距离矢量，

 最佳路径（选路）：管理距离（120），度量值（hop）

## 9.2 RIP工作原理

 动态学习<30s周期>

 每个有RIP功能的路由器在默认的情况下，每间隔30秒利用UDP 520端口向与它直连的网络邻居广播（RIPv1）或者组播（RIPv2）路由更新

 故障收敛

 路径改变不可达，向网络邻居广播

## 9.3 RIP基本部署和路由分组

 RIP路由分组

 request分组（用于刚启动时对邻居进行路由请求）

 response分组（用于承载和传递路由条目）

 特征：①周期更新（25.5-30s）；②广播更新（255.255.255.255）；③不可靠更新

## 9.4 RIP计时器

 更新计时器30s

 每30sRIP路由器向邻居发送广播更新报文

 失效计时器180s

 当180s没有收到更新，则此路由失效

 抑制计时器180s

 当收到故障路由之后，保持180s之后 再删除路由条目。

 刷新计时器240s

 当240s没有收到更新，则此路由从路由表中移除

## 9.5 RIPv1 VS RIPv2

 有类（遵循ABC类网络规定）/无类  RIPv2组播更新，RIPv1广播更新  RIPv2传递路由时，夹带子网掩码信息  RIPv2增量更新+周期更新，RIPv1周期更新   （增量：只发送产生变动的路由，并且不受30s影响）

## 9.6 RIP路由算法

 ①如果收到邻居给的路由，若本地没有，则接收；  ②如果收到邻居给的路由，若本地有，根据度量值对比， 若优则录入，若劣质则丢弃；  ③如果收到邻居给的路由，若劣质，但是还是从原有的 邻居学到的，也录入。

## 9.7 RIP路由防环

 RIP路由环路形成原因

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/Tjq3LrTZDr*zjTZ6DSRqrRxg1E*w6BwxJabnAleohkM!/r/dMQAAAAAAAAA)

 RIP防环机制

 水平分割定义：从本接口收到的路由条目，不能再从 本接口发送出去。

 最大16跳定义：若RIP的路由条目跳数达到16跳，则 此路由失效并且被丢弃。

 毒化定义：若RIP的路由条目发生故障时，会将此路 由标记为16跳，并发送给邻居，告知邻居此路由有问 题，尽快删除。

 毒性逆转定义：若RIP的路由条目发送故障时，会将 此路由标记为16跳，并发送给邻居，邻居会返回16跳 的中毒路由，实现确认。

 抑制计时器定义：当收到故障路由之后，默认会直接删除本故障路由；若此时从远方又收到此路由，可  能造成再一次的环路；所以设置抑制计时器，当收到故障路由之后，保持180s之后再删除路由条目。

# 10 开放最短路径优先OSFP

## 10.1 OSPF概述

 基于传输层，IP协议号89，无类路由协议，运行特征:链路状态协议，IGP（内部网关协议）

  

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/V4SWeUVN8DhOxpmTCRBf9C1MQW2nugmKwbzHDKWzqxY!/r/dFYBAAAAAAAA)

 最佳路径（如何选路）：管理距离(110)，度量值(cost)= 100M/带宽（m）。

## 10.2 OSPF基本部署

 进程号

 范围1-65535，本地标识，用于标识或区分不同的OSPF进程（邻居之间采用不同进程，可以正常通信）

 路由标识符

 用于域内唯一地标志OSPF路由器（手工指定，环回口IP最大，选择物理口IP最大）

 反掩码（通配符掩码）

 标识需要通告的网段范围，0表示精确匹配， 1表示随意。

 区域划分（拓补层次性，减少路径计算，易管理）

 AS0骨干区域，中转其他区域流量防环；AS12常规区域连接分点，汇聚流量

## 10.3 OSPF邻居建立和路由分组

 1 OSPF邻居建立

 Down：两边都处于“沉默”状态  Init：一边开始发送hello分组  2way：两边相互发送hello分组，neighbor 状态，并且执行DR/BDR选举  Exstart：执行Master/Slave选举  Exchange：交换DBD分组  Loading：相互加载对方链路状态信息  Full:表示数据库达到一致，邻接状态

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/g1eQm3sa3rFZFYeUEivMVjiphR5BcYKpbjhBGLS4MHY!/r/dL8AAAAAAAAA)

 OSPF的路由分组

 Hello分组：用于建立和维持邻居关系

 DBD分组：数据库描述符，用于对OSPF的网络拓补进行描述

 LSR分组：用于对LSU进行真正的请求，即用于请求邻居链路状态信息

 LSU分组:用于承载和传递链路信息

 LSACK分组:用于对于LSU等分组进行可靠确认

## 10.4 OSPF两种选举机制

 DR/BDR选举

 DR：连接有多个路由器的网络中，指定其中一个路由器负责向外发 送该网络中所有链路状态信息。

 Master/Slave选举

 OSPF主从选举：保证DBD数据库描述信息可靠更新   MS，主从位（1表示Master，0表示Slave）

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/WFmooTusQb.8HsIJLkD0q5Z2uf0rwY.a7aGPXu17n*c!/r/dLYAAAAAAAAA)

## 10.5 OSPF的LSA分组

 1 Router LSAs   2 Network LSAs   3 or 4 Summary LSAs   5 Autonomous system  external LSAs   6 Multicast OSPF LSA   7 Defined for not-so-stubby areas   8 External attributes LSA for  Border Gateway Protocol (BGP)

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/zMmzIOpeFuWuoZA9RJs*RpTo*N1sUdZgOjlml83*cP0!/r/dL8AAAAAAAAA)

# 11 HTTP

## 11.1 http概述

 http超文本传输协议，实现web客户端与服务器之间通信，基于TCP默认端口80

 HTTP协议具备无连接无状态的特点，每次请求响应都是独立的，服务器默认无法“记住”客户端。

 最常使用的版本1.1

## 11.2 http请求和响应

 请求行Request Line/响应行Response

 请求头/响应头 Header

 请求/响应数据 Body

## 11.3 常见的请求方法

 GET 用于请求指定页面信息。请求访问的内容会显示在浏览器地址栏中

 POST 用于请求并提交内容到指定页面信息。数据被包含在请求体中。比GET安全。

 HEAD 类似于GET请求，只不过返回的响应中没有具体的内容，用于获取报头

 HTTP1.1新增了五种请求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT 方法。

## 11.4 HTTP消息报文

 请求字段

 HOST

 表示请求的主机和端口。（从哪去）

 User-Agent

 将客户端的操作系统和浏览器信息告知服务器。

 Referer

 表示从哪个链接跳转到此页面的，包含一个URL。（从哪来）  用于广告统计，安全分析，CDN统计

 Cookie

 用于记录客户端的身份信息。可以通过Cookie登录网站。

 Accept系列

 Accept-Charset：表示客户端能接受的字符集。  Accept-Encoding：表示客户端能接受的编码。  Accept-Language：表示客户端能接受的语言

 图片

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/4QuMQq9Ml5m84GxTY6SokHmC7W1fDIjIi0He6FbnkYE!/r/dLYAAAAAAAAA)

 响应字段

 Server

 表示Web服务器信息。如Apache，Microsoft-IIS

 X-Powered-By

 表示服务器的程序版本。如PHP，ASP，JAVA

 Set-Cookie

 服务器通过此字段为客户端设置Cookie信息，后续客户端根据此Cookie来进行请求

 Location

 服务器告知客户端去哪里访问这个资源，用于重定向，配合状态码302使用

 图片

  

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/mLqibtFOBlbTTReqOUmngGIPPXINSPf3hH.NdYfWkas!/r/dLYAAAAAAAAA)

 通用字段

 Connection

 用于表示连接是否可以继续。如重定向则置为close。

 Data

 用于标识内容产生时间

  ![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/I0hBesx4hpFKrgxU68vV74HJoZh9AmhBWmiwcyDEMNg!/r/dL4AAAAAAAAA)

 实体字段

 Content-Type

 ![img](http://r.photo.store.qq.com/psb?/V13Zm3q22BacOv/Qz0I3Q*X.nirTN9Z1w7eZVXGtytn8VrvTktBTECb2SU!/r/dFMBAAAAAAAA)

 表示实体内容的介质类型。

 Content-Length

 表示实体内容的长度。



------

