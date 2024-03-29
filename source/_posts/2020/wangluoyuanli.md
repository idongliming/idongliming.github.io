---
title: 网络原理复习笔记
categories:
  - 学习笔记
tags:
  - 基础知识
keywords: 网络原理
top: ture
toc: false
date: 2020-06-14 16:51:48
---

# 概述
互联网的核心部分起特殊作用的是路由器. 路由器实现分组交换的关键构件, 其任务是转发收到的分组

- 电路交换的三个步骤:

	- 建立连接
	- 通话
	- 释放连接;在通话的全部时间内, 通话的两个用户始终占用全部端到端的通信资源
- 分组交换技术的主要特点:

	- 采用存储转发技术, 我们要发送的整块数据称为一个报文, 发送报文时将报文划分成登场数据段, 加上必要的首部就成了一个分组/包
	- 位于网络边缘的主机和位于网络核心部分的路由器都是计算机, 主机为用户进行信息处理, 路由器用来转发分组
	- 路由器收到分组, 暂时存储, 检查其首部, 查找转发表, 检查首部目的地址, 从合适的接口转发出去, 将分组交给下一个路由器
- 分组交换的主要有点

	- 高效, 在分组传输中动态分配传输贷款, 对通信链路逐段占用
	- 灵活, 为每一个分组独立的选择最合适的转发路由
	- 迅速, 以分组为单位, 可以不先建立连接就能向其他主机发送分组
	- 可靠, 保证可靠性的网络协议, 分布式多路由的分组交换网
	- 几种不同的计算机网络

- 作用范围:

	- 广域网(WAN)

	- 城域网(MAN), 覆盖范围5-50km, 采用以太网技术

	- 局域网(LAN), 范围1km

	- 个人区域网(PAN)和无线个人区域网(WPAN)

- 按照使用中分类

	- 公用网

	- 专用网

- 计算机网络的性能

- 计算机网络的性能指标

速率: 指数据的传送速率, 也称为数据率或比特率

带宽: 在频域中是信号具有的频带宽度, 在时域中网络通道内传送数据的能力

吞吐量: 单位时间内通过某个网络的实际数据量

时延是指数据(一个报文或者分组)从网络(链路)的一端传送带另一端所需的时间

发送时延: 是主机或路由器发送数据帧所需要的时间, 也叫传输时延, 发送时延=(数据帧长度)/(发送速率)

传播时延: 是电磁波在信道中传播一定的距离需要花费的时间, 传播时延=信道长度/电磁波在信道上的传播速率

电磁波在自由空间的传播速率是光速310^5Km/s, 在铜线电缆中的传播速率为2.310^5Km/s, 在光纤中的传播速率为2*10^5Km/s

发送时延是只在网络适配器内部转发分组的时延, 传播时延在链路中的发送时延

处理时延: 是主机或者路由器收到分组是花费一定的时间进行处理(分析首部等)

排队时延: 是分组经过网络传输是经过路由器后要先在输入队列中排队等待处理的时延

时延带宽积: 是传播时延和带宽相乘, 时延带宽积是指链路的容纳量

往返时间RTT, 发送时间=数据长度/发送速率, 有效数据率=数据长度/(发送时间+RTT)

利用率有信道利用率和网络利用率, 网络当前时延=网络空闲时的时延/(1 - 利用率)

计算机网络

协议与划分层次

网络协议是为进行网络中的数据交换而建立规则,标准或约定

语法, 即数据与控制信息的结构或格式
语义, 即需要发出何种控制信息, 完成何种动作以及做出何种响应
同步, 即事件实现顺序的详细说明
网络层次

各层是独立的. 不需要知道他的下一层是如何实现的, 只需要通过层间的接口提供服务

灵活性好, 当某一层发生变化时, 只要层间接口关系不便, 各层均不受影响

结构上可分割开, 各层采用最适合的技术来实现

易于实现和维护, 能够实现和调试一个庞大而又复杂的系统变得易于处理

能促进标准化工作

通常各层需要完成的功能

差错控制
流量控制
分段和重装
复用和分用
连接建立和释放
具有五层协议的体系结构

OSI参考模型具有七层体系结构, 物理层, 数据链路层, 数据链路层, 网路层, 传输层, 会话层, 表示层, 应用层OSI参考模型

TCP/IP参考模型, 链路层, 网络层, 传输层, 应用层

五层参考模型

