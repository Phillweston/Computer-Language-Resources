---
title: day9-架构初探-谁动了我的蛋糕
date: 2022-07-16 15:32:24
tags: 
- Go学习路线
- 字节跳动青训营
---

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220716154814.jpg)

这是我参与「第三届青训营 -后端场」笔记创作活动的的第9篇笔记。

## 「架构初探-谁动了我的蛋糕」 第三届字节跳动青训营 - 后端专场

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220716154511.png)

同时这也是课表的第9天课程《架构初探-谁动了我的蛋糕》。PC端阅读效果更佳，点击文末：**阅读原文**即可。

# 课前预习

**什么是架构？**

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717210827.png)

📌 一些小问题：

- 如何给架构下定义？
- 架构的重要性？
- 架构演进的初衷？
- 架构演进的思路？

**企业级后端架构剖析**

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717211509.png)

### 企业级后端架构的挑战

- 离线任务

- 在线任务

- IO 密集型

- CPU 密集型

- 服务治理

- IPC (Inter-Process Communication)

- RPC (Remote Procedure Call)

### 后端架构实战

- 负载均衡 Load Balancing

- 服务发现 Service Discovery

- 服务注册 Service Registry

- 宿主机 Host

- 容器 Container

- 时序数据 Time Series

- 一致性哈希 Consistent Hash

### 课前思考题

1. 软件架构演进至今都有哪些形态？它们分别解决了什么问题？仍然存在什么问题？
2. 云计算有哪些基础技术？云计算服务的形态又有哪些？
3. 云原生是什么？它跟云计算的关系是？
4. 云原生的代表技术有哪些？
5. 企业级后端架构面临的挑战有哪些？

#### 架构定义

**Q：如何给架构下定义？**

A：架构，又称软件架构：

1. 是有关软件整体结构与组件的抽象描述
2. 用于指导软件系统各个方面的设计

**Q：架构的重要性？**

A：那盖房子来做举例子。

我们都知道，地基对于一栋楼房的主要性，架构对于一个软件的重要性也是类似的：

1. 架构没设计好，软件容易崩，用户体验上不去。最终要么重构，要么放弃
2. 架构设计好了，软件的稳定性上去了，用户体验高了，口碑一点点就打造出来了
3. 良好的架构基础，也为软件的未来发展提供了更多的可能。为用户赋能，实现自身价值

#### 单机架构

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717213039.png)



#### 单体架构

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717213057.png)

#### 垂直架构

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717213148.png)

### SOA (面向服务架构)

![SOA (面向服务架构)](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717213205.png)

#### 微服务加架构

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717213238.png)

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717213308.png)

### 企业级后端架构剖析

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717220040.png)

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717220102.png)

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717220117.png)

在云原生的大背景下，不论是计算资源还是存储资源，他们都像是服务一样供用户使用。

### 微服务架构

微服务架构下，服务之间的通讯标准是基于协议而不是 ESB 的。

- **HTTP** - H1/H2

- **RPC** - Apache Thrift/gRPC

如何在 HTTP 和 RPC 之间选择？

- **性能** - RPC 协议往往具备较好的压缩率，性能较高。如 Thrift, Protocol Buffers

- **服务治理** - RPC 中间件往往集成了丰富的服务治理能力。如 **熔断、降级、超时**等

- **可解释性** - HTTP 通信的协议往往首选 JSON，可解释性、可调试性更好

### 服务网格

什么是服务网格？

- 微服务之间通讯的中间层

- 一个高性能的 4 层网络代理

- 将流量层面的逻辑与业务进程解耦

没有什么是加一层代理解决不了的问题，服务网格相比较于 RPC/HTTP 框架：

- 实现了异构系统治理体验的统一化

- 服务网格的数据平面代理与业务进程采取进程间通信的模式，使得流量相关的逻辑（包含治理）与业务进程解耦，生命周期也更容易管理

### 企业级后端架构的挑战

#### 挑战

- 基础设施层面：
   Q：我们总说，云是弹性的，也就是说，在用户的角度，云提供的资源是无限的。然而，云背后的物理资源是有限的。在企业级后端架构里，云如何解决近乎无限的弹性资源和有限的物理资源之间的矛盾？

  Q：闲事的资源就这么空着呢？如何提高资源利用率，提高物理资源的价值转换率？

