# 设计目标

本文概括 SkyWalking 项目的核心设计目标。

- **保持可观测性**. 不管目标系统如何部署, SkyWalking 总要提供一种方案或集成方式来保持对目标系统的观测, 基于此, SkyWalking 提供了数种运行时探针。

- **拓扑结构, 性能指标和追踪一体化**. 理解分布式系统的第一步是通过观察其拓扑结构图. 拓扑图可以将复杂的系统在一张简单的图里面进行可视化展现. 基于拓扑图，运维支撑系统相关人员需要更多关于服务/实例/端点/调用的性能指标. 链路追踪(trace)作为详细的日志, 对于此种性能指标来说很有意义, 如你想知道什么时候端点延时变得很长, 想了解最慢的链路并找出原因. 因此你可以看到, 这些需求都是从大局到细节的, 都缺一不可. SkyWalking 集成并提供了一系列特性来使得这些需求成为可能, 并且使之易于理解.

- **轻量级**. 有两个方面需要保持轻量级. (1) 探针, 我们通常依赖于网络传输框架, 如 gRPC. 在这种情况下, 探针就应该尽可能小, 防止依赖库冲突以及虚拟机的负载压力(例如 JVM 永久代内存占用压力). (2) 作为一个观测平台, 在你的整个项目环境中只是次要系统, 因此我们使用自己的轻量级框架来构建后端核心服务. 所以你不需要部署并维护大数据相关的平台, SkyWalking 在技术栈方面应该足够简单。

- **可插拔**. SkyWalking 核心团队提供了许多默认实现, 但这肯定是不够的, 也不可能适用于每一种场景, 因此我们提供了大量的特性来支持可插拔功能。

- **可移植**.  SkyWalking 可以运行在多种环境下, 包括:
(1) 使用传统的注册中心, 如 [Eureka](https://github.com/spring-cloud/spring-cloud-netflix)
(2) 使用包含服务发现的RPC框架，如Spring Cloud, Apache Dubbo
(3) 在现代基础设施中使用服务网
(4) 使用云服务
(5) 跨云部署

在所有这些情况下，SkyWalking 应该运行良好

- **可互操作**. 可观测性是一个庞大的领域, 即使有强大的社区, SkyWalking 不可能支持所有方方面面, 因此 SkyWalking 支持与其他运维支撑系统进行互操作, 主要是探针, 如 Zipkin, Jaeger, OpenTracing 和 OpenCensus. SkyWalking 接收并理解他们的数据格式, 这对于终端用户来说是非常有用的, 因为不需要他们更换已有的库。

## 下一步

- 查看 [探针简介](probe-introduction.md) 理解 SkyWalking 的探针组成.
- 从 [后端概览](backend-overview.md), 你可以理解平台后端接收到探针数据之后做了什么.
- 如果你想自定义用户界面, 请从 [用户界面概览](ui-overview.md) 开始入手.