应用层, 通过应用进程间的交互来完成特定网络应用, 交互数据单元称为报文

运输层, 负责向两台主机中的进程之间的通信提供数据传输服务, 并不指定某个特定层网络应用, 多种应用都可以使用同一个运输层服务, 因此有复用和分用的功能, 复用是指多个应用同时使用运输层服务, 分用是运输层收到的信息分别交付到应用层中的相应进程

transmission Control protocol协议—-提供面向连接的, 可靠的数据传输服务, 数据传输单位是报文段
User Datagram protocol协议—-提供无连接的,尽力的数据传输服务, 数据传输单位是用户数据报
网络层, 为分组交换网上的不同主机提供通信服务, 将运输层产生的报文段或用户数据报封装成分组或包进行传送, 分组也称IP数据报, 另一个任务是将源主机运输层传下来的分组通过网络中的路由器找到目的主机

数据链路层, 数据链路层将网络层交下来的网络IP数据报组装成帧, 在相邻结点链路上传送帧, 每一帧包括数据和必要的控制信息(如同步信息等)

物理层, 光纤等

人们经常提到的TCP/IP并不一定是指这两个具体协议, 往往是整个TCP/IP协议族

实体, 协议, 服务和服务访问点

协议是控制两个对等实体(或多个)进行通信的规则的集合

在协议的控制下, 两个对等实体间的通信是的本层能够向上一层提供服务, 要实现本层协议还需要实现下面一层所提供的服务

协议是水平的, 服务是垂直的, 上层使用下层提供的服务必须通过与下一层交换命令(服务原语)

TCP/IP协议可以为各式各样的应用提供服务, 同时TCP/IP协议也允许IP协议在各式各样的网络构成的互联网上运行

物理层
物理层在计算机内部多采用并行传输方式, 但数据在通信线路上采用串行传输

一个数据通信系统可以划分为源系统, 传输系统, 目的系统

源系统
源点, 信号源
发送器, 通常源点生成的数字比特流要通过发送器编码后才能在传输系统进行传输, 典型的发送器是调制器, 很多计算机使用内置的调制解调器
接收器, 解调器
终点, 屏幕等
信号
模拟信号, 或连续信号, 调制解调器到电话局之间的用户线
数字信号, 或离散信号, 计算机到调制解调器
信道基本概念
单向通信, 单工通信
双向交替通信, 半双工通信
双向同时通信, 全双工通信
来自信源的信号称为基带信号, 计算机输出的代表各种文字或图像文件的数据信号都属于基带信号, 基带信号中往往包含较多的低频成分, 甚至有直流成分, 因此需要对基带信号进行调制解调

调制可分为两类, 一种是仅对基带信号的波形进行变换, 使他能与信道特性相适应, 变换后的信号还是基带信号, 这类调制称为基带调制, 另一类调制需要使用载波进行调制, 把基带信号的频率范围搬移到较高的频段, bin转换为模拟信号, 进过载波的信号称为带通信号调制

常用编码方式

不归零值, 正电平为1, 负电平为0
归零制, 正脉冲为代表1, 负脉冲为0
曼彻斯特编码, 周期内向上跳的代表0, 向下跳代表1
差分曼彻斯特编码, 在每一位中心处始终有跳变, 位开始边界有跳变代表0，而位开始边界没有跳变代表1。
基本的带通调制方法

调幅(AM) 载波的振幅随基带数字信号而变化
调频(FM) 载波的频率随基带数字信号而变化
调相(PM) 载波的初始相位随基带数字信号而变化
信噪比 = 10 log 10(s/n)

香农公式: 信道的极限信息传输速率是 C = W log2(1 + s/N)(bit/s), w是信道的带宽(以hz为单位), S为信道内所传信号的平均功率, N为信道内部的高斯噪声功率

信道的带宽或信道中的信噪比越大, 信息的极限传输速率就越高, 用编码的方法让每一个码元携带更多比特的信息量

物理层下面的传输媒体
导引型媒体
双绞线
同轴电缆
光缆, 传输损耗小, 中继距离长, 抗干扰强, 保密性好, 体积轻
信道复用技术
频分复用, 时分复用和统计时分复用
频分复用是所有用户在同样的时间占用不同的带宽(频率带宽)资源
时分复用的所有用户在不同的时间占用相同的频带宽度, 时分复用则有利于数字信号的传输
波分复用是光的频分复用
码分复用: 每一个用户可以在同样的时间使用同样的频带进行通信, 由于各用户使用不同码型, 因此各用户之间不会造成干扰, 其频谱类似与白噪声, 不易被发现
宽带接入技术
ADSL技术, 非对称数字用户线, 是用数字技术对现有的模拟电话用户线进行改造, 是他能承载宽带数字业务
光纤同轴混合网(HFC网)
FTTx技术, 光纤到户技术
数据链路层
数据链路层属于计算机网络的低层