- 用户层面：
   Q：上了云原生微服务后，服务之间的通信开销较大，应该如何做成本优化？

  Q：微服务看起来没有那么美好，抖动导致的运维成本较高，如何解决？

  Q：异构的物理环境应该对用户是透明的，如何屏蔽这些细节？

#### 离在线资源并池

考虑到在线业务的**潮汐性**，物理资源的用量不是一成不变的。离在线资源并池，可以：

- 提高物理资源利用率

- 提供更多的弹性资源

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717221720.webp)

#### 微服务亲合性部署

微服务之间的通信成本较高，是否可以：

- 形态上是微服务架构

- 通信上是单体架构

亲合性部署，通过将微服务调用形态与资源调度系统结合，将一些调用关系紧密、通信量大的服务部署在同一个机器上，并且使用 IPC 代替 RPC 的方式，降低网络通信带来的开销

#### 流量治理

Q：微服务之间的通信流量为什么需要治理？

Q：都有哪些常用的治理手段？

Q：微服务中心件和服务网格在其中扮演着怎样的角色？

#### 屏蔽异构环境的算力差异

Q：基础设施层往往是个复杂的异构环境，比如，有些机器的 CPU 是英特尔的，而有些是 AMD 的。就算是同一个品牌，也可能是不同代际。如何将这些差异屏蔽掉，使用户尽可能不感知呢？

Q：什么情况下，我们觉得，服务需要扩容了？异构环境会对这个评判标准产生怎样的影响？

### 后端架构实战

> 问题：如何设计一个根据主机层面的资源信息，实时进行流量调度的系统，打平不同宿主机异构环境的算力差异。

关键点：

- 紧急回滚能力

- 大规模

- 极端场景

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717221922.webp)

## 最后-尾声

1. 没有最好的架构，只有最合适的架构

2. 做架构设计
   - 先从需求出发。要满足什么样的需求？预期规模有多大？
   - 做足够的业界调研。业界对于类似的需求是怎么做的？有无成熟的方案可以借鉴？直接拿来用有什么问题？
   - 技术选型。涉及的技术组件是自研，还是使用开源的？
   - 异常情况。任何时候，都不能做『输入合法』的假设。容灾能力一定要有

3. 学好架构，是工程师成长的一个重要标志

---

# 正式课程笔记

### 本章目录

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220716154424.png)

## 01 什么是架构

架构，又称软件架构

- 是有关软件整体结构与组件的抽象描述；用于指导软件系统各个方面的设计

**Q：定义还是太抽象，能不能再通俗点?**

- 实现一个软件有很多种方法，架构在方法选择上起着至关重要的指导作用

**Q：架构的重要性?**

- 地基没打好，大厦容易倒
- 地基坚实了，大厦才能盖得高
- 站在巨人肩膀上，才能看得远

比如这个房子：![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717222628.png)

## 1.1 什么是架构-问题

兰师傅蛋糕坊要开张了，亟须解决如下问题:

| 如何做蛋糕                 | 如何卖蛋糕                     |
| -------------------------- | ------------------------------ |
| 独家秘方，还是亲自做比较好 | 刚开始客流量应该不大，边做边卖 |

看起来问题都解决了，开张！

## 1.2 什么是架构-单机

软件系统需要具备对外提供服务，单机，就是把所有功能都实现在一个进程里，并部署在一台机器上

优点：简单

问题：

 C10K problem，也即单机处理 10k 个并发连接的问题。随着 epoll、kqueue 等技术的不断发展，高性能网络编程逐渐回答了 C10K 问题。但在互联网飞速发展的今天，我们正陆续面临 C10M、C10B 等问题。也就是说，单体服务一定是有架构瓶颈的。

回到兰师傅蛋糕店，仅靠兰师傅自己卖蛋糕，就算再怎么磨练手速，每天能卖出去的量也是有上限的。 **运维需要停服。**任何运维操作都需要停服，因为只有一个单体服务，有用户使用的时间点没有办法运维。再看我们的蛋糕店，如果兰师傅去上厕所了。。。 单机服务的模式，除了简单之外没有任何优点。当今互联网时代，单机服务的形态一般只适合出现在预研或初创阶段，但凡业务有发展和迭代的诉求，就应该快速做架构迭代。

