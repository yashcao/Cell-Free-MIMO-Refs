# Cell-Free-MIMO-Refs

## Cell-Free MIMO 学习交流资料





# Basis of CF-MIMO

## CF 背景
- 关于6G不得不说的事: 虽然目前还远远没有达到6G定义的统一阶段，但是综合各国专家的研究进展，可以预见未来6G将主要从以下3个维度采取变革性技术:
  - 去蜂窝（CF）网络架构
  - 太赫兹技术
  - 人工智能技术
  
- 关于cell不得不说的事：蜂窝网络架构是美国**贝尔**实验室在**20世纪70年代**提出的跨时代概念。它通过`频率复用`和`小区分裂`技术**提高频谱资源的利用率**，支撑移动通信快速发展。然而随着蜂窝小区面积不断缩小（比如微小区和超密集部署），`小区间干扰`和`频繁越区切换`等问题愈发严重导致系统性能提升遭遇瓶颈。为了解决这些瓶颈问题，对蜂窝网络架构进行彻底变革的去蜂窝网络架构成为人们关注的可行技术方案之一。

- 关于CF不得不提的概念：
  - 蜂窝通信：由于频谱资源有限，蜂窝通信采用频率复用的方式实现有限频谱资源对无限区域的覆盖。**多小区的频率复用，每个小区采用一组频带。因此，使用相同频段的小区之间必然存在同频干扰。**
  - MIMO的核心思想是在`同一时频资源`下，利用空间自由度，部署具有大型天线阵列的基站，同时为多个用户终端服务。然而，多天线同时放置在一起可能会导致`信道内的相关性`。为了应对这一重大的实现挑战，提出了 DAS。
  - 分布式天线系统（DAS）：蜂窝小区内多个基站地理位置上分离，通过高性能的回程链路进行协作对多个用户同时进行传输。
  - 多点协同传输（CoMP）：本质上是协同的DAS。
  - 网络 MIMO：又称为`虚拟 MIMO`、`分布式 MIMO`。文献 `Cooperative multicell precoding: Rate region characterization and distributed strategies with instantaneous and statistical CSI` 介绍的模型。分布式基站协作的情况，其中每个基站只有本地CSI。通过协同基站在回程链路上共享重要数据，并联合下行传输给预定用户来实现干扰消除。CF系统与其类似。
  - CF：与CoMP设置相同，但没有`小区边界`的概念。（思考：小区边界意味着蜂窝通信的`频率复用`以及`小区间干扰`等特点存在。）上述的系统都存在**簇间干扰与交互开销**的问题。
  - Cell-free massive MIMO is a recent concept that conveniently combines elements from 
    - small cells
    - **TDD massive MIMO**
    - **user-centric** joint transmission coordinated multi-point (JT-CoMP)
  - > 因此，可以说 CF 就是大区域扩展的JT-CoMP，学术大佬也这样说：CF就是 **user-centric** JT-CoMP！



## 一些回答

> Cell-free MIMO is a new name for network MIMO and distributed MIMO. One purpose for the renaming is to impose new assumptions on how the system should operate to be practically implementable. You can think of it as Network MIMO 2.0.

- https://www.researchgate.net/post/How_cell-free_CF_network_is_different_from_multi-access_MA_network
- https://www.researchgate.net/post/Could-anyone-can-explain-what-differences-between-C-RAN-and-cell-free-MIMO
- https://www.researchgate.net/post/Is-there-any-difference-between-Network-MIMO-Cooperative-MIMO-and-Cell-Free-MIMO-Full-BS-Cooperation-system

## 推荐文献
- Distributed Precoding Design for Cell-Free Massive MIMO Systems
- Cell Free Massive MIMO with Limited Capacity Fronthaul

-------------------

## 关于 "Channel hardening in massive MIMO"
  - **信道「硬化」**：理论上讲，当m-MIMO发射天线足够多（趋于无穷）时，`随机矩阵理论`的一些特性可以得到应用，比如如果天线数目足够（趋于无穷），`信道参数将会从原有的具有随机性变为逐渐变为确定性`，信道的`相干时间`也可能会随之延长，`快衰落（快时间）的影响会逐渐变小`，这里我们称之为信道「硬化」。这种特性可以保证基站侧使用简单的线性预编码来替代复杂的非线性预编码和实时预编码，但是目前信道硬化理论受限于实际中的m-MIMO天线阵子数不够多和模拟器件的非理想性问题，无法得到广泛应用。
  - 大规模/超大规模天线是配置有多达数百根天线的增强型多天线技术，它的出现是为了满足未来无线通信网络对于巨流量、巨连接的需求，能够大幅度提高系统容量和可靠性。大规模/超大规模天线`信道特性`主要包括`空间非平稳`、`信道硬化`与`球面波`特性。
    - 某些特定的簇不能被整个阵列天线都观察到（簇在阵列轴上是非平稳的），在阵列轴上将观察到簇的消失和出现。此外，在整个阵列上也将观察到功率的不平衡以及莱斯因子的变化，不同的天线单元之间的功率、时延参数也将发生漂移。
    - 信道硬化是指由于窄波束和大规模/超大规模天线阵列的应用，导致信道波动下降，`用户之间的正交性越来越强`。
    - 由于大规模/超大规模天线的应用，收发天线距离可能在瑞利距离以内，从而表现出球面波前。
    
  - 总结：信道矩阵的奇异值的分布对于信道矩阵元素的实际分布变得越来越不敏感（只要保持独立同分布便可）。这就会导致 `Marcenko-Pastur定律`。
  $$\mathbf{H}\mathbf{H}^{H} = \mathbf{U} \mathbf{\Sigma}\mathbf{U}^{H}, \quad \mathbf{\Sigma}=\text{diag}(\lambda_1, \cdots, \lambda_N)$$
  - CF 关切点：由于大规模天线阵列具有信道硬化特性，平均了信道的小尺度衰落，现有研究多是假设在大尺度衰落已知条件下进行功率优化等信号处理问题，然而无小区大规模天线阵列由于接入点装配天线数目较少，相比于集中式大规模天线阵列信道硬化现象并不显著。因此在大尺度衰落未知条件下的信号处理是目前无小区大规模天线阵列结构中需要研究的问题之一。

-----------

## 参考资料
- Refs:

  - https://ma-mimo.ellintech.se/?s=cell-free
  - https://www.youtube.com/watch?v=ZepQAw21HfA
  - https://cell-free.blogspot.com/p/source-codes.html
  - https://dblp.org/search?q=cell-free%20MIMO
  - https://dblp.org/search?q=cell-free%20communications

- github codes refs:
  - https://github.com/emilbjornson
  - https://github.com/hienquocngo
  - https://github.com/DinhNguyenCherry
  - https://cell-free.blogspot.com/p/source-codes.html