点对点通道, 这种通道使用一对一的点对点通信方式
广播信道, 这种信道使用一对多的广播通信方式
使用点对点信道的数据链路层
数据链路和帧
链路就是一个结点到相邻结点的一段物理线路(有线或无线)
数据链路是另一个概念, 在一条线路上传送数据时, 除了一条必须的物理链路外, 还需要包括必要的通信协议来控制这些数据的传输才构成了数据链路, 现在最常用的方法是使用网络适配器来实现这些协议, 一般的适配器都包括了数据链路层和物理层这两层功能
帧
数据链路层将网络层交下来的数据构成帧发送到链路上, 以及把收到的帧中的数据取出在上交到网络层, 网络层协议数据单元是IP数据报
三个基本问题
封装成帧是在一段数据的前后加上首部和尾部, 首部和尾部的一个重要作用是帧定界, 为了提高数据传输速率, 帧的数据部分长度应尽可能的大于首部和尾部的长度, 每一种链路层协议所能传送的帧的数据部分长度上线为最大传送单元MTU
透明传输, 由于帧的开始就结束的标记使用专门的控制字符, 因此所传输任何8比特组合总一定不允许和用作帧定界的控制字符比特编码相同, 在数据链路层透明传输表示无论什么样的比特组合的数据都能够原样无差错的通过数据链路层, 因此, 对于所传送的数据来说, 这些数据就看不见数据链路层有什么妨碍数据传输的东西(转义字符)
差错检测, 传输错误的比特总数站所传输比特总数的比率称为误码率, 信噪比越高误码率越小(循环冗余校验)
循环冗余检验, 帧检验序列FCS是帧检验序列, 一般使用冗余检验法是模二运算, 异或运算, 发送的FCS是M + FCS(余数)
如果帧无差错, 将每一帧都除以除数, 余数为0
凡是被接收端数据链路层接受的帧均无差错
数据链路层没有提供可靠传输服务
在CRC上加上了帧编号, 确认和重传机制, 对于质量较好的有线传输线路, 不适用确认和重传机制
点对点协议PPP
PPP协议满足的需求

简单, 只进行封装校验
封装成帧
透明性
多种网络协议
多种类型链路
差错检测
检测连接状态
最大传送单元
网络层地址协商
数据压缩协商
只支持点对点链路通信, 只支持全双工链路

协议的组成

将IP数据报封装到串行链路的方法, PPP既支持异步链路(无奇偶校验的8比特数据), 也支持面向比特的同步链路
一个用来建立配置和测试数据链路连接的链路控制协议LCP
一套网络控制协议NCP, 其中每一个协议支持不同的网络层协议
PPP协议帧格式

PPP协议帧格式
PPP协议帧格式
首部的第一个字段和尾部第二字段都是标志字段, 字段A和C没有携带帧信息,第四个字段是协议字段, 当协议字段是0x0021时, ppp帧信息字段是IP数据报, 若为0xC021是ppp链路协议的LCP数据, 0x8021是控制数据
字节填充
将信息字段中的每一个0x7E 字节转变为2字节序列(0x7D, 0x5E)
若信息中出现了一个0x7D字节, 转变为(0x7D,0x5D)
若信息字段中出现小于0x20字符, 则在字符前加入一个0x7D字节, 同时改变编码
零比特填充, 在使用SONET/SDH链路使用同步传输时, 只要发现连续5个一,则立即加入一个0
使用广播信道的数据链路层
局域网的数据链路层

网络为一个单位所有, 且地理范围和站点数目均有限

具有广播功能
便于系统的扩展和逐渐演变, 各设备的位置可灵活调整和改变
提高了系统的可靠性, 可用性, 生存性
分类,星形网, 总线网, 环形网, 总线网中以太网最为出名

以太网标准
数据链路层被拆分为两层, 逻辑链路控制层LLC, 媒体接入控制MAC

适配器作用: 进行数据串行传输和并行传输的转换

CSMA/CD, 载波监听多点接入/碰撞检测