演进：如何卖更多的蛋糕?

多雇几个蛋糕师傅![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717223046.png)



## 1.3 什么是架构-单体、垂直应用|垂直切分

单体架构：分布式部署
垂直应用架构：按应用垂直切分的
单体
优点：

1. 水平扩容
2. 运维不需要停服

问题:

1. 职责太多，开发效率不高
2. 爆炸半径大

演进：如何提高做蛋糕效率? **分工协作**

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717232602.png)

按照这个思路： 我们把进程部署在多个机器上，并引入**负载均衡**层，经过这样的垂直切分，就来到了**单体架构**。多个机器就好比把蛋糕切成几大块，负载均衡层负责引导用户去事先切好的几块蛋糕处。

在单体架构基础上，进一步地，再把不同应用的代码从之前一个大的进程中拆分出来，就来到了垂直应用架构。按应用拆分进程，就好比慕斯、戚风等蛋糕在不同的点发配 。

这种经过垂直切分的架构，尝试解决了单机服务的水平扩容、运维停服问题。当然这里面很多细节还没有提及，比如，**多个机器上部署的进程如何保证数据一致性**。虽然它们解决了单机服务的两个最重要的问题，但也面临着很多挑战。

这其中，有两个问题使得我们不得不放弃单体和垂直应用架构： 随着业务场景越来越复杂，服务的职责也越来越多。学过面向对象程序设计的同学都知道**单一职责的重要性**，在软件架构里也是一样的。开发者不仅要关心 Web 后端业务逻辑，还要关心缓存、持久化存储，甚至跟机器打交道。长此以往，RD 很难分出精力专注于业务能力的开发。业务发展需要上线、变更，将会影响所有其他不涉及的场景。一旦出问题，影响面不可估量。既然可以根据应用把架构做垂直拆分，那是否可以根据模块/职责对架构进行水平拆分呢？

## 1.4 什么是架构SOA 微服务|水平切分 

**SOA** (Service-Oriented Architecture)

1. 将应用的不同功能单元抽象为服务
2. 定义服务之间的通信标准

微服务架构：SOA的去中心化演进方向

问题:

- 数据一致性
  - 装货台共交付了多少蛋糕?
- 高可用
  - 这么多师傅，如何合作?
- 治理
  - 烤箱坏了，怎么容灾?
- 解耦 Vs 过微
  - 运维成本高了，值当么?

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220717233145.png)

我们把原本包含了众多复杂逻辑的进程按照功能单元抽象成多个服务，以服务为一等公民，并为它们之间的通信定义标准，便得到了 SOA 架构。 这里有两个相对比较重要的概念： 

1. 服务，是根据功能抽象出来的概念。比如说，处理用户登录信息的 Passport 服务，负责持久化存储的数据库服务，以及为了加快查询速度的缓存服务等 

2. 通信标准，是服务之间通信的基石。没有实现定义好的通信标准，就好比多个做蛋糕的师傅语言不通，难以协作 为了服务之间更好的通信，有两个大的发展方向：中心化和去中心化。

去中心化的方向，最终的形态就是微服务架构这下， 

1. 不同模块的 RD 可以专心于自己的业务逻辑了，开发迭代效率得到显著提高 

2. 各个服务独立运维，变更操作的影响面可控，应用整体的稳定性得到了提高 

3. 最后，我们还需要回答垂直切分和水平切分所产生的一系列问题： 

   - 由单机部署演进来的分布式架构，如何解决数据一致性?

   - 服务越来越多，依赖越来越复杂，如何做到高可用？
   - 一个团队甚至一个人可能同时管理多个微服务，如何运维？
   - 微服务的目标是强化单一职责，控制爆炸半径，如何在解耦和『过微』之间取舍？

## 02 企业级后端架构剖析

**背景**

兰师傅蛋糕店经过3年的蓬勃发展，积累了良好的口碑和用户基础，接下来，需要扩大规模:

- 店面怎么盘？
  - 买
  - 租

