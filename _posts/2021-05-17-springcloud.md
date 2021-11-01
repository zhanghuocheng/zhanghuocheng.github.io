---
layout: page
---
springcloud

### 注册中心 和zk的区别

```
CAP理论的核心
1.一个分布式系统不可能同时很好的满足一致性，可用性和分区容错性这三个需求
2.根据CAP原理,将NoSQL数据库分成了满足CA原则，满足CP原则和满足AP原则三大类:
①CA:单点集群，满足一致性，可用性的系统，通常可扩展性较差
②CP:满足一致性,分区容错性的系统，通常性能不是特别高
③AP:满足可用性,分区容错性的系统，通常可能对一致性要求低一些
作为服务注册中心，Eureka比Zookeeper好在哪里?
著名的CAP理论指出，一个分布式系统不可能同时满足C (一致性)、A (可用性)、P (容错性)。由于分区容错性P在分布式系统中是必须要保证的，因此我们只能在A和C之间进行权衡。
Zookeeper保证的是CP;Eureka保证的是AP;

Zookeeper保证的是CP
当向注册中心查询服务列表时，我们可以容忍注册中心返回的是几分钟以前的注册信息，但不能接受服务直接down掉不可用。也就是说，服务注册功能对可用性的要求要高于一致性。但是zk会出现这样一种情况，当master节点因为网络故障与其他节点失去联系时,剩余节点会重新进行leader选举。问题在于，选举leader的时间太长,30~120s，且选举期间整个zk集群都是不可用的，这就导致在选举期间注册服务瘫痪。在云部署的环境下，因为网络问题使得zk集群失去master’节点是较大概率会发生的事件，虽然服务最终能够恢复，但是漫长的选举时间导致的注册长期不可用是不能容忍的。

Eureka保证的是AP
Eureka看明白了这一点, 因此在设计时就优先保证可用性。Eureka各个节点都是平等的，几个节点挂掉不会影响正常节点的工作，剩余的节点依然可以提供注册和查询服务。而Eureka的客户端在向某个Eureka注册时，如果发现连接失败，则会自动切换至其他节点，只要有一台Eureka还在, 就能保住注册服务的可用性,只不过查到的信息可能不是最新的，除此之外，Eureka还有一种自我保护机制，如果在15分钟内超过85%的节点都没有正常的心跳，那么Eureka就认为客户端与注册中心出现了网络故障，此时会出现以下几种情况:
1.Eureka不再从注册列表中移除因为长时间没收到心跳而应该过期的服务
2.Eureka仍然能够接受新服务的注册和查询请求，但是不会被同步到其他节点上(即保证当前节点依然可用)
3.当网络稳定时，当前实例新的注册信息会被同步到其他节点中
因此,Eureka可以很好的应对因网络故障导致部分节点失去联系的情况，而不会像Zookeeper那样使整个注册服务瘫痪

```

### Eureka注册中心的原理 数据结构

ConcurrentHashMap<String, Map<String, Lease<InstanceInfo>>> registry = new ConcurrentHashMap<String, Map<String, Lease<InstanceInfo>>>();

```
数据结构
服务存储的数据结构可以简单的理解为是一个两层的HashMap结构（为了保证线程安全使用的ConcurrentHashMap），具体的我们可以查看源码中的AbstractInstanceRegistry类：

private final ConcurrentHashMap<String, Map<String, Lease<InstanceInfo>>> registry = new ConcurrentHashMap<String, Map<String, Lease<InstanceInfo>>>();
第一层ConcurrentHashMap的key=spring.application.name，也就是应用名称，value为ConcurrentHashMap。

第二层ConcurrentHashMap的key=instanceId，也就是服务的唯一实例id，value为Lease对象，也就是具体的服务。Lease其实就是对InstanceInfo的包装，里面保存了实例信息、服务注册的时间等。具体的我们可以查看InstanceInfo源码。
```





### Eureka原理

```
两个组件：Eureka Server和Eureka Client。
Eureka Server 组建功能：注册、发现和心跳检测
client 是用轮训算法 

Server 端心跳周期30秒。90秒移除
自我保护机制：统计15分钟内的  心跳请求成功率低于85% 则认为是自身网络问题。则不会剔除服务
```





## Hystri

，命令模式实现熔断器

怎么看线程的等待时间：

```
1 命令模式
2 信号量
3 线程池隔离
4 熔断  打开 关闭 半开
```



设置线程池的个数

```
1. 如果是CPU密集型应用，则**线程池**大小设置为N+1 （N为CPU总核**数**）
2. 如果是IO密集型应用，则**线程池**大小设置为2N+1 （N为CPU总核**数**）
```