采用无连接的方式, 尽最大努力交付, 重传也当做新的数据帧
曼彻斯特编码
载波监听是检测信道, 每个站都必须不停检测信道
碰撞检测也就是边发边听
一个站不可能同时进行发送和接收
争用期是值以太网在发送数据帧后至多经过两个时间, 又称碰撞窗口, 经过争用期还没有检测到碰撞才能肯定这次发送没有发生碰撞
以太网使用截断二进制指数退避算法, 发生碰撞后不是等待信道空闲后立即重发, 而是推迟一个最忌时间, 若连续多次发生冲突, 使用此算法可以使重传需要推迟的平均时间随重传次数二增大(动态退避)
使用集线器的星形拓扑

使用集线器的以太网逻辑上仍是总线网, 使用的还是CSMA/CD协议
一个集线器有许多接口
集线器工作在物理层, 每个接口仅简单转发比特不进行检测
以太网的MAC层

硬件地址又称MAC地址, 固化在适配器ROM中的地址

mac帧由五个字段组成, 前两段分别为6字节长的目的地址和原地址地址, 第三个字段是类型字段

扩展以太网
最初是网桥, 对收到的帧进行转发和过滤, 交换式集线器称为以太网交换机

实质是多接口网桥, 每个接口都直接与单台主机或另一个以太网交换机相连, 还具有并行性, 链接多个主机同时通信
相互通信的主机都是独占传输媒体, 无碰撞的传输数据
虚拟局域网
100BASE-T 以太网, 使用IEEE802.3CSMA/CD协议, IEE802.3u
吉比特以太网IEE802.3z
10吉比特以太网和更快地以太网IEE802.3an

网络层
##　网络层提供的两种服务
网络层向上只提供简单灵活的，无连接的尽最大努力交付的数据报服务

虚电路服务和数据报服务的对比
对比的方面 | 虚电路服务 | 数据报服务
— | — | —-
思路|可靠通信应当由网络来保证|可靠通信应该由用户主机来保证
连接的建立 | 必须有 | 不需要
终点的地址 | 仅在连接建立阶段使用, 每个分组使用短的虚电路好 | 每个端点都有终点的完整地址
分组的转发 | 属于同一虚电路的分组按照同意路由转发 | 每个分组独立选择路由进行转发
结点故障 | 均失败 | 丢失分组
分组顺序 | 按序到达 | 无序
差错控制流量控制 | 由网络或者用户主机负责 | 由用户主机负责

网际协议IP
与IP协议配套的协议还有三个协议

地址解析协议ARP, 反向的RARP逆地址解析协议
网际控制报文协议ICMP
网际组管理协议IGMP
虚电路互连网络
将网络互连起来的设备要使用一些中间设备

物理层使用的中间设备叫做转发器
数据链路层使用的中间设备叫做网桥
网络层使用的中间设备叫做路由器
在网络层以上使用的中间设备叫做网关, 用网关连接两个不兼容的系统需要在高层进行协议的转换
当中间设备是装阿奇或网桥, 这仅仅是扩大一个网络, 这仍然是一个网络, 并不是网络互连

互联网可以由多种易购网络互连组成

分类ip地址
IP地址由两个长度的字段组成, 第一个字段是网络号, 标志主机(或路由器)所连接到的网络, 一个网络号在整个互联网范围内是必须是唯一的, 第二个字段是主机号, 标志主机

A类B类C类地址的网络号字段分别为一个, 两个, 三个字节长
D类地址(前四位1110)用于多播
E类地址(前四位1111)保留以后用

A类地址网络号占一个字节,只有7位可供使用, 可使用的网络好为(2^7 - 2), 一个是全0地址, 代表网络本身. 一个是127保留作为本地软件环回测试主机间进程使用

A类地址主机号占三个字节, 每一个A类网络最大主机数为(2^24 -2): 全0的表示表示网络地址, 全1的表示网络上的所有主机

B类地址可指派的网络数为2^14 -1个, 最大主机数为2^16 - 2个

ip地址与硬件地址
物理地址是数据链路层和物理层使用的地址, IP地址是网络层和以上各层使用的地址, 是一种逻辑地址

IP地址放在IP数据报的首部, 硬件地址放在mac帧的首部, 在网络层和网络层以上使用的是ip地址, 数据链路层及一下使用的是链路地址