- 师傅怎么招？
  - 兰师傅全家出马
  - 招培训班出身的
- 是否继续坚持纯手工制作?
- 规模大了之后，工作重心应该是？
  - 精进蛋糕制作收益
  - 蛋糕店重点方向梳理&未来规划

## 2.1 企业级后端架构剖析-云计算

**云计算**：是指通过软件自动化管理，提供计算资源的服务网络，是现代互联网大规模熟悉分析和存储的基石。

**虚拟化技术**：硬件（虚拟机）、操作系统（容器）、网络 

**编排方案**：虚拟机编排方案（OpenStack）、容器编排方案（Kubernetes）

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718111950.png)

## 2.2 企业级后端架构剖析-云原生

**云原生**技术为组织(公司)在公有云、自由云、混合云等新型的动态环境中，构建和运行可弹性拓展的应用提供了可能。

云原生代表技术有： **容器化、服务网格、微服务、不可变基础架构、声明式API** 

基于这些技术，开发者可以构建出容错性好、易于管理、具备较好观测性的云服务。结合可靠的自动化机制，服务可以轻松应对频繁和可预测的重大变更。 

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718113934.png)

云原生主要涉及四个大方面： 

1. 弹性资源：基于虚拟化容器以及灵活的编排调度机制，可以为云服务提供快速扩缩容能力，而且极大程度地提高了物理资源的利用率。代表性的**kubernetes** 技术已经称为了业界的标准 
2. 微服务架构：微服务架构也是云原生的重要基石之一。依托于功能单元解构，使得云服务具备了快速迭代的可能，业务得以迅速发展；统一的通信标准能够帮助越来越多的组件加入到云原生的大家庭，同时也使得各组件之间的交互变的更容易。
3. DevOps：设计->开发->测试->交付->开发->测试->交付，自动化的流程使得软件的工作流程更高效，将微服务架构的优势发挥的淋漓尽致。
4. 服务网格：微服务架构是将庞大的单体服务按照业务功能解耦开来，那么，服务网格就是将业务逻辑与网络通信和治理解耦开来。业务不再需要关心异构系统中 RPC 中间件治理能力的不统一，也使得复杂的治理能力的落地成为可能。

### 2.2.1 企业级后端架构剖析-云原生之弹性计算资源

弹性计算资源类型：

- 服务资源调度
  - 微服务：和面、雕花
  - 大服务：烤箱

- 计算资源调度
  - 在线：热销榜单
  - 离线：热销榜单更新

- 消息队列
  - 在线：削峰、解耦
  - 离线：大数据分析

- 经典

  - 对象：宣传视频

  - 大数据：用户消费记录

- 关系型数据库

  - 收银记录

- 元数据

  - 服务发现：蛋糕店通讯录

- NoSQL

  - KV：来个xx蛋糕

**总结：将存储资源当成服务一样**

### 2.2.3 企业级后端架构剖析-云原生之DevOps

**DevOps**是云原生时代软件交付的利器，贯穿整个软件开发周期。

结合自动化流程，提高软件开发、交付效率。

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718114731.png)

### 2. 2.4 企业级后端架构剖析-云原生之微服务架构

通信标准:

- HTTP (RESTful API)
- RPC (Thr ift,gRPC)

微服务中间件RPC vs HTTP:

- 性能
- 服务治理
- 协议可解释性

云原生场景下，微服务大可不必在业务逻辑中实现符合通信标准的交互逻辑，而是交给框架来做。

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718121601.png)

### 2.2.5 企业级后端架构剖析-云原生之服务网格

服务网格(Service Mesh) :

- 微服务之间通讯的中间层
- 高性能网络代理
- 业务代码与治理解耦

相比较于 RPC/HTTP 框架:

- 异构系统治理统一化
- 与业务进程解耦，生命周期易管理。

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718122207.png)

**02 企业级后端架构剖析-云原生蛋糕店**

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718122309.png)

## 03 企业级后端架构的挑战

## 03 企业级后端架构的挑战-问题

挑战：

- 基础设施层面
  - 物理资源是有限的
    - 机器
    - 带宽
  - 资源利用率受制于部署服务

