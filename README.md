# go-stress-testing
go 实现的压测工具 一句话简介




## 目录
- [1、项目说明](#1项目说明)
    - [1.1 go-stress-testing](#11-go-stress-testing)
    - [1.2 项目使用](#12-项目使用)
- [2、介绍go-stress-testing](#2介绍go-stress-testing)
- [3、压测](#3压测)
    - [3.1 压测是什么](#31-压测是什么)
    - [3.2 为什么要压测](#32-为什么要压测)
    - [3.3 压测名词解释](#33-压测名词解释)
- [4、压测工具](#4压测工具)
    - [4.1 ab](#41-ab)
    - [4.2 locust](#42-locust)
    - [4.3 Jmeter](#43-Jmeter)
    - [4.4 网络压测工具](#44-网络压测工具)
    - [4.5 比较](#45-比较)


## 1、项目说明
### 1.1 go-stress-testing
### 1.2 项目使用

## 2、介绍go-stress-testing

## 3、压测
### 3.1 压测是什么
### 3.2 为什么要压测
### 3.3 压测名词解释


## 4、压测工具
### 4.1 ab
### 4.2 locust
### 4.3 Jmeter
### 4.4 网络压测工具
### 4.5 比较





过程
先写代码 优化 书写文档 优化文档 绘制图标 发布

## 压测名词解释

- 压测名词解释

| 压测名词 |   解释  |
| :----:   | :---- |
| 并发(Concurrency)     |  指一个处理器同时处理多个任务的能力(逻辑上处理的能力)     |
| 并行(Parallel)        |  多个处理器或者是多核的处理器同时处理多个不同的任务(物理上同时执行)     |
| QPS(每秒钟查询数量 Query Per Second) | 服务器每秒钟处理请求数量 (req/sec  请求数/秒  一段时间内总请求数/请求时间)    |
| 事务(Transactions) | 是用户一次或者是几次请求的集合    |
| TPS(每秒钟处理事务数量 Transaction Per Second) | 服务器每秒钟处理事务数量(一个事务可能包括多个请求)    |
| 请求成功数(Request Success Number) | 在一次压测中，请求成功的数量    |
| 请求失败数(Request Failures Number) | 在一次压测中，请求失败的数量    |
| 错误率(Error Rate) | 在压测中，请求成功的数量与请求失败数量的比率  |
| 最大响应时间(Max Response Time) | 在一次事务中，从发出请求或指令系统做出的反映(响应)的最大时间  |
| 最少响应时间(Mininum Response Time) | 在一次事务中，从发出请求或指令系统做出的反映(响应)的最少时间  |
| 平均响应时间(Average Response Time) | 在一次事务中，从发出请求或指令系统做出的反映(响应)的平均时间  |

- 压测类型解释

| 压测类型 |   解释  |
| :----:   | :---- |
| 压力测试(Stress Testing)          |  也称之为强度测试，测试一个系统的最大抗压能力，在强负载(大数据、高并发)的情况下，测试系统所能承受的最大压力，预估系统的瓶颈    |
| 并发测试(Concurrency Testing)     |  通过模拟很多用户同一时刻访问系统或对系统某一个功能进行操作，来测试系统的性能，从中发现问题(并发读写、线程控制、资源争抢)      |
| 耐久性测试(Configuration Testing) |  通过对系统在大负荷的条件下长时间运行，测试系统、机器的长时间运行下的状况,从中发现问题(内存泄漏、数据库连接池不释放、资源不回收)     |


- 机器性能指标解释

| 机器性能 |   解释  |
| :----:   | :---- |
| CUP利用率(CPU Usage)       |  CUP 利用率分用户态、系统态和空闲态，CPU利用率是指:CPU执行非系统空闲进程的时间与CPU总执行时间的比率      |
| 内存使用率(Memory usage)    |  内存使用率指的是此进程所开销的内存。      |
| IO(Disk input/ output)    |  磁盘的读写包速率       |
| 网卡负载(Network Load)      |  网卡的进出带宽,包量       |



- 访问指标

| 访问 |   解释  |
| :----:   | :---- |
| PV(页面浏览量 Page View)           |  用户每打开1个网站页面，记录1个PV。用户多次打开同一页面，PV值累计多次      |
| UV(网站独立访客 Unique Visitor)    |  通过互联网访问、流量网站的自然人。1天内相同访客多次访问网站，只计算为1个独立访客       |

## 如何计算访问量

- QPS = req/sec = 请求数/秒 = 一段时间内总请求数/请求时间 
- 压测原则:每天80%的访问量集中在20%的时间里，这20%的时间就叫做峰值
- 公式: ( 总PV数*80% ) / ( 每天的秒数*20% ) = 峰值时间每秒钟请求数(QPS)
- 机器: 峰值时间每秒钟请求数(QPS) / 单台机器的QPS = 需要的机器的数量

- 压测是在上线前为了应对未来可能达到的用户数量的一次预估，通过准备充足的机器或优化程序的性能，来保证用户的体验。
- 所以我们压测的目的就是通过压测(模拟真实用户的行为)，测算出机器的性能(单台机器的QPS)，从而推算出系统在承受指定用户数(100W)时，需要多少机器能支撑得住


- 假设:网站每天的用户数(100W)，每天的用户的访问量约为3000W PV，这台机器的需要多少QPS?
> ( 30000000*0.8 ) / (86400 * 0.2) ≈ 1389 (QPS)

- 假设:单台机器的的QPS是69，需要需要多少台机器来支撑？
> 1389 / 69 ≈ 20 


## 常见的压测工具
- 常用的压测工具实现的语言、使用方法、比较、说明
- Jmeter
- AB

## 网络压测
- 阿里云等

## 为什么要实现一个压测工具
- 为什么

## go语言实现压测
- 怎么保持连接
- 实现过程
- 耗时怎么计算，算不算连接事件
- tcp
- webSocket
- http常见的压测
- 压测结束条件

## 新机器部署进行压测
- 申请机器
- 部署环境
- 启动压测 
- 被压测的机器收集数据

## 压测以后
- 数据汇聚成图表
- 百度 ECharts

## 注意事项

## 工作
- 通过文件的方式设置 body Headers
- 解析curl的参数
- webSocket 连接
- 连接以后初始化动作
- 循环事件
- 显示压测数量
- 实现用户数 每秒加几个用户
- 程序结束 优化
- webSocket 建立连接以后，发送消息
- webSocket 首发数据模型调整

## 完善的


## 反思

[性能测试工具](https://testerhome.com/topics/17068)
[性能测试常见名词解释](https://blog.csdn.net/r455678/article/details/53063989)
[性能测试名词解释](https://codeigniter.org.cn/forums/blog-39678-2456.html)
[PV、TPS、QPS是怎么计算出来的？](https://www.zhihu.com/question/21556347)

github 搜:link1st 进入项目
[go-stress-testing https://github.com/link1st/go-stress-testing](https://github.com/link1st/go-stress-testing)