在ip抽象的互联网上只能看见IP数据报
路由器只根据目的站的ip地址的网络号进行路由选择
在局域网的链路层, 只能看见mac帧
隐藏细节
地址解析协议ARP
ARP是在主机ARP高速缓存中存放一个IP地址到硬件地址的映射表, 并且实时更新

广播请求分组

ip数据报格式
固定首部

版本号4位, 协议版本ipv?

首部长度4位, 表示最大十进制数值为15字节, 最常用的首部长度为20字节(即0101)

区分服务8位, 一般不使用

总长度值首部和数据数据之和的长度, 单位为字节, 总长度为16位, 数据报最大长度为2^16 - 1字节

IP协议规定, 所有的主机路由必须能够接受长度不超过576字节的数据报, 超过时需要分片

标识16位, 作为计数器, 产生一个数据报就加1, ip作为无连接服务不存在按序接收,用来重组数据报, 在分片时这个标识字段复制给所有的数据报标识字段

标志3位, 只有两位有意义

最低位字段为MF,MF=1 标识后面还有分片的数据报,MF=0 标识是若干数据报片中的最后一个
中间一位为DF, 标识不能分片, 当DF=0才允许分片
片偏移13位, 分片后在原分组的相对位置

生存时间8位, 防止无法转发的, 每经过一个路由器就把TTL减去数据报在路由器消耗的时间, 小于一就减一,现在是跳数限制

协议8位,例如ICMP

首部校验和16位, 只校验数据报的首部, 先把IP数据报首部划分为16字节的序列, 校验和字段设为0, 算数运算想加所有的, 写入到检验和字段, 接收方收到后把所有的16字节使用运算相加后取反码, 未发生变化结果为0

源地址

目的地址

划分子网和构造超网
划分子网

ip地址空间利用率不合理
给每一个物理网络分配一个网络号会使路由表变的太大, 互联网中的网络越多, 路由器中的路由表项目数越多, 也会导致路由器成本变高
两级IP地址不灵活
划分子网的思路与

一个拥有许多物理网络的单位, 可将所属的网络划分成若干子网, 划分子网是单位内部的, 单位以外的看不见, 只表现一个物理网络
从主机网络号借用若干位做子网号
子网掩码, 用来确定网络划分

把三级ip地址和收到的数据报目的地址按位与就能得出子网的网络地址
使用子网时分组的转发

路由表必须包含: 目的网络地址, 子网掩码, 下一跳地址
相与之后的结果如果不在路由表, 继续将结果再次相与
无分类编址CIDR(构造超网)

消除了传统A类等划分子网的概念
将32位IP地址分为前后两部分, 前面部分是网络前缀,后面部分指主机
使用斜线记法,IP地址后面加上斜线,然后协商网络前缀所占的位数
CIDR使用32为的地址掩码,也可称为子网掩码,斜线表示1的个数
最长前缀匹配
网际控制报文协议
允许主机或路由器报告差错

种类
ICMP差错报告报文
ICMP询问报文
统一三个字段: 类型, 代码和校验和

ICMP报文种类	类型值	ICMP报文类型
差错报告报文	3	终点不可达
–	11	时间超过
–	12	参数问题
–	5	改变路由
询问报文	8/0	回送请求或应答
–	13/14	时间戳请求或回答
应用在ping/tracerout

互联网的路由选择协议
理想的路由算法

算法完整
计算简单
适应变化
具有稳定性
公平的
最佳的
分层次路由选择协议

自治系统
内部网关协议IGP, 处在相同同的自治系统中, 如RIP和OSPF协议
外部网关EGP协议
内部网关RIP是一种分布式的基于距离向量的路由网关协议, 距离也称跳数, RIP允许一条路劲最多15个路由器, 只适用于小型互联网

仅仅和邻路由器交换信息
交换的信息是路由表
按固定时间间隔交换信息
RIP协议首部4字节, 每个路由信息20字节, 最多包含25个路由

内部网关协议OSPF

开放最短路径优先, 是分布式的链路状态协议

洪泛法向本自治系统所有路由器发送信息
发送的是与本路由器相邻的所有路由器链路状态
只有当链路状态发生变化后才向路由器发送信息
外部网关协议BGP

互联网规模太大, 自治系统之间路由选择困难
自治系统之间的路由选择必须考虑油管策略
ipv6
IPv6基本首部

更大的地址空间
扩展的地址层次结构
灵活的首部格式
允许协议的继续扩充
支持资源的预分配
首部8字节对其
IPv6的改变