- 用户层面
  - 网络通信开销较大
  - 网络抖动导致运维成本提高
  - 异构环境下，不同实例资源水位不均

## 3.1 企业级后端架构的挑战-离在线资源并池

核心收益：

- 降低物理资源成本
- 提供更多的弹性资源，增加收入

解决思路：**离在线资源并池**

**在线业务**的特点

- IO密集型为主
- 潮汐性、实时性

**离线业务**的特点

- 计算密集型占多数
- 非实时性

**问题：同一个机器怎么做离在线隔离?**

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718122849.png)

## 3.2 企业级后端架构的挑战-自动扩缩容

核心收益：降低业务成本

解决思路:

- **自动扩缩容**
- 利用在线业务潮汐性自动扩缩容

问题：扩缩容依据什么指标?

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718123137.png)



## 3. 3 企业级后端架构的挑战-微服务亲合性部暑

核心收益：

- 降低业务成本
- 提高服务可用性

解决思路：**微服务亲合性部署**

- 将满足亲合性条件的容器调度到一台宿主机
- 微服务中间件与服务网格通过共享内存通信
- 服务网格控制面实施灵活、动态的流量调度

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718123349.png)

## 3.4 企业级后端架构的挑战-流量治理

核心收益：

- 提高微服务调用容错性
- 容灾
- 进一步提高开发效率，Dev0ps 发挥到极致

解决思路：基于微服务中间件&服务网格的流量治理

- 熔断、重试
- 单元化
- 复杂环境(功能、预览)的流量调度

## 3.5 企业级后端架构的挑战-CPU水位负载均衡

核心收益:

- 打平异构环境算力差异
- 为自动扩缩容提供正向输入

解决思路：CPU水位负载均衡

- laaS

- 提供资源探针

服务网格：动态负载均衡

## 04 后端架构实战
## 04 后端架构实战-问题背景

兰师傅蛋糕店也碰到了类似的问题:

- 不同师傅干活的效率差距较大
- 有些师傅希望：能者多劳多挣

在这个背景下，继续像之前一样为每个师傅分配完全相同的工作，会引起他们的不满。。。

回到03最后的挑战：**CPU水位负载均衡，应该如何设计?**

1. 需要哪些输入?
2. 设计时需要考虑哪些关键点?

## 04 后端架构实战-问题提炼

输入:

- 服务网格数据面：支持带权重的负载均衡策略

- 注册中心存储了所有容器的权重信息
- 宿主机能提供
  - 容器的资源使用情况
  - 物理资源信息(如CPU型号)

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718124356.png)

## 4.1 后端架构实战-自适应静态权重
方案：

- 采集宿主机物理资源信息
- 调整容器注册的权重

优势: 

- 复杂度低
- 完全分布式，可用性高
- 微服务中间件无适配成本

缺点:

- 无紧急回滚能力
- 缺乏运行时自适应能力

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718124536.png)

## 4.2 自适应动态权重 Alpha

方案：

- 容器动态权重的自适应调整
- 服务网格的服务发现&流量调度能力

演进方向:

- 解决无法紧急回滚的问题
- 运行时权重自适应

缺点：过度流量倾斜可能会有异常情况

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718132353.png)

## 4.3 自适应动态权重 Beta

方案：服务网格上报RPC指标
演进方向：极端场景的处理成为可能

缺点：

- 时序数据库压力较大

- 动态权重决策中心职责越来越多，迭代->变更->风险

  ![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718132841.png)

## 4.4 自适应动态权重Release

演进方向：

- 微服务化
- 引入消息队列削峰、解耦
- 离在线链路切分
- 梳理强弱依赖

![](https://nateshao-blog.oss-cn-shenzhen.aliyuncs.com/img/20220718132931.png)

解决在线分析引擎的数据一致性问题：**一致性哈希** 

解决时序数据库压力：将其作为旁路工具，采用纯内存的在线分析引擎进行实时策略计算 

离线分析：使用消息队列解耦、削峰，离线回馈在线



参考文献

1. 青训营官方账号：https://juejin.cn/post/7098182433941651492
1. C10K 问题：https://landscape.cncf.io/?selected=portus
1. CNCF：https://www.cncf.io/
1. CNCF landscape：https://landscape.cncf.io/