取消了首部长度字段, 固定40字节
取消服务类型字段, 优先级和流标号实现了功能
取消了总长度字段改为有效载荷长度字段
取消了标识,标志, 片偏移字段, 包含在分片扩展首部
取消了协议字段, 改用下一个首部字段
取消了检验和字段
取消了选项字段, 用扩展来实现功能
首部格式

版本4位
通信量8位,区分数据报类别或优先级
流标号20位,流是互联网上从特定源点到特定终点(单播或多播)的一些了数据报(视频等), 流经过的路径上都保证指明服务质量
有效载荷长度16位, 除基本首部以外的字节数, 最大值为64kB
下一个首部8位,相当于ipv4协议字段或可选字段
跳数限制,TTL
源地址128位
目的地址128位
ipv6的地址

单播:点对点通信
多播:一点对多点的通信
任播:终点是一组计算机
IPv4到IPv6的转变

双协议栈值一部分主机装有双协议站,v4和v6,双向通信,若DNS返回的是ipv4的地址,双协议栈主机就是用v4, 在v4向v6转发的时候转换后再发, 但是有些数据没法恢复, 例如流标号
隧道技术, 在ipv6进入v4网络时, 将ipv6数据报封装为v4数据部分,整个v6数据报变成了v4数据报数据部分
ip多播
vpn和网络地址转换NAT
vpn在对路由器中的所有路由器, 对目的地址是专用地址的数据报一律不进行转发,也称专用互联网

运输层
运输层协议概述
进程之间的通信
运输层向它上面的应用层提供通信服务, 是面向通信部分的最高层, 也是用户功能的最低层

运输层为相互通信的应用进程提供了端到端的逻辑通信

IP层真正通信的实体是主机中的进程

运输层的两个主要协议
用户数据报协议UDP
传输控制协议TCP
运输层端口
运输层所有的应用进程都可以通过运输层传送到IP层,这就是复用, 运输层从IP层收到发送给各应用进程的数据够分别交付给应用进程, 这就是分用

通信的终点虽然是应用进程, 单报文交付的是目的主机端口

晕乎数据协议UDP
udp是无连接的
尽最大努力交付
UDP是面向报文的, 一次性交付一个完整的报文
没有拥塞控制
UDP支持一对一, 一对多, 多对多的交互通信
UDP首部开销小
UDP首部格式, 首部字段只有8个字节
源端口, 不需要可全为0
目的端口
长度, 最小值为8
检验和, 判断是够有误
计算校验和时, 需要在头部加上一个伪首部(源IP地址, 目的IP地址, 0, 17, UDP长度), 仅用作计算检验和

传输控制TCP
面向连接
每条连接有两个TCP
TCP提供全双工通信
面向字节流, 指流入到进程或从进程流出的字节序列
tcp的链接
TCP连接的端点是套接字,套接字是IP拼接端口

可靠传输的工作原理
TCP下面的网络提供的都是不可靠的传输, 不可靠的传输信道能够实现可靠传输

停止等待协议
停等就是每发送一个分组就停止发送等到确认

无差错情况
出现差错后重传, 设置重传等待时间
确认丢失和确认迟到
信道利用率= 发送分组时间/(发送分组时间 + RTT + 确认分组所需时间)

为了提高传输速率, 使用流水线传输

连续ARQ协议
滑动窗口协议, 每收到一个确认, 发送窗口就向前滑动一个分组位置,接受方采用累计确认的方式

TCP报文段首部格式
源端口和目的端口, 各占2个字节
序号,占四个字节, 报文段序号
确认号, 占四字节, 期望收到对方下一个报文段的第一个数据字节的序号, 确认号表示序号前的所有数据都已正确收到
数据偏移, 占4位, 指出TCP报文段的数据起始处距离TCP报文段的起始出有多远
保留文6位
控制位6位, URG=1紧急字段
ACK=1是确认号字段才有效
推送PSH=1是立即创建一个报文段发送过去, 接收方收到后立即交付
复位RST=1表示需要释放链接,然后重新建立链接
同步SYN=1而ACK=0是表示这是一个请求连接报文段, 若同意连接, 响应报文段syn=1,ACK=1
终止FIN用来释放连接
窗口站两字节
检验和占两字节, 同UDP一样都要加上伪首部, 第四个字段应改为6
紧急指针,2字节在URG=1才有效,指出本报文段中的紧急数据字节数
选项, 长度可变, 最长20字节
TCP可靠传输的实现
以字节为单位的滑动窗口
超时重传时间的选择
选择确认SACK
TCP流量控制
流量控制是让发送方的发送速率不要太快, 要让接收方来得及接收,设置持续计时器防止丢失后形成死锁

TCP拥塞控制
拥塞控制是防止过多的数据注入到网络中, 这样可以使用网络中的路由器或链路不会过载

流量控制是点对点通信量的控制, 是一个端到端的问题, 抑制发送方的数据发送速率

拥塞控制方法
慢开始, 拥塞避免, 快重传, 快恢复

慢开始和拥塞避免
基于窗口的拥塞控制, 发送方维持一个拥塞窗口的状态变量, 窗口的大小取决于网络的拥塞程度, 发送方让自己的发送窗口等于拥塞窗口

判断出现网络拥塞的依据是出现了超时

慢开始是由小到大逐渐增大拥塞窗口数值,每经过一个传输轮次就加倍

防止拥塞窗口增长过大引起拥塞,设置慢开始门限

拥塞避免算法就是让拥塞串口慢慢增大, 每经过一个往返时间RTT就加1

快重传是不等待自己发送数据是才确认,而是立即发送确认

TCP运输链接管理
三次握手
四次挥手

应用层
不同的网络应用的应用进程之间, 需要不同通信规则

域名系统DNS
域名到IP的解析是有分布在互联网的域名服务器程序完成

域名不区分大小写, 完整域名不超过255个字符

域名服务器
一个服务器所负责管辖的范围叫区, 一个区的所有节点必须是能够连通的, DNS服务器的范围不是以域作为单位, 而是区作为单位, 区小于等于域

根域名服务器是最高层次的域名服务器, 所有根域名服务器都知道所有的顶级域名服务器
顶级域名服务器, 这些域名管理所有二级域名
权限域名服务器, 一个区的域名服务器
本地域名服务器
主机向本地域名服务器的查询一般采用递归查询
本地域名服务器向根域名服务器查询使用迭代查询
维护有高速缓存
文件传送协议FTP
FTP客户与服务器建立两个连接, “控制连接”和”数据传送连接”

简单文件传送协议TFTP
每次传送512字节数据
数据报文按序编号,从1开始
支持ASCII码或二进制传送
可以对文件读写
使用简单的首部
远程终端协议TELNET
万维网WWW
统一资源定位符url
超文本传送协议HTTP
http1.1 使用的持续连接

代理服务器
请求代理服务器
若存在就返回
否则代理服务器与互联网上的源点服务器建立TCP连接,并发送http报文
源点服务器吧请求的对象放在http响应报文返回代理服务器
代理服务器收到后复制到自己本地存储器中, 在吧这个对象放在http响应报文总通过已建立的链接返回请求该对象的浏览器
http报文结构
开始行, 区分请求报文和响应报文, 在开始行的三个字段之间用空格分隔开
首部行, 说明浏览器服务器或报文主体的一些信息,每一行的结束位置都要有回车和换行, 整个首部结束时, 还要空一行隔开
实体主题
电子邮件
简单邮件传送协议SMTP, 通用互联网邮件扩充(附件),邮件读取协议pop3

连接建立250, 不可用421
邮件传送, 出错451, 452空间不够, 500命令无法识别
连接释放221
动态主机配置协议DHCP
简单网络管理协议SNMP
网络安全
被动攻击是从网络上窃听他人通信内容

主动攻击

篡改, 更改报文流
恶意程序
计算机病毒
计算机蠕虫
特洛伊木马
逻辑炸弹
后门入侵
流氓软件
拒绝服务
安全的计算机网络
保密性
端点鉴别
信息完整性
运行完全性
两类密码体制
对称密码密码体制,DES属于对称秘钥密码体制, 保密性取决于对秘钥的保密, 算法是公开的
公钥密码体制使用不同的加密秘钥和解密秘钥,基于大数分解的RSA体制
数字签名
接受者能够核实发送至对报文的签名
接受者确认收到的数据没有被篡改过
发送者不可抵赖
鉴别
报文鉴别
密码散列函数
MD5和SHA-1,SHA
报文鉴别码
运输层安全协议
安全套接字层SSL
运输层安全TLS
应用层安全协议PGP
系统安全防火墙
防火墙是一种访问控制技术,严格控制网络边界的分组禁止任何不必要的通信