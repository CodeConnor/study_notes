# 一、大数据导论

## 1.1. 数据分析的作用、方向

> 各行各业可能都需要开展数据分析，我们重点关注商业领域。也就是说企业为什么需要数据分析。
>
> a、原因分析--对应历史数据
>
> b、现状分析--对应当下数据
>
> c、预测分析--结合数据预测未来

- ==离线==分析（==批处理==  batch processing）

  ```
  分析已有的数据 历史数据，面向过去分析。
  在时间维度明显成批次性变化。一周一分析(T+7)，一天一分析（T+1）
  ```

- ==实时==分析（Real Time Processing  ==流处理==Streaming）

  ```
  分析实时产生的数据 当下的数据 面向当下分析
  所谓的实时从数据产生到分析到应用 时间间隔   秒级（spark streaming）  毫秒级(storm flink)
  ```

- ==机器学习==（Machine Learning,ML）

  ```
  基于历史数据和当下产生的实时数据预测未来发生的事情。
  侧重于数学算法的运用。  分类 聚类 关联  预测。
  ```

## 1.2. 数据分析基本步骤

> 数据分析的步骤和流程不仅对我们开展分析提供支撑，同时也对我们去沟通阐述数据分析项目的流程有非常大的支撑。面试时：介绍一下你最近做的项目？如何介绍？介绍什么？

- 明确分析的目的和思路

  ```
  目的：分析方向  分析的主题  要解决什么问题 
  
  思路：如何去开展数据分析 关键分析具有体系。
  
  体系化也就是逻辑化，简单来说就是先分析什么，后分析什么，使得各个分析点之间具有逻辑联系
  
  需要营销、管理类理论进行支撑  叫做数据分析方法论。 偏向于战略层面 从宏观角度指导。
  ```

- 数据收集

  ```shell
  企业常见数据源:
  
  #1、业务数据（RDBMS 关系型数据库 比如：Mysql oracle 事务支持）
  
  #2、日志数据、日志文件（服务器日志、应用日志、用户行为日志）
  
  #3、爬虫数据
  
  #4、其他事数据
  ```

- 数据预处理

  ```shell
  结构化数据、半结构化数据、非结构化数据
  
  大数据青睐什么？结构化数据。
  
  #所谓的结构化数据指的是具有schema约束信息的数据。 通俗理解易于程序处理解读的数据。
  
  半结构化数据（json xml）
  
  #经过预处理把数据变成干净规则统一整洁的结构化数据。
  ```

- 数据分析

  ```
  利用技术和软件 基于指标开展分析。
  ```

- 数据应用

  ```
  分析的结果去哪里？
  数据展现、数据可视化（Data Visualization）
  即席查询
  数据挖掘
  数据接口对外
  ```

**数据源 -> 数据采集 -> 数据存储 -> 数据预处理 -> 数据分析 -> 数据应用**

##   1.3. 分布式、集群

- 共同点：==多台机器==  不是单机的

- 不同点：

  - 集群：每台机器上的服务是一样的。
  - 分别苏：每台集群上的服务、组件是不一样的。

- 提醒：==**口语上，经常会混淆二者概念。都是汲取两者的共同点**==。

  ```
  搭建一个分布式hadoop集群。  多台机器部署不是单机部署
  ```

- 数据大爆炸和面临的挑战解决方案

  - 如何存储海量数据？存储得下。------>==分布式存储==。
  - 如何计算海量数据？高效计算。------->==分布式计算==。

- 扩展：大数据、云计算两个名词如何区分？

  ```shell
  #大数据侧重于海量数据的分析。
  
  #云计算侧重于硬件资源的虚拟机技术。云cloud. 阿里云服务器。vmware。
  公有云：把云资源当做产品卖。
  私有云：自己公司内部搭建云服务器。
  混合云：结合上面两点。
  ```

- 主从架构集群（master/slave架构）

  ```shell
  #指的是集群中的角色分类。分为两类：主角色，从角色。
  
  主角色：master(主宰; 主人; 有控制力的人)  、leader 、大哥
  从角色：slave(奴隶)                    、follower、小弟
  
  作用:主从角色各司其职，互相共同配合 对外提供完整的服务。
  
  对于主从架构，常见的是一主多从。也就是所谓的一个大哥带领多个小弟。
  ```

- 主备架构集群

  ```shell
  #解决单点故障问题。 所谓的单点故障指的是一个服务当中某个组件出现故障，导致整体服务不可用。
  局部故障导致整体不可用。
  
  主角色： active（活跃的角色）
  备份角色：standby(备用物品; 后备人员)
  
  对于主备架构，常见的是一主一备。也可以一主多备，浪费资源。
  ```



# 二、apache zookeeper

## 2.1. 简介

zookeeper是一个分布式的==协调服务==软件（distributed ==**coordination**==）。

```
分布式：多台机器的环境。

协调服务：在分布式环境下，如何控制大家有序的去做某件事。
	顺序
	一致
	共同
	共享
```

zookeeper的本质：==分布式的小文件存储系统==

- 存储系统：存储数据、存储文件   目录树结构
- 小文件：上面存储的数据有大小限制  
- 分布式：可以部署在多台机器上运行，对比单机来理解。
- 问题：zk这个存储系统和我们常见的存储系统不一样。基于这些不一样产生了很多应用。

zookeeper是一个标准的==主从架构==集群。

```
主角色
从角色

主从各司其职 共同配合 对外提供服务。
```

## 2.2. 集群的架构与角色职责

> zk是标准的主从架构，只不过为了扩大集群的读写能力，同时又不增加选举复杂度，又提供了观察者角色。

- 主角色  ==leader==

  ```
  事务性请求的唯一调度和处理者
  ```

- 从角色 ==follower==

  ```
  处理非事务性操作  转发事务性操作给leader
  参与zk内部选举机制
  ```

- 观察者角色 ==Observer==

  ```
  处理非事务性操作  转发事务性操作给leader
  不参与zk内部选举机制
  
  通俗话：是一群被剥夺政治权利终身的follower。
  ```

## 2.3. 数据一致性

==zookeeper集群（zk）中每个服务器保存一份相同的数据副本,客户端无论连接到哪个服务器，展示的数据都是一致的，这是最重要的特征。==

数据一致性解决办法：

读操作（非事务性操作）：主从角色都可以直接处理读操作，直接返回结果给客户端。

写操作（事务性操作）：如果从角色接收到写操作，内部转发给leader，由leader全局统一编号，顺序执行。

## 2.4. zk集群搭建

zk集群在搭建部署的时候，通常选择==**2n+1**==奇数台。底层 Paxos 算法支持（过半成功）。

zk部署之前，保证服务器基础环境正常、==JDK成功安装==。

- 服务器基础环境

  ```
  IP
  主机名
  hosts映射
  防火墙关闭
  时间同步
  ssh免密登录
  ```

- JDK环境

  ```
  jdk1.8
  配置好环境变量
  ```

zk具体安装部署（选择node1安装 scp给其他节点）

- 安装包

  ```
  zookeeper-3.4.6.tar.gz
  ```

- 上传解压重命名

  ```shell
  cd /export/server
  
  tar zxvf zookeeper-3.4.6.tar.gz
  mv zookeeper-3.4.6/ zookeeper
  ```

- 修改配置文件

  - ==**zoo.cfg**==

    ```shell
    #zk默认加载的配置文件是zoo.cfg 因此需要针对模板进行修改。保证名字正确。
    cd zookeeper/conf
    mv zoo_sample.cfg zoo.cfg
    
    vi zoo.cfg
    
    #修改
    dataDir=/export/data/zkdata
    #文件最后添加 2888心跳端口 3888选举端口
    server.1=node1:2888:3888
    server.2=node2:2888:3888
    server.3=node3:2888:3888
    ```

  - 扩展：心跳机制  

    - 分布式软件中从角色向主角色进行心跳 heartbeat
    - 目的：==报活==

  - ==myid==

    ```shell
    #在每台机器的dataDir指定的目录下创建一个文件 名字叫做myid
    #myid里面的数字就是该台机器上server编号。server.N  N的数字就是编号
    [root@node1 conf]# mkdir -p /export/data/zkdata
    [root@node1 conf]# echo 1 >/export/data/zkdata/myid
    ```

  

把安装包同步到其他节点上

```shell
  cd /export/server
scp -r zookeeper/ node2:$PWD
  scp -r zookeeper/ node3:$PWD
```

创建其他机器上myid和datadir目录

```shell
[root@node2 ~]# mkdir -p /export/data/zkdata
[root@node2 ~]# echo 2 > /export/data/zkdata/myid 

[root@node3 ~]# mkdir -p /export/data/zkdata
[root@node3 ~]# echo 3 > /export/data/zkdata/myid 
```

### 2.4.1. 集群启停

每台机器上单独启动服务

```shell
#在哪个目录执行启动命令 默认启动日志就生成当前路径下 叫做zookeeper.out

/export/server/zookeeper/bin/zkServer.sh  start|stop|status

#3台机器启动完毕之后 可以使用status查看角色是否正常。
#还可以使用jps命令查看zk进程是否启动。
[root@node3 ~]# jps
2034 Jps
1980 QuorumPeerMain  #看我，我就是zk的java进程
```

扩展：编写shell脚本 一键脚本启动。

- 本质：在node1机器上执行shell脚本，由==shell程序通过ssh免密登录==到各个机器上帮助执行命令。

- 一键关闭脚本

  ```shell
  [root@node1 ~]# vim stopZk.sh
    
  #!/bin/bash
  hosts=(node1 node2 node3)  # hosts里的主机名称最好通过动态传参赋值，不写死
  for host in ${hosts[*]}
  do
   ssh $host "/export/server/zookeeper/bin/zkServer.sh stop"
  done
  ```

- 一键启动脚本

  ```shell
  [root@node1 ~]# vim startZk.sh
    
  #!/bin/bash
  hosts=(node1 node2 node3)  # hosts里的主机名称最好通过动态传参赋值，不写死
  for host in ${hosts[*]}
  do
   ssh $host "source /etc/profile;/export/server/zookeeper/bin/zkServer.sh start"  # shell程序ssh登录的时候不会自动加载/etc/profile 需要shell程序中自己加载
  done
  ```


注意：关闭java进程时候 根据进程号 直接杀死即可就可以关闭。启动java进程的时候 需要JDK。

shell程序ssh登录的时候不会自动加载/etc/profile 需要shell程序中自己加载。

**在哪个目录执行启动命令 默认启动日志就生成当前路径下 叫做zookeeper.out，启动报错一定要查看日志（tail -f）**

## 2.5. zk数据模型

- 概述

  在结构上和标准文件系统的非常相似，拥有一个层次的命名空间，都是采用树形层次结构；

  ZooKeeper树中的每个节点被称为：Znode，没有文件和目录之分；

  Znode兼具文件和目录两种特点；

  Znode存储数据大小有限制，通常以KB为大小单位；

  Znode通过路径引用，路径必须是绝对的，因此zk路径必须由斜杠字符/来开头，且路径唯一。

![](images\zookeeper节点.png)

- znode

  zk数据模型树中的每个节点称为一个znode，兼具目录文件两种特点。

  每个znode由3部分组成:

  ① stat：此为状态信息, 描述该Znode的版本, 权限等信息

  ② data：与该Znode关联的数据

  ③ children：该Znode下的子节点

- znode类型

  永久节点（PERSISTENCE）

  临时节点（EPHEMERAL）

  永久序列化节点（PERSISTENCE_SEQUENTIAL）

  临时序列化节点（EPHEMERAL_SEQUENTIAL）

临时、永久区别：创建的znode生命周期和创建其客户端的session状态有关

客户端session结束，znode被自动删除-----> 临时节点（ephemeral node）

客户端session结束，znode依然存在，除非手动强制删除-----> 永久节点（persistence node）

临时节点不允许拥有子节点。



- 序列化特性

  开启序列化之后，会自动追加一个不断增加的序列号，记录每个子节点创建的先后顺序。

  序列号对于此节点的父节点来说是唯一的，由10位数字组成。

![](images\zk序列化节点.png)

## 2.6. zk的shell操作

zk的操作:自带shell客户端

```shell
/export/server/zookeeper/bin/zkCli.sh -server ip

#如果不加-server 参数 默认去连接本机的zk服务 localhost:2181
#如果指定-server 参数 就去连接指定机器上的zk服务

#退出客户端端 ctrl+c
```

基本操作

- 创建查看

  ```shell
  [zk: node2(CONNECTED) 28] ls /itcast   #查看指定路径下有哪些节点
  [aaa0000000000, bbbb0000000002, aaa0000000001]
  [zk: node2(CONNECTED) 29] get /
  
  zookeeper   itcast
  [zk: node2(CONNECTED) 29] get /itcast  #获取znode的数据和stat属性信息
  1111
  cZxid = 0x200000003   #创建事务ID
  ctime = Fri May 21 16:20:37 CST 2021 #创建的时间
  mZxid = 0x200000003   #上次修改时事务ID
  mtime = Fri May 21 16:20:37 CST 2021  #上次修改的时间
  pZxid = 0x200000009
  cversion = 3
  dataVersion = 0  #数据版本号  只要有变化 就自动+1
  aclVersion = 0
  ephemeralOwner = 0x0   #如果为0 表示永久节点 如果是sessionID数字 表示临时节点
  dataLength = 4   #数据长度
  numChildren = 3  #子节点个数
  ```

- 更新节点数据

  ```
  set path data
  ```

- 删除节点

  ```shell
    [zk: node2(CONNECTED) 43] ls /itcast
    [aaa0000000000, bbbb0000000002, aaa0000000001]
    [zk: node2(CONNECTED) 44] delete /itcast/bbbb0000000002
    [zk: node2(CONNECTED) 45] delete /itcast               
  Node not empty: /itcast
    [zk: node2(CONNECTED) 46] rmr /itcast  #递归删除
  ```

## 2.7. zk的监听机制

监听实现需要几步？

```shell
#1、设置监听 

#2、执行监听

#3、事件发生，触发监听 通知给设置监听的   回调callback
```

zk中的监听是什么？

- 谁监听谁？

  ```
  客户端监听zk服务
  ```

- 监听什么事？

  ```
  监听zk上目录树znode的变化情况。 znode增加了 删除了 增加子节点了 不见了
  ```

- zk中监听实现步骤

  ```shell
  #1、设置监听 然后zk服务执行监听
  ls path [watch]
  	没有watch 没有监听 就是查看目录下子节点个数
  	有watch  有监听  设置监听子节点是否有变化
  get path [watch]
  	监听节点数据是否变化
  	
  e.g: get /itheima  watch	
  #2、触发监听 
  set /itheima 2222  #修改了被监听的节点数据 触发监听
  
  #3、回调通知客户端
  WATCHER::
  
  WatchedEvent state:SyncConnected type:NodeDataChanged path:/itheima
  ```

zk的监听特性

- ==先注册 再触发==

- ==一次性的监听==，这个效果是一次性的，后续再次发生同样的事件，不会再次触发

- ==异步通知==

- ==通知是使用event事件来封装的==

  ```
  state:SyncConnected type:NodeDataChanged path:/itheima
  
  type：发生了什么
  path:哪里发生的
  ```
  

# 

zk中监听类型

    - 连接状态事件监听  系统自动触发 用户如果不关心可以忽略不计
    - 上述所讲的是用户自定义监听 主要监听zk目录树的变化  这类监听必须先注册 再监听。

==总结：zk的很多功能都是基于这个特殊文件系统而来的。==

- ==特殊1：znode有临时的特性。==
- ==特殊2：znode有序列化的特性。顺序==
- ==特殊3：zk有监听机制 可以满足客户端去监听zk的变化。==
- ==特殊4：在非序列化节点下，路径是唯一的。不能重名。==



# 三、Apache Hadoop

## 3.1. 概述

Hadoop介绍

- 狭义上：hadoop指的是Apache一款java开源软件，是一个大数据分析处理平台。

  - Hadoop ==HDFS：分布式文件系统==。 解决了海量数据存储问题。

    ```
    Hadoop Distributed File System (HDFS™)
    ```

  - Hadoop ==MapReduce：分布式计算框架==。解决海量数据计算问题。

    ```
    parallel processing of large data sets.
    ```

  - Hadoop ==YARN：集群资源管理和任务调度==。

    ```shell
    A framework for job scheduling and cluster resource management.
    
    #资源指的是和程序运行相关的硬件资源
    cpu ram内存
    
    #任务调度
    集群资源繁忙的时候 如何分配资源给各个程序  调度
    调度的关键是策略：先来后到  权重
    ```

- 广义上：Hadoop指的是==hadoop生态圈==。

  ```
  提供了大数据的几乎所有软件。
  采集、存储、导入、分析、挖掘、可视化、管理...
  ```

### 3.1.1. 起源发展

- Hadoop之父--==Doug Cutting== 卡大爷

- 起源项目Apache Nutch。 致力于构建一个==全网搜索引擎==。

  ```
  1、爬取互联网网页 --->存储在哪里？ 海量数据存储问题
  
  2、基于网页创建倒排索引。--->如何计算？  海量数据计算问题
  ```

- Google也在做搜索，也遇到这些问题，内部解决了。

  - ==google==不想开源软件，但是又憋的难受，怕被人不知道，写论文发表。

  - 前后写了==3篇论文==（谷歌是使用c实现的）。 

    ```
    谷歌分布式文件系统（GFS）------>HDFS
    谷歌版MapReduce 系统------>Hadoop MapReduce
    bigtable---->HBase
    ```

  - 基于论文的影响 Nutch团队实现了相应的java版本开源组件。

- Nutch团队把HDFS和MapReduce抽取独立成为单独软件在==2008年贡献给了Apache==。开源。

### 3.1.2. 集群简介

通常是有==hdfs集群==和==yarn集群==组成。两个集群都是标准的==主从架构==集群。

两个集群逻辑上分离，物理上在一起。

HDFS集群：解决了海量数据存储  分布式存储系统

- 主角色：namenode（NN）
- 从角色：datanode（DN）
- 主角色辅助角色"秘书角色"：secondarynamenode （SNN）

YARN集群：集群资源管理 任务调度

- 主角色：resourcemanager（RM）
- 从角色：nodemanager（NM）

## 3.2. 集群搭建部署

- 单机模式 Standalone

  ```
  一台机器，所有的角色在一个java进程中运行。 适合体验。
  ```

- 伪分布式

  ```
  一台机器 每个角色单独的java进程。 适合测试
  ```

- ==分布式  cluster== 

  ```
  多台机器  每个角色运行在不同的机器上  生产测试都可以
  ```

- 高可用（持续可用）集群 HA

  ```
  在分布式的模式下 给主角色设置备份角色  实现了容错的功能 解决了单点故障
  保证集群持续可用性。
  ```

### 3.2.1. 源码编译

> https://archive.apache.org/dist/
>
> Apache软件基金会的所有软件所有版本的下载地址.

- 源码下载地址

  ```
  https://archive.apache.org/dist/hadoop/common/
  
  hadoop-3.3.0-src.tar.gz    source 源码包
  hadoop-3.3.0.tar.gz        官方编译后安装包
  ```

- 对应java语言开发的项目软件来说，所谓的==编译==是什么？

  ```
  xxx.java(源码)---->xxx.class(字节码)---->jar包
  ```

- 正常来说，官方网站提供了安装包，可以直接使用，为什么要自己编译呢？

  - ==修改源码==之后需要重新编译。
  - 官方提供的最大化编译 满足在各个平台运行，但是不一定彻底==兼容本地环境==。
  - 某些软件，官方只提供源码。

  ```
  native library 本地库。
  官方编译好的 Hadoop的安装包没有提供带 C程序访问的接口。主要是本地压缩支持、IO支持。
  ```

- 怎么编译？

  ```
  在源码的根目录下有编译相关的文件BUILDING.txt 指导如何编译。
  使用maven进行编译 联网jar.
  ```

- 可以使用编译好的安装包

  ```shell
  hadoop-3.3.0-Centos7-64-with-snappy.tar.gz
  ```

### 3.2.2. 集群角色规划

根据==软件和硬件的特性 合理的安排==各个角色在不同的机器上。

- 有冲突的尽量不部署在一起
- 有工作依赖尽量部署在一起
- nodemanager  和datanode是基友

```properties
node1: namenode  datanode                    | resourcemanager  nodemanger
node2:			 datanode   secondarynamenode|			        nodemanger
node3:			 datanode                    |  		        nodemanger
```

- Q：如果后续需要扩容hadoop集群，应该增加哪些角色呢？

  ```properties
  node4:  datanode  nodemanger
  node5:  datanode  nodemanger
  node6:  datanode  nodemanger
  .....
  ```

### 3.2.3. 安装包目录结构

**bin**：==Hadoop最基本的管理脚本和使用脚本的目录==，这些脚本是sbin目录下管理脚本的基础实现，用户可以直接使用这些脚本管理和使用Hadoop。

**etc**：==Hadoop配置文件所在的目录==，包括core-site,xml、hdfs-site.xml、mapred-site.xml等从Hadoop1.0继承而来的配置文件和yarn-site.xml等Hadoop2.0新增的配置文件。

include：对外提供的编程库头文件（具体动态库和静态库在lib目录中），这些头文件均是用C++定义的，通常用于C++程序访问HDFS或者编写MapReduce程序。

lib：该目录包含了Hadoop对外提供的编程动态库和静态库，与include目录中的头文件结合使用。

libexec：各个服务对用的shell配置文件所在的目录，可用于配置日志输出、启动参数（比如JVM参数）等基本信息。

**sbin**：==Hadoop管理脚本所在的目录，主要包含HDFS和YARN中各类服务的启动/关闭脚本。==

**share**：==Hadoop各个模块编译后的jar包所在的目录，官方自带示例==。

### 3.2.4. 修改配置文件

修改配置文件(配置文件路径 hadoop-3.3.0/etc/hadoop)

- hadoop-env.sh

  ```shell
  export JAVA_HOME=/export/server/jdk1.8.0_241
  
  #文件最后添加
  export HDFS_NAMENODE_USER=root
  export HDFS_DATANODE_USER=root
  export HDFS_SECONDARYNAMENODE_USER=root
  export YARN_RESOURCEMANAGER_USER=root
  export YARN_NODEMANAGER_USER=root 
  ```

- core-site.xml

  ```xml
  <!-- 设置默认使用的文件系统 Hadoop支持file、HDFS、GFS、ali|Amazon云等文件系统 -->
  <property>
      <name>fs.defaultFS</name>
      <value>hdfs://node1:8020</value>
  </property>
  
  <!-- 设置Hadoop本地保存数据路径 -->
  <property>
      <name>hadoop.tmp.dir</name>
      <value>/export/data/hadoop-3.3.0</value>
  </property>
  
  <!-- 设置HDFS web UI用户身份 -->
  <property>
      <name>hadoop.http.staticuser.user</name>
      <value>root</value>
  </property>
  
  <!-- 整合hive 用户代理设置 -->
  <property>
      <name>hadoop.proxyuser.root.hosts</name>
      <value>*</value>
  </property>
  
  <property>
      <name>hadoop.proxyuser.root.groups</name>
      <value>*</value>
  </property>
  
  <property>
      <name>fs.trash.interval</name>
      <value>1440</value>
  </property>
  ```

- hdfs-site.xml

  ```xml
  <!-- 设置SNN进程运行机器位置信息 -->
  <property>
      <name>dfs.namenode.secondary.http-address</name>
      <value>node2:9868</value>
  </property>
  ```

- mapred-site.xml

  ```xml
  <!-- 设置MR程序默认运行模式： yarn集群模式 local本地模式 -->
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
  
  <!-- MR程序历史服务器端地址 -->
  <property>
    <name>mapreduce.jobhistory.address</name>
    <value>node1:10020</value>
  </property>
   
  <!-- 历史服务器web端地址 -->
  <property>
    <name>mapreduce.jobhistory.webapp.address</name>
    <value>node1:19888</value>
  </property>
  
  <property>
    <name>yarn.app.mapreduce.am.env</name>
    <value>HADOOP_MAPRED_HOME=${HADOOP_HOME}</value>
  </property>
  
  <property>
    <name>mapreduce.map.env</name>
    <value>HADOOP_MAPRED_HOME=${HADOOP_HOME}</value>
  </property>
  
  <property>
    <name>mapreduce.reduce.env</name>
    <value>HADOOP_MAPRED_HOME=${HADOOP_HOME}</value>
  </property>
  ```

- yarn-site.xml

  ```xml
  <!-- 设置YARN集群主角色运行机器位置 -->
  <property>
  	<name>yarn.resourcemanager.hostname</name>
  	<value>node1</value>
  </property>
  
  <property>
      <name>yarn.nodemanager.aux-services</name>
      <value>mapreduce_shuffle</value>
  </property>
  
  <!-- 是否将对容器实施物理内存限制 -->
  <property>
      <name>yarn.nodemanager.pmem-check-enabled</name>
      <value>false</value>
  </property>
  
  <!-- 是否将对容器实施虚拟内存限制。 -->
  <property>
      <name>yarn.nodemanager.vmem-check-enabled</name>
      <value>false</value>
  </property>
  
  <!-- 开启日志聚集 -->
  <property>
    <name>yarn.log-aggregation-enable</name>
    <value>true</value>
  </property>
  
  <!-- 设置yarn历史服务器地址 -->
  <property>
      <name>yarn.log.server.url</name>
      <value>http://node1:19888/jobhistory/logs</value>
  </property>
  
  <!-- 保存的时间7天 -->
  <property>
    <name>yarn.log-aggregation.retain-seconds</name>
    <value>604800</value>
  </property>
  ```

- workers

  ```
  node1
  node2
  node3
  ```

分发同步hadoop安装包

```shell
cd /export/server

scp -r hadoop-3.3.0 root@node2:$PWD
scp -r hadoop-3.3.0 root@node3:$PWD
```

- 将hadoop添加到环境变量（3台机器）

  ```shell
  vim /etc/profile
  
  export HADOOP_HOME=/export/server/hadoop-3.3.0
  export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
  
  source /etc/profile
  
  
  #别忘了scp给其他两台机器哦
  ```

### 3.2.5. 启动

Hadoop集群启动

（==首次启动==）格式化namenode

```shell
hdfs namenode -format
```

format准确来说翻译成为==初始化==比较好。对namenode工作目录、初始文件进行生成。

通常在namenode所在的机器执行  ==执行一次。首次启动之前==

```shell
#在node1 部署namenode的这台机器上执行

hadoop namenode -format

#执行成功 日志会有如下显示
21/05/23 15:38:19 INFO common.Storage: Storage directory /export/data/hadoopdata/dfs/name has been successfully formatted.

[root@node1 server]# ll /export/data/hadoopdata/dfs/name/current/
total 16
-rw-r--r-- 1 root root 321 May 23 15:38 fsimage_0000000000000000000
-rw-r--r-- 1 root root  62 May 23 15:38 fsimage_0000000000000000000.md5
-rw-r--r-- 1 root root   2 May 23 15:38 seen_txid
-rw-r--r-- 1 root root 207 May 23 15:38 VERSION
```

Q：如果不小心初始化了多次，如何？

- 现象：主从之间互相不识别。

- 解决

  ```shell
  #企业真实环境中    绝不允许
  
  #学习环境
  删除每台机器上hadoop.tmp.dir配置指定的文件夹/export/data/hadoop-3.3.0。 
  重新format。
  ```



单节点单进程逐个手动启动

- HDFS集群

  ```shell
  #hadoop2.x版本命令
  hadoop-daemon.sh start|stop  namenode|datanode|secondarynamenode
  
  #hadoop3.x版本命令
  hdfs --daemon start|stop namenode|datanode|secondarynamenode
  ```

- YARN集群

  ```shell
  #hadoop2.x版本命令
  yarn-daemon.sh start|stop resourcemanager|nodemanager
  
  #hadoop3.x版本命令
  yarn --daemon start|stop resourcemanager|nodemanager
  ```

- 优点：精准的控制每个角色每个进程的启停。避免了群起群停（时间成本）。



脚本一键启动

前提：==配置好免密登录。ssh==

HDFS集群

```
start-dfs.sh 
stop-dfs.sh 
```

YARN集群

```shell
start-yarn.sh
stop-yarn.sh
```

同时启动HDFS和YARN：

```shell
start-all.sh
stop-all.sh

[root@node1 ~]# start-all.sh 
This script is Deprecated. Instead use start-dfs.sh and start-yarn.sh
```



集群进程确认和错误排查

- 确认是否成功

  ```shell
  [root@node1 ~]# jps
  8000 DataNode
  8371 NodeManager
  8692 Jps
  8264 ResourceManager
  7865 NameNode
  ```

- 如果进程不在  ==看启动运行日志！！！！！！！！！！！！！==

  ```shell
  #默认情况下 日志目录
  cd /export/server/hadoop-3.3.0/logs/
  
  #注意找到对应进程名字 以log结尾的文件
  ```

### 3.2.6 UI界面

Hadoop Web UI页面

- HDFS集群   http://namenode_host:9870（部署namenode的主机的地址+9870端口，比如：node1:9870）
- YARN集群  http://resourcemanager_host:8088 （node1:8088）

```
http://node1:9870/dfshealth.html#tab-overview
```

### 3.2.7. jobhistory服务配置与功能

背景

```
默认情况下，yarn上关于MapReduce程序执行历史信息、执行记录不会永久存储；
一旦yarn集群重启 之前的信息就会消失。
```

功能

```
保存yarn上已经完成的MapReduce的执行信息。
```

配置

- 因为需求修改配置。==重启hadoop集群==才能生效。使用node1:19888查看

  ```xml
  vim mapred-site.xml
  
  <property>
  	<name>mapreduce.jobhistory.address</name>
  	<value>node1:10020</value>
  </property>
  
  <property>
  	<name>mapreduce.jobhistory.webapp.address</name>
  	<value>node1:19888</value>
  </property>
  ```

- scp同步给其他机器

  ```shell
  scp /export/server/hadoop-3.3.0/etc/hadoop/mapred-site.xml node2:/export/server/hadoop-3.3.0/etc/hadoop/
  
  scp /export/server/hadoop-3.3.0/etc/hadoop/mapred-site.xml node3:/export/server/hadoop-3.3.0/etc/hadoop/
  ```

- 重启hadoop集群

- 自己手动启停jobhistory服务。

  ```shell
  #hadoop2.x版本命令
  mr-jobhistory-daemon.sh start|stop historyserver
  
  #hadoop3.x版本命令
  mapred --daemon start|stop historyserver
  
  [root@node1 ~]# jps
  13794 JobHistoryServer
  13060 DataNode
  12922 NameNode
  13436 NodeManager
  13836 Jps
  13327 ResourceManager
  ```

---

### 3.2.8. HDFS垃圾桶机制

背景：垃圾桶在windows叫做回收站 

```shell
在默认情况下 hdfs没有垃圾桶 意味着删除操作直接物理删除文件。

[root@node1 ~]# hadoop fs -rm /itcast/1.txt
Deleted /itcast/1.txt
```

功能：和回收站一种  在删除数据的时候 先去垃圾桶 如果后悔可以复原。

配置

```xml
在core-site.xml中开启垃圾桶机制

指定保存在垃圾桶的时间。单位分钟

<property>
	<name>fs.trash.interval</name>
	<value>1440</value>
</property>
```

集群同步配置 重启hadoop服务。

```shell
[root@node1 hadoop]# pwd
/export/server/hadoop-3.3.0/etc/hadoop
[root@node1 hadoop]# scp core-site.xml node2:$PWD
core-site.xml                                              100% 1027   898.7KB/s   00:00    
[root@node1 hadoop]# scp core-site.xml node3:$PWD
core-site.xml 
```

垃圾桶使用

- 配置好之后 再删除文件  直接进入垃圾桶

  ```
  [root@node1 ~]# hadoop fs -rm /itcast.txt
  INFO fs.TrashPolicyDefault: Moved: 'hdfs://node1:8020/itcast.txt' to trash at: hdfs://node1:8020/user/root/.Trash/Current/itcast.txt
  ```

- 垃圾桶的本质就是hdfs上的一个隐藏目录。

  ```
    hdfs://node1:8020/user/用户名/.Trash/Current
  ```

- 后悔了 需要恢复怎么做？

  ```
    hadoop fs -cp /user/root/.Trash/Current/itcast.txt /
  ```

- 就想直接删除文件怎么做？

  ```shell
    hadoop fs -rm -skipTrash /itcast.txt
     
    [root@node1 ~]#  hadoop fs -rm -skipTrash /itcast.txt
    Deleted /itcast.txt
  ```

## 3.3. HDFS

> ==成熟的分布式==文件系统应该要具备的属性、功能

- 分布式存储
- 元数据记录
- 分块存储
- 副本机制

### 3.3.1. 简介

HDFS基本概念

首先是一个==文件系统==，就是用来存储文件、存储数据。是大数据最底层一个服务。其次是一个==分布式的文件系统==。分布式意味着多台机器存储。

![HDFS结构](images\HDFS结构.png)

起源发展和设计目标

- 具备故障检测和快速恢复的能力（容错）
- 面对海量数据的存储，注重吞吐能力，而不是交互式。（延迟高）
- 支持大文件存储（越大越开心）
- ==一次写入==多次读取模型  （不支持修改操作）
- 异构存储、可移植性

### 3.3.2. 核心特征

**主从架构**

![HDFS核心架构](images\HDFS核心架构.png)

HDFS采用master/slave架构。一般一个HDFS集群是有一个Namenode和一定数目的Datanode组成。

Namenode是HDFS集群主节点，Datanode是HDFS集群从节点，两种角色各司其职，共同协调完成分布式的文件存储服务。

官方架构图中是一主五从模式，其中五个从角色位于两个机架（Rack）的不同服务器上。

**分块存储**

HDFS中的文件在物理上是分块存储（block）的，默认大小是128M（134217728），不足128M则本身就是一块。

块的大小可以通过配置参数来规定，参数位于hdfs-default.xml中：dfs.blocksize。

**副本机制**

文件的所有block都会有副本。副本系数可以在文件创建的时候指定，也可以在之后通过命令改变。

副本数由参数dfs.replication控制，默认值是3，也就是会额外再复制2份，连同本身总共3份副本。

**元数据管理**

我们把目录结构及文件分块位置信息叫做元数据。Namenode负责维护整个hdfs文件系统的目录树结构，以及每一个文件所对应的block块信息（block的id，及所在的datanode服务器）。

在HDFS中，Namenode管理的元数据具有两种类型：

文件自身属性信息：文件名称、权限，修改时间，文件大小，复制因子，数据块大小。

文件块位置映射信息：记录文件块和DataNode之间的映射信息，即哪个块位于哪个节点上。

**namespace**

HDFS支持传统的层次型文件组织结构。用户或者应用程序可以创建目录，然后将文件保存在这些目录里。文件系统名字空间的层次结构和大多数现有的文件系统类似：用户可以创建、删除、移动或重命名文件。

Namenode负责维护文件系统的名字空间，任何对文件系统名字空间或属性的修改都将被Namenode记录下来。

HDFS会给客户端提供一个统一的抽象目录树，客户端通过路径来访问文件，形如：hdfs://namenode:port/dir-a/dir-b/dir-c/file.data。

**datanode数据存储**

文件的各个block的具体存储管理由datanode节点承担。每一个block都可以在多个datanode上。Datanode需要定时向Namenode汇报自己持有的block信息。

### 3.3.3. shell命令行

Hadoop提供了文件系统的shell命令行客户端: hadoop fs [generic options]

HDFS Shell CLI支持操作多种文件系统，包括本地文件系统（file:///）、分布式文件系统（hdfs://nn:8020）等

具体操作的是什么文件系统取决于命令中文件路径URL中的前缀协议。

如果没有指定前缀，则将会读取环境变量中的fs.defaultFS属性，以该属性值作为默认文件系统。

文件系统shell包括与Hadoop分布式文件系统（HDFS）以及Hadoop支持的其他文件系统（如本地FS，HFTP FS，S3 FS等）直接交互的各种类似shell的命令。所有FS shell命令都将路径URI作为参数。

URI格式为scheme://authority/path。对于HDFS，该scheme是hdfs，对于本地FS，该scheme是file。scheme和authority是可选的。如果未指定，则使用配置中指定的默认方案。

```shell
# 对于HDFS,命令示例如下：
hadoop fs -ls  hdfs://namenode:host/parent/child
hadoop fs -ls  /parent/child  # fs.defaultFS中有配置

# 对于本地文件系统，命令示例如下：
hadoop fs -ls file:///root/ 

# 如果使用的文件系统是HDFS，则使用hdfs dfs也是可以的，此时
hadoop fs <args> = hdfs dfs <args>
```

#### 3.3.3.1 命令行常用操作

| 选项名称       | 使用格式                                                     | 含义                             |
| -------------- | ------------------------------------------------------------ | -------------------------------- |
| -ls            | -ls <路径>                                                   | 查看指定路径的当前目录结构       |
| -lsr           | -lsr <路径>                                                  | 递归查看指定路径的目录结构       |
| -du            | -du <路径>                                                   | 统计目录下个文件大小             |
| -dus           | -dus <路径>                                                  | 汇总统计目录下文件(夹)大小       |
| -count         | -count [-q] <路径>                                           | 统计文件(夹)数量                 |
| -mv            | -mv <源路径> <目的路径>                                      | 移动                             |
| -cp            | -cp <源路径> <目的路径>                                      | 复制                             |
| -rm            | -rm [-skipTrash] <路径>                                      | 删除文件/空白文件夹              |
| -rmr           | -rmr [-skipTrash] <路径>                                     | 递归删除                         |
| -put           | -put <多个linux上的文件> <hdfs路径>                          | 上传文件                         |
| -copyFromLocal | -copyFromLocal <多个linux上的文件> <hdfs路径>                | 从本地复制                       |
| -moveFromLocal | -moveFromLocal <多个linux上的文件> <hdfs路径>                | 从本地移动                       |
| -getmerge      | -getmerge <源路径> <linux路径>                               | 合并到本地                       |
| -appendToFile  | -appendToFile <源路径> <linux路径>                           | 追加一个文件到已经存在的文件末尾 |
| -cat           | -cat <hdfs路径>                                              | 查看文件内容                     |
| -text          | -text <hdfs路径>                                             | 查看文件内容                     |
| -copyToLocal   | -copyToLocal [-ignoreCrc] [-crc] [hdfs源路径] [linux目的路径] | 从本地复制                       |
| -moveToLocal   | -moveToLocal [-crc] <hdfs源路径> <linux目的路径>             | 从本地移动                       |
| -mkdir         | -mkdir <hdfs路径>                                            | 创建空白文件夹                   |
| -setrep        | -setrep [-R] [-w] <副本数> <路径>                            | 修改副本数量                     |
| -touchz        | -touchz <文件路径>                                           | 创建空白文件                     |
| -stat          | -stat [format] <路径>                                        | 显示文件统计信息                 |
| -tail          | -tail [-f] <文件>                                            | 查看文件尾部信息                 |
| -chmod         | -chmod [-R] <权限模式> [路径]                                | 修改权限                         |
| -chown         | -chown [-R] [属主][:[属组]] 路径                             | 修改属主                         |
| -chgrp         | -chgrp [-R] 属组名称 路径                                    | 修改属组                         |
| -help          | -help [命令选项]                                             | 帮助                             |

**-ls**

使用方法：hadoop fs -ls [-h] [-R] <args>

功能：显示文件、目录信息。

示例：hadoop fs -ls /user/hadoop/file1



**-mkdir**

使用方法：hadoop fs -mkdir [-p] <paths>

功能：在hdfs上创建目录，-p表示会创建路径中的各级父目录。

示例：hadoop fs -mkdir –p /user/hadoop/dir1



**-put**
使用方法：hadoop fs -put [-f] [-p] [ -|<localsrc1> .. ]. <dst> 

功能：将单个src或多个srcs从本地文件系统复制到目标文件系统。

-p：保留访问和修改时间，所有权和权限。

-f：覆盖目的地（如果已经存在）

示例：hadoop fs -put -f localfile1 localfile2 /user/hadoop/hadoopdir



**-get**

使用方法：hadoop fs -get [-ignorecrc] [-crc] [-p] [-f] <src> <localdst>

-ignorecrc：跳过对下载文件的CRC检查。

-crc：为下载的文件写CRC校验和。

功能：将文件复制到本地文件系统。

示例：hadoop fs -get hdfs://host:port/user/hadoop/file localfile



**-appendToFile** 

使用方法：hadoop fs -appendToFile <localsrc> ... <dst>

功能：追加一个文件到已经存在的文件末尾

示例：hadoop fs -appendToFile localfile  /hadoop/hadoopfile



**-cat**  

使用方法：hadoop fs -cat [-ignoreCrc] URI [URI ...]

功能：显示文件内容到stdout

示例：hadoop fs -cat  /hadoop/hadoopfile



**-tail**

使用方法：hadoop fs -tail [-f] URI 

功能：将文件的最后一千字节内容显示到stdout。

-f选项将在文件增长时输出附加数据。

示例：hadoop  fs  -tail  /hadoop/hadoopfile



**-chgrp** 

使用方法：hadoop fs -chgrp [-R] GROUP URI [URI ...]

功能：更改文件组的关联。用户必须是文件的所有者，否则是超级用户。

-R将使改变在目录结构下递归进行。

示例：hadoop fs -chgrp othergroup /hadoop/hadoopfile



**-chmod**

功能：改变文件的权限。使用-R将使改变在目录结构下递归进行。

示例：hadoop  fs  -chmod  666  /hadoop/hadoopfile



**-chown**

功能：改变文件的拥有者。使用-R将使改变在目录结构下递归进行。

示例：hadoop  fs  -chown  someuser:somegrp  /hadoop/hadoopfile



**-cp**        

功能：从hdfs的一个路径拷贝hdfs的另一个路径

示例： hadoop  fs  -cp  /aaa/jdk.tar.gz  /bbb/jdk.tar.gz.2



**-mv**           

功能：在hdfs目录中移动文件

示例： hadoop  fs  -mv  /aaa/jdk.tar.gz  /



**-getmerge**   

功能：合并下载多个文件

示例：比如hdfs的目录 /aaa/下有多个文件:log.1, log.2,log.3,...

hadoop fs -getmerge /aaa/log.*  ./log.sum



**-rm**         

功能：删除指定的文件。只删除非空目录和文件。-r 递归删除。

示例：hadoop fs -rm -r /aaa/bbb/



**-df**        

功能：统计文件系统的可用空间信息

示例：hadoop  fs  -df  -h  /



**-du** 

功能：显示目录中所有文件大小，当只指定一个文件时，显示此文件的大小。

示例：hadoop fs -du /user/hadoop/dir1



**-setrep**         

功能：改变一个文件的副本系数。-R选项用于递归改变目录下所有文件的副本系数。

示例：hadoop fs -setrep -w 3 -R /user/hadoop/dir1

### 3.3.4. 集群角色

**NameNode概述**

a、NameNode是HDFS的核心。

b、 NameNode也称为Master。

c、 NameNode仅存储HDFS的元数据：文件系统中所有文件的目录树，并跟踪整个集群中的文件。

d、 NameNode不存储实际数据或数据集。数据本身实际存储在DataNodes中。

e、 NameNode知道HDFS中任何给定文件的块列表及其位置。使用此信息NameNode知道如何从块中构建文件。

f、 NameNode并不持久化存储每个文件中各个块所在的DataNode的位置信息，这些信息会在系统启动时从数据节点重建。

g、 NameNode对于HDFS至关重要，当NameNode关闭时，HDFS / Hadoop集群无法访问。

h、 NameNode是Hadoop集群中的单点故障。

i、 NameNode所在机器通常会配置有大量内存（RAM）。



**datanode概述**

a、 DataNode负责将实际数据存储在HDFS中。

b、 DataNode也称为Slave。

c、 NameNode和DataNode会保持不断通信。

d、 DataNode启动时，它将自己发布到NameNode并汇报自己负责持有的块列表。

e、 当某个DataNode关闭时，它不会影响数据或群集的可用性。NameNode将安排由其他DataNode管理的块进行副本复制。

f、 DataNode所在机器通常配置有大量的硬盘空间。因为实际数据存储在DataNode中。

g、 DataNode会定期（dfs.heartbeat.interval配置项配置，默认是3秒）向NameNode发送心跳，如果NameNode长时间没有接受到DataNode发送的心跳， NameNode就会认为该DataNode失效。

h、 block汇报时间间隔取参数dfs.blockreport.intervalMsec,参数未配置的话默认为6小时.

### 3.3.5. 读写流程

#### 3.3.5.1. 核心知识

**Pipeline**

中文翻译为管道。这是HDFS在上传文件写数据过程中采用的一种数据传输方式。

客户端将数据块写入第一个数据节点，第一个数据节点保存数据之后再将块复制到第二个数据节点，后者保存后将其复制到第三个数据节点。

为什么datanode之间采用pipeline线性传输，而不是一次给三个datanode拓扑式传输呢？

==因为数据以管道的方式，顺序的沿着一个方向传输，这样能够充分利用每个机器的带宽，避免网络瓶颈和高延迟时的连接，最小化推送所有数据的延时。==

在线性推送模式下，每台机器所有的出口宽带都用于以最快的速度传输数据，而不是在多个接受者之间分配宽带。

**ACK应答响应**

ACK (Acknowledge character）即是确认字符，在数据通信中，接收方发给发送方的一种传输类控制字符。表示发来的数据已确认接收无误。

在HDFS pipeline管道传输数据的过程中，传输的反方向会进行ACK校验，确保数据传输安全。

![pipeline & ACK](images\pipeline & ACK.png)

**默认3副本存储策略**

第一块副本：优先客户端本地，否则随机

第二块副本：不同于第一块副本的不同机架。

第三块副本：第二块副本相同机架不同机器。

![默认3副本存储策略](images\默认3副本存储策略.png)

#### 3.3.5.2. 写（上传）数据流程

![HDFS写数据流程](images\HDFS写数据流程.png)

1、HDFS客户端创建FileSystem对象实例DistributedFileSystem， FileSystem封装了与文件系统操作的相关方法。

2、调用DistributedFileSystem对象的create()方法，通过RPC请求NameNode创建文件。NameNode执行各种检查判断：目标文件是否存在、父目录是否存在、客户端是否具有创建该文件的权限。检查通过，NameNode就会为本次请求记下一条记录，返回FSDataOutputStream输出流对象给客户端用于写数据。

3、客户端通过FSDataOutputStream输出流开始写入数据。

4、客户端写入数据时，将数据分成一个个数据包（packet 默认64k）,并写入一个内部数据队列（data queue）。有一个内部类做DataStreamer，用于请求NameNode挑选出适合存储数据副本的一组DataNode，默认是3副本存储。DataStreamer将数据包流式传输到pipeline的第一个DataNode,该DataNode存储数据包并将它发送到pipeline的第二个DataNode。同样，第二个DataNode存储数据包并且发送给第三个（也是最后一个）DataNode。

5、OutputStream也维护着一个内部数据包队列来等待DataNode的收到确认回执，称之为确认队列（ack queue）,收到pipeline中所有DataNode确认信息后，该数据包才会从确认队列删除。

6、客户端完成数据写入后，在FSDataOutputStream输出流上调用close()方法关闭。

7、DistributedFileSystem联系NameNode告知其文件写入完成，等待NameNode确认。因为namenode已经知道文件由哪些块组成（DataStream请求分配数据块），因此仅需等待最小复制块即可成功返回。最小复制是由参数dfs.namenode.replication.min指定，默认是1。

#### 3.3.5.3. 读（下载）数据流程

![HDFS读数据流程](images\HDFS读数据流程.png)

1、HDFS客户端创建FileSystem对象实例DistributedFileSystem， FileSystem封装了与文件系统操作的相关方法。调用DistributedFileSystem对象的open()方法来打开希望读取的文件。

2、DistributedFileSystem使用RPC调用namenode来确定文件中前几个块的块位置（分批次读取）信息。对于每个块，namenode返回具有该块所有副本的datanode位置地址列表，并且该地址列表是排序好的，与客户端的网络拓扑距离近的排序靠前。

3、DistributedFileSystem将FSDataInputStream输入流返回到客户端以供其读取数据。

4、客户端在FSDataInputStream输入流上调用read()方法。然后，已存储DataNode地址的InputStream连接到文件中第一个块的最近的DataNode。数据从DataNode流回客户端，结果客户端可以在流上重复调用read（）。

5、当该块结束时，InputStream将关闭与DataNode的连接，然后寻找下一个块的最佳datanode。这些操作对用户来说是透明的。所以用户感觉起来它一直在读取一个连续的流。客户端从流中读取数据时，也会根据需要询问NameNode来检索下一批数据块的DataNode位置信息。

6、一旦客户端完成读取，就对FSDataInputStream调用close()方法。

### 3.3.6. HDFS辅助工具

#### 3.3.6.1. 跨集群复制数据 distcp（distributed copy）

- 功能：实现在不同的hadoop集群之间进行数据复制同步。

- 用法：

  ```shell
  #同一个集群内 复制操作
  hadoop fs -cp /zookeeper.out /itcast
  
  #跨集群复制操作
  hadoop distcp hdfs://node1:8020/1.txt  hdfs:node5:8020/itcast
  ```

#### 3.3.6.2. 文件归档工具 archive

背景

```
hdfs的架构设计不适合小文件存储的。
因为小文件不管多小 都需要一定的元数据记录它 元数据保存在内存中的，
如果集群小文件过多 就会造成内存被撑爆。 俗称 小文件吃内存。
```

archive功能

- 将一批小文件归档一个档案文件。
- 底层是通过==MapReduce程序将小文件进行合并的。启动yarn集群执行mr程序==。
- 企业中可以根据时间 定时进行归档，比如一周创建一个档案。

![HDFS archive](images\HDFS archive.png)

使用

```shell
#创建档案
hadoop archive -archiveName test.har -p /small /outputdir

基于自己的需求 删除小文件 减少对内存的消耗
hadoop fs -rm /small/*

#查看档案文件 --归档之后的样子
[root@node1 ~]# hadoop fs -ls hdfs://node1:8020/outputdir/test.har
Found 4 items
hdfs://node1:8020/outputdir/test.har/_SUCCESS
hdfs://node1:8020/outputdir/test.har/_index
hdfs://node1:8020/outputdir/test.har/_masterindex
hdfs://node1:8020/outputdir/test.har/part-0

#查看档案文件 --归档之前的样子
[root@node1 ~]# hadoop fs -ls har://hdfs-node1:8020/outputdir/test.har
Found 3 items
 har://hdfs-node1:8020/outputdir/test.har/1.txt
 har://hdfs-node1:8020/outputdir/test.har/2.txt
 har://hdfs-node1:8020/outputdir/test.har/3.txt

#从档案文件中提取文件
[root@node1 ~]# hadoop fs -cp har://hdfs-node1:8020/outputdir/test.har/* /small/
[root@node1 ~]# hadoop fs -ls /small
Found 3 items
-rw-r--r--   3 root supergroup          2 2021-05-24 17:58 /small/1.txt
-rw-r--r--   3 root supergroup          2 2021-05-24 17:58 /small/2.txt
-rw-r--r--   3 root supergroup          2 2021-05-24 17:58 /small/3.txt
```

注意

- archive没有压缩的功能 就是简单的==合二为一的操作 减少小文件个数==。

### 3.3.7. 安全模式

安全模式（safe mode）是HDFS集群处于一种保护状态，==文件系统只可以读，不可以写==。

安全模式如何进入离开的？

- 自动进入离开

  ```shell
  #在HDFS集群刚启动时候 会自动进入 为了演示方便  使用单个进程逐个启动方式
  
  #step1：启动namenode
  hadoop-daemon.sh start namenode
  
  #step2: 执行事务性操作 报错
  [root@node1 ~]# hadoop fs -mkdir /aaaa
  mkdir: Cannot create directory /aaaa. Name node is in safe mode.
  
  Safe mode is ON. The reported blocks 0 needs additional 52 blocks to reach the threshold 0.9990 of total blocks 52. The number of live datanodes 0 has reached the minimum number 0. Safe mode will be turned off automatically once the thresholds have been reached.
  
  #1、条件1:已经汇报的block达到总数据块的 0.999
  #2、条件2:存活的dn数量大于等于0  说明这个条件不严格
  
  
  #step3:依次手动启动datanode
  hadoop-daemon.sh start datanode
  
  Safe mode is ON. The reported blocks 52 has reached the threshold 0.9990 of total blocks 52. The number of live datanodes 2 has reached the minimum number 0. In safe mode extension. Safe mode will be turned off automatically in 25 seconds.
  #3、条件3:满足12条件的情况下 持续30s 结束自动离开安全模式
  
  Safemode is off.
  
  
  #为什么集群刚启动的时候 要进入安全模式 
  文件系统元数据不完整 无法对外提供可高的文件服务  属于内部的元数据汇报、校验、构建的过程。
  
  ```

- 手动进入离开

  ```shell
  hdfs dfsadmin -safemode enter
  hdfs dfsadmin -safemode leave
  
  Safe mode is ON. It was turned on manually. Use "hdfs dfsadmin -safemode leave" to turn safe mode off.
  
  #运维人员可以手动进入安全模式 进行集群的维护升级等动作 避免了群起群停浪费时间。
  ```

安全模式的注意事项

- 刚启动完hdfs集群之后 等安全模式介绍才可以正常使用文件系统  文件系统服务才是正常可用。
- 后续如果某些软件依赖HDFS工作，必须先启动HDFS且等安全模式结束才可以使用你的软件。
- 启动-->启动成功-->==可用==（安全模式结束）

### 3.3.8. 元数据管理机制

元数据

```shell
元数据（Metadata），又称中介数据、中继数据，为描述数据的数据（data about data），主要是描述数据属性（property）的信息，用来支持如指示存储位置、历史数据、资源查找、文件记录等功能。

#记录数据的数据 描述数据的数据
```

HDFS元数据，按类型分，主要包括以下几个部分： 

1、文件、目录自身的属性信息，例如文件名，目录名，修改信息等。 

2、文件记录的信息的存储相关的信息，例如存储块信息，分块情况，副本个数等。 

3、记录HDFS的Datanode的信息，用于DataNode的管理。

按形式分为内存元数据和元数据文件两种，分别存在内存和磁盘上。

HDFS磁盘上元数据文件分为两类，用于持久化存储：

fsimage 镜像文件：是元数据的一个持久化的检查点，包含Hadoop文件系统中的所有目录和文件元数据信息，但不包含文件块位置的信息。文件块位置信息只存储在内存中，是在 datanode加入集群的时候，namenode询问datanode得到的，并且间断的更新。

Edits 编辑日志：存放的是Hadoop文件系统的所有更改操作（文件创建，删除或修改）的日志，文件系统客户端执行的更改操作首先会被记录到edits文件中。

fsimage和edits文件都是经过序列化的，在NameNode启动的时候，它会将fsimage文件中的内容加载到内存中，之后再执行edits文件中的各项操作，使得内存中的元数据和实际的同步，存在内存中的元数据支持客户端的读操作，也是最完整的元数据。

当客户端对HDFS中的文件进行新增或者修改操作，操作记录首先被记入edits日志文件中，当客户端操作成功后，相应的元数据会更新到内存元数据中。因为fsimage文件一般都很大（GB级别的很常见），如果所有的更新操作都往fsimage文件中添加，这样会导致系统运行的十分缓慢。

HDFS这种设计实现着手于：一是内存中数据更新、查询快，极大缩短了操作响应时间；二是内存中元数据丢失风险颇高（断电等），因此辅佐元数据镜像文件（fsimage）+编辑日志文件（edits）的备份机制进行确保元数据的安全。

**NameNode维护整个文件系统元数据**。因此，元数据的准确管理，影响着HDFS提供文件存储服务的能力。

**元数据相关目录文件**

回想首次启动HDFS集群的时候 进行format操作

- 本质就是初始化操作  初始化namenode工作目录和元数据文件。

- 元数据存储的目录由参数dfs.namenode.name.dir决定  在NN部署机器的本地linux文件系统中

  ```
  最终目录
  
  /export/data/hadoopdata/dfs/name
  ```

#### 3.3.8.1. secondary namenode合并元数据

当HDFS集群运行一段事件后，就会出现下面一些问题：

- edit logs文件会变的很大，怎么去管理这个文件是一个挑战。

- NameNode重启会花费很长时间，因为有很多改动要合并到fsimage文件上。

- 如果NameNode挂掉了，那就丢失了一些改动。因为此时的fsimage文件非常旧。

因此为了克服这个问题，我们需要一个易于管理的机制来帮助我们**减小edit logs文件的大小和得到一个最新的fsimage文件**，这样也会减小在NameNode上的压力。这跟Windows的恢复点是非常像的，Windows的恢复点机制允许我们对OS进行快照，这样当系统发生问题时，我们能够回滚到最新的一次恢复点上。

SecondaryNameNode就是来帮助解决上述问题的，它的职责是合并NameNode的edit logs到fsimage文件中。

**Checkpoint**

每达到触发条件，会由secondary namenode将namenode上积累的所有edits和一个最新的fsimage下载到本地，并加载到内存进行merge（这个过程称为checkpoint），如下图所示：

![SNN Checkpoint](images\SNN Checkpoint.png)

**Checkpoint详细步骤**

1. NameNode管理着元数据信息，其中有两类持久化元数据文件：edits操作日志文件和fsimage元数据镜像文件。新的操作日志不会立即与fsimage进行合并，也不会刷到NameNode的内存中，而是会先写到edits中(因为合并需要消耗大量的资源)，操作成功之后更新至内存。

2. 有dfs.namenode.checkpoint.period和dfs.namenode.checkpoint.txns 两个配置，只要达到这两个条件任何一个，secondarynamenode就会执行checkpoint的操作。

3. 当触发checkpoint操作时，NameNode会生成一个新的edits即上图中的edits.new文件，同时SecondaryNameNode会将edits文件和fsimage复制到本地（HTTP GET方式）。

4. secondarynamenode将下载下来的fsimage载入到内存，然后一条一条地执行edits文件中的各项更新操作，使得内存中的fsimage保存最新，这个过程就是edits和fsimage文件合并，生成一个新的fsimage文件即上图中的Fsimage.ckpt文件。

5. secondarynamenode将新生成的Fsimage.ckpt文件复制到NameNode节点。

6. 在NameNode节点的edits.new文件和Fsimage.ckpt文件会替换掉原来的edits文件和fsimage文件，至此刚好是一个轮回，即在NameNode中又是edits和fsimage文件。

7. 等待下一次checkpoint触发SecondaryNameNode进行工作，一直这样循环操作。

### 3.3.9. MapReduce（MR）

核心：==**先分再合，分而治之**==。

步骤

- 分的阶段（==**局部并行计算**==）--map

  ```shell
  把复杂的任务拆分成若干个小的任务。
  拆分的目的以并行方式处理小任务提高效率。
  
  #前提：任务可以拆分，拆分之后没有依赖关系。
  结果：每个任务处理完都是一个局部的结果。
   
  map侧重于映射（对应关系）  任务1-->结果1  任务2-->结果2
  ```

- 汇总阶段（**==全局汇总计算==**）--reduce

  ```
  把上一个分的阶段局部结果进行全局汇总 得到最终结果。
  
  reduce指的是结果数量的减少 汇总。
  ```

**单词统计(WordCount)需求剖析**

背景

```
网页倒排索引 统计关键字在页面中出现的次数。
```

业务需求

```
统计文件中每个单词出现的总次数。
```

实现思路

![MR实现思路](images\MR实现思路.png)

> map阶段的核心：把输入的数据经过切割，全部标记1，因此输出就是<单词，1>。
>
> shuffle阶段核心：经过默认的排序分区分组，key相同的单词会作为一组数据构成新的key-value对。
>
> reduce阶段核心：处理shuffle完的一组数据，该组数据就是该单词所有的键值对。对所有的1进行累加求和，就是单词的总次数。
>
> 读取数据组件  写出数据组件MR框架已经封装好（自带）

程序提交

```shell
#上传的文本文件1.txt到HDFS文件系统的/input目录下，如果没有这个目录，使用shell创建
	hadoop fs -mkdir /input	
	hadoop fs -put 1.txt /input

#准备好之后，执行官方MapReduce实例，对上述文件进行单词次数统计
	第一个参数：wordcount表示执行单词统计任务；
	第二个参数：指定输入文件的路径；
	第三个参数：指定输出结果的路径（该路径不能已存在）
	

[root@node1 mapreduce]# pwd
/export/server/hadoop-3.3.0/share/hadoop/mapreduce

[root@node1 mapreduce]# hadoop jar hadoop-mapreduce-examples-3.3.0.jar wordcount /input /output
```

#### 3.3.9.1. Hadoop Streaing提交python脚本

Python3在Linux安装

```shell
#1、安装编译相关工具
yum -y groupinstall "Development tools"

yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel

yum install libffi-devel -y

#2、解压Python安装包
tar -zxvf  Python-3.8.5.tgz

#3、编译、安装Python
mkdir /usr/local/python3 #创建编译安装目录
cd Python-3.8.5
./configure --prefix=/usr/local/python3
make && make install  #make编译c源码 make install 编译后的安装

#安装过，出现下面两行就成功了
Installing collected packages: setuptools, pip
Successfully installed pip-20.1.1 setuptools-47.1.0


#4、创建软连接
# 查看当前python软连接
[root@node2 Python-3.8.5]# ll /usr/bin/ |grep python
-rwxr-xr-x.   1 root root      11232 Aug 13  2019 abrt-action-analyze-python
lrwxrwxrwx.   1 root root          7 May 17 11:36 python -> python2
lrwxrwxrwx.   1 root root          9 May 17 11:36 python2 -> python2.7
-rwxr-xr-x.   1 root root       7216 Aug  7  2019 python2.7


#默认系统安装的是python2.7 删除python软连接
rm -rf /usr/bin/python

#配置软连接为python3
ln -s /usr/local/python3/bin/python3 /usr/bin/python

#这个时候看下python默认版本
python -V

#删除默认pip软连接，并添加pip3新的软连接
rm -rf /usr/bin/pip
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip


#5、更改yum配置
#因为yum要用到python2才能执行，否则会导致yum不能正常使用（不管安装 python3的那个版本，都必须要做的）
vi /usr/bin/yum 
把 #! /usr/bin/python 修改为 #! /usr/bin/python2 

vi /usr/libexec/urlgrabber-ext-down 
把 #! /usr/bin/python 修改为 #! /usr/bin/python2

vi /usr/bin/yum-config-manager
#!/usr/bin/python 改为 #!/usr/bin/python2
```

代码部分：

- mapper.py

  ```python
  import sys
  
  for line in sys.stdin:
      # 捕获输入流
      line = line.strip()
      # 根据分隔符切割单词
      words = line.split()
      # 遍历单词列表 每个标记1
      for word in words:
          print("%s\t%s" % (word, 1))
  ```

- reducer.py

  ```python
  import sys
  # 保存单词次数的字典 key:单词 value：总次数
  word_dict = {}
  
  for line in sys.stdin:
  
      line = line.strip()
      word, count = line.split('\t')
  
      # count类型转换
      try:
          count = int(count)
      except ValueError:
          continue
      # 如果单词位于字典中 +1，如果不存在 保存并设初始值1
      if word in word_dict:
          word_dict[word] += 1
      else:
          word_dict.setdefault(word, 1)
  # 结果遍历输出
  for k, v in word_dict.items():
      print('%s\t%s' % (k, v))
  ```



代码的本地测试

```shell
#上传待处理文件 和Python脚本到Linux上
[root@node2 ~]# pwd
/root
[root@node2 ~]# ll
-rw-r--r--  1 root  root        105 May 18 15:12 1.txt
-rwxr--r--  1 root  root        340 Jul 21 16:16 mapper.py
-rwxr--r--  1 root  root        647 Jul 21 16:18 reducer.py


#使用shell管道符运行脚本测试
[root@node2 ~]# cat 1.txt | python mapper.py |sort|python reducer.py 
allen   4
apple   3
hadoop  1
hello   5
mac     1
spark   2
tom     2
```

代码提交集群执行

```shell
#上传处理的文件到hdfs
#上传Python脚本到linux

#提交程序执行
hadoop jar /export/server/hadoop-3.3.0/share/hadoop/tools/lib/hadoop-streaming-3.3.0.jar \
-D mapred.reduce.tasks=1 \
-mapper "python mapper.py" \
-reducer "python reducer.py" \
-file mapper.py -file reducer.py \
-input /wordcount/input/* \
-output /wordcount/outputpy
```



### 3.3.10. YARN集群

物理层面上-2个组件

- 主角色 ==resourcemanager== RM

  ```
  ResourceManager 负责整个集群的资源管理和分配，是一个全局的资源管理系统。
  是程序申请资源的唯一入口 负载调度。
  ```

- 从角色 ==nodemanager==  NM

  ```
  nodemanager 负责每台机器上具体的资源管理 负责启动 关闭container容器
  ```

程序内部--1个组件

- ==ApplicationMaster==  AM

```shell
yarn作为通用资源管理系统 不关心程序的种类和程序内部的执行情

#为了解决这个问题 yarn提供了第三个组件 applicationmaster 

#把applicationmaster称之为程序内部的老大角色 负责程序内部的执行情况

#AM针对不同类型的程序有不同的具体实现
yarn默认实现了MapReduce的AM  名字叫做MrAppMaster.
其他软件比如spark flink需要实现自己的AM 才能在yarn运行。

#结论：在上述设计模式下  任何种类程序在yarn运行，首先都是申请资源运行AM角色，然后由AM控制程序内部具体的执行。
```

#### 3.3.10.1. MR与YARN的交互流程

![MR与YARN交互流程](images\MR与YARN交互流程.png)

1. 客户端连接RM，请求资源运行本次程序的AM。
2. RM指定NM预留资源，配合客户端启动容器container。
3. AM启动并向RM进行注册，保持通信。
4. AM根据切片个数向RM申请与之对应的容器进行maptask。
5. AM根据申请的容器到各个机器上与NM配合启动容器运行maptask并监督其执行情况。
6. AM根据Reducetask个数申请容器并运行，过程同上
7. 整个MR程序执行过程中，都是AM在申请资源、监督执行并把执行情况汇报给RM。

> 总结：
>
> YARN只负责分配资源、回收资源，不负责程序内部的逻辑
>
> 不管是客户端、还是AM，只要向申请新的资源，必须找RM，因为RM才是资源分配的唯一仲裁者
>
> 真正负责操心程序内部执行情况的是AM，每个程序都有自己的AM

#### 3.3.10.2. YARN调度策略

理想情况下，我们应用对Yarn资源的请求应该立刻得到满足，但现实情况资源往往是有限的，特别是在一个很繁忙的集群，一个应用资源的请求经常需要等待一段时间才能的到相应的资源。在**Yarn中，负责给应用分配资源的就是Scheduler**。其实调度本身就是一个难题，很难找到一个完美的策略可以解决所有的应用场景。为此，Yarn提供了多种调度器和可配置的策略供我们选择。

在Yarn中有三种调度器可以选择：FIFO Scheduler ，Capacity Scheduler，Fair Scheduler。

**FIFO** Scheduler把应用按提交的顺序排成一个队列，这是一个**先进先出**队列，在进行资源分配的时候，先给队列中最头上的应用进行分配资源，待最头上的应用需求满足后再给下一个分配，以此类推。

Capacity 调度器允许多个组织共享整个集群，每个组织可以获得集群的一部分计算能力。通过为每个组织分配专门的队列，然后再为每个队列分配一定的集群资源，这样整个集群就可以通过设置多个队列的方式给多个组织提供服务了。除此之外，队列内部又可以垂直划分，这样一个组织内部的多个成员就可以共享这个队列资源了，在一个队列内部，资源的调度是采用的是先进先出(FIFO)策略。

在Fair调度器中，我们不需要预先占用一定的系统资源，Fair调度器会为所有运行的job动态的调整系统资源。如下图所示，当第一个大job提交时，只有这一个job在运行，此时它获得了所有集群资源；当第二个小任务提交后，Fair调度器会分配一半资源给这个小任务，让这两个任务公平的共享集群资源。

需要注意的是，在下图Fair调度器中，从第二个任务提交到获得资源会有一定的延迟，因为它需要等待第一个任务释放占用的Container。小任务执行完成之后也会释放自己占用的资源，大任务又获得了全部的系统资源。最终效果就是Fair调度器即得到了高的资源利用率又能保证小任务及时完成。

### 3.3.11. HA集群

**HDFS HA**

![](images\HDFS HA.png)

Hadoop中单点故障

- NameNode
- Resourcemanager

NameNode HA ---==QJM共享日志集群方案==

- zkfc 实现主备切换避免脑裂
- jn集群 editslog编辑日志同步



**YARN HA**

![](images\YARN HA.png)

Resourcemanager HA --基于zk实现

- RM需要维护的数据量很少 不像NN需要同步文件系统大量的元数据。直接基于zk即可完成
- zk也是一个分布式小文件存储系统。



# 四、Apache Hive

## 4.1. 数仓

数据仓库，中文简称==数仓==。英文叫做Data WareHouse,简称==DW==。

数据仓库是==**面向分析**==的集成化数据平台，分析的结果给企业提供==**决策支持**==；

数据仓库本身不生产数据；

```
其分析的数据来自于企业各种数据源。
企业中常见的数据源：
	RDBMS关系型数据库--->业务数据
	log file----->日志文件数据
	爬虫数据
	其他数据
```

数据仓库本身也不消费数据；

```
其分析的结果给外部各种数据应用（Data application）来使用。

Data visualization（DV）数据可视化
Data Report 数据报表
Data Mining(DM) 数据挖掘
Ad-Hoc 即席查询

	即席查询（Ad Hoc）是用户根据自己的需求，灵活的选择查询条件，系统能够根据用户的选择生成相应的统计报表。即席查询与普通应用查询最大的不同是普通的应用查询是定制开发的，而即席查询是由用户自定义查询条件的。
```

企业中一般==先有数据库，然后有数据仓库，可以没有数据仓库，但是不能没有数据库==。

数据仓库不是大型的数据库，只是一个数据分析的平台。

### 4.1.1. 数仓分层结构

![](images\数仓分层结构.png)

数仓本身不生产数据也不消费数据，按照数据流入流出的特点，对平台进行分层

最基础最核心的3层架构，企业实际应用中，可以结合需要添加不同分层。

核心3层架构

- ==**ODS 操作型数据层**==、源数据层、临时存储层

  ```
  其数据来自于各个不同的数据源 临时存储 和数据源解耦合 之间有差异 一般不直接用于分析
  
  Operational Data Store
  ```

- ==**DW 数据仓库**==

  ```
  其数据来自于ODS经过层层的ETL变成各种模型的数据  数据干净规则 统一
  基于各种模型开展各种分析
  
  企业中根据业务复杂度 继续在DW中继续划分子层。 存储大量的中间结果。其数据来自于ODS经过层层ETL得出 企业中可以根据需求在DW中继续分层。
  
  Data Warehouse
  ```

- ==**DA 数据应用层**==

  ```
  最终消费DW数据的各种应用。
  
  Data Application 
  ```

==分层好处==

- ==清晰数据结构==

  每一个数据分层都有它的作用域，在使用表的时候能更方便地定位和理解

- ==数据血缘追踪==

  简单来说，我们最终给业务呈现的是一个能直接使用业务表，但是它的来源有很多，如果有一张来源表出问题了，我们希望能够快速准确地定位到问题，并清楚它的危害范围。

- ==减少重复开发==

  规范数据分层，开发一些通用的中间层数据，能够减少极大的重复计算。

- ==把复杂问题简单化==

  将一个复杂的任务分解成多个步骤来完成，每一层只处理单一的步骤，比较简单和容易理解。而且便于维护数据的准确性，当数据出现问题之后，可以不用修复所有的数据，只需要从有问题的步骤开始修复。

- ==屏蔽原始数据的异常==

  屏蔽业务的影响，不必改一次业务就需要重新接入数据

## 4.2. Hive架构、组件

![](images\Hive 架构.png)

Hive的架构组件

- ==客户端用户接口==

  ```
  所谓的客户端指的是给用户一种方式编写Hive SQL
  目前常见的客户端：CLI（命令行接口 shell）、Web UI、JDBC|ODBC
  ```

- ==Hive Driver驱动程序==

  ```
  hive的核心
  完成从接受HQL到编译成为MR程序的过程。
  sql解释 编译 校验 优化 制定计划
  ```

- ==metadata==

  ```
  元数据存储。 描述性数据。
  对于hive来说，元数据指的是表和文件之间的映射关系。
  ```

- Hadoop

  ```
  HDFS  存储文件
  MapReduce 计算数据
  YARN  程序运行的资源分配
  ```

- Q:Hive是分布式的软件吗？

  ```
  Hive不是分布式软件。只需要在一台机器上部署Hive服务即可；
  Hive的分布式处理能力是借于Hadoop完成的。HDFS分布式存储  MapReduce分布式计算。
  ```

Hive和Mysql的区别

- 从外表、形式模型、语法各层面上看 ，hive和数据库（Mysql）很类似。
- 底层应用场景是完全不一样的。
- hive属于olap系统 是面向分析的侧重于数据分析（select）
- 数据库属于oltp系统 是面向事务的 侧重于数据时间交互（CRUD）
- ==Hive绝不是大型数据库 也不是为了要取代MySQL这样的数据库==。

## 4.3. Hive metadata

![](images\Hive metadata.png)

Metadata 元数据
对于hive来说，元数据主要指的是表和文件之间的映射关系。
元数据也是数据，存储在哪里呢？Hive当下支持两种地方存储元数据。
	1、存储在Hive内置的RDBSM中，Apache Derby(内存级别轻量级关系型数据库)  
	2、存储在外界第三方的RDBMS中，比如：MySQL。  企业中常用的方式。

metastore 元数据访问服务
专门用于操作访问metadata的一种服务，对外暴露服务地址给各个不同的客户端使用访问Hive的元数据。
并且某种程度上保证了metadata的安全。

## 4.4. Hive三种部署模式

==**内嵌模式**==

```
1、元数据存储在内置的derby
2、不需要单独配置metastore 也不需要单独启动metastore服务

安装包解压即可使用。

适合测试体验。实际生产中没人用。适合单机单人使用。
```

![](images\Hive内嵌模式.png)

==**本地模式**==

```
1、元数据使用外置的RDBMS，常见使用最多的是MySQL。
2、不需要单独配置metastore 也不需要单独启动metastore服务
```

![](images\Hive本地模式.png)

==**远程模式**==

```
1、元数据使用外置的RDBMS，常见使用最多的是MySQL。
2、metastore服务单独配置  单独手动启动  全局唯一。

这样的话各个客户端只能通过这一个metastore服务访问Hive.

企业生产环境中使用的模式，支持多客户端远程并发操作访问Hive.
```

![](images\Hive远程模式.png)

对比

|              | metadata存储在哪 | metastore服务如何      |
| ------------ | ---------------- | ---------------------- |
| 内嵌模式     | Derby            | 不需要配置启动         |
| 本地模式     | MySQL            | 不需要配置启动         |
| ==远程模式== | ==MySQL==        | ==单独配置、单独启动== |

## 4.5. 安装部署、初始化

安装Hive (==选择node1安装==)

```shell
panache-hive-3.1.2-bin.tar.gz

上传、解压
tar zxvf apache-hive-3.1.2-bin.tar.gz
```

0、解决Hive与Hadoop之间guava版本差异

```shell
cd /export/server/apache-hive-3.1.2-bin/
rm -rf lib/guava-19.0.jar
cp /export/server/hadoop-3.3.0/share/hadoop/common/lib/guava-27.0-jre.jar ./lib/
```

1、==hive-env.sh==

```shell
cd /export/server/apache-hive-3.1.2-bin/conf
mv hive-env.sh.template hive-env.sh

vim hive-env.sh
export HADOOP_HOME=/export/server/hadoop-3.3.0
export HIVE_CONF_DIR=/export/server/apache-hive-3.1.2-bin/conf
export HIVE_AUX_JARS_PATH=/export/server/apache-hive-3.1.2-bin/lib
```

2、==hive-site.xml==

vim hive-site.xml

```xml
<configuration>
<!-- 存储元数据mysql相关配置 -->
<property>
	<name>javax.jdo.option.ConnectionURL</name>
	<value>jdbc:mysql://node1:3306/hive3?createDatabaseIfNotExist=true&amp;useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8</value>
</property>
<property>
	<name>javax.jdo.option.ConnectionDriverName</name>
	<value>com.mysql.jdbc.Driver</value>
</property>

<property>
	<name>javax.jdo.option.ConnectionUserName</name>
	<value>root</value>
</property>

<property>
	
<!-- MySQL密码 --><name>javax.jdo.option.ConnectionPassword</name>
	<value>123456</value>
</property>

<!-- H2S运行绑定host -->
<property>
    <name>hive.server2.thrift.bind.host</name>
    <value>node1</value>
</property>

<!-- 远程模式部署metastore metastore地址 -->
<property>
  <name>hive.metastore.uris</name>
    <value>thrift://node1:9083</value>
</property>

<!-- 关闭元数据存储授权  --> 
<property>
  <name>hive.metastore.event.db.notification.api.auth</name>
    <value>false</value>
</property>
</configuration>

```

3、上传Mysql jdbc驱动到Hive安装包的==Lib目录==下

```
mysql-connector-java-5.1.32.jar
```

4、手动执行命令初始化Hive的元数据

```shell
cd /export/server/apache-hive-3.1.2-bin/

bin/schematool -initSchema -dbType mysql -verbos
#初始化成功会在mysql中创建74张表
```

## 4.6. metastore服务启动

### 4.6.1. 第一代客户端（Hive客户端）

==metastore服务==

前台启动

```shell
#前台启动
/export/server/apache-hive-3.1.2-bin/bin/hive --service metastore

#前台启动开启debug日志
/export/server/apache-hive-3.1.2-bin/bin/hive --service metastore --hiveconf hive.root.logger=DEBUG,console  

#前台启动关闭方式  ctrl+c结束进程
```

后台挂起启动

```shell
nohup /export/server/apache-hive-3.1.2-bin/bin/hive --service metastore &

#后台挂起启动 结束进程
使用jps查看进程 使用kill -9 杀死进程

#nohup 命令，在默认情况下（非重定向时），会输出一个名叫 nohup.out 的文件到当前目录下
```

==Hive的客户端==

Hive的第一代客户端

==**bin/hive**==

直接访问metastore服务

配置

```xml
<configuration>
<property>
        <name>hive.metastore.uris</name>
        <value>thrift://node1:9083</value>
</property>
</configuration>
```

弊端：

```
第一代客户端属于shell脚本客户端 性能友好安全方面存在不足 Hive已经不推荐使用
```

官方建议使用第二代客户端beeline

### 4.6.2. 第二代客户端（beeline客户端）

Hive的第二代客户端

![](images\Hive的第一代和第二代客户端、HS2服务.png)

bin/beeline

无法访问metastore服务，只能够访问==Hiveserver2服务==。

使用

```shell
# 拷贝node1上 hive安装包到beeline客户端机器上（node3）
scp -r /export/server/apache-hive-3.1.2-bin/ node3:/export/server/

#1、在安装hive的服务器上 首先启动metastore服务 再启动hiveserver2服务
nohup /export/server/apache-hive-3.1.2-bin/bin/hive --service metastore &
nohup /export/server/apache-hive-3.1.2-bin/bin/hive --service hiveserver2 &

#2、在任意机器(如node3)上使用beeline客户端访问
[root@node3 ~]# /export/server/apache-hive-3.1.2-bin/bin/beeline                   
beeline> ! connect jdbc:hive2://node1:10000    #jdbc访问HS2服务
Connecting to jdbc:hive2://node1:10000
Enter username for jdbc:hive2://node1:10000: root  #用户名 要求具备HDFS读写权限
Enter password for jdbc:hive2://node1:10000:       #密码可以没有
```

## 4.7. HQL

### 4.7.1. 数据类型

Hive中的数据类型指的是Hive表中的列字段类型。Hive数据类型整体分为两个类别：**原生数据类型**（primitive data type）和**复杂数据类型**（complex data type）。

原生数据类型包括：数值类型、时间类型、字符串类型、杂项数据类型；

复杂数据类型包括：array数组、map映射、struct结构、union联合体。

关于Hive的数据类型，需要注意：

英文字母大小写不敏感；

除SQL数据类型外，还支持Java数据类型，比如：string；

int和string是使用最多的，大多数函数都支持；

复杂数据类型的使用通常需要和分隔符指定语法配合使用。

如果定义的数据类型和文件不一致，hive会尝试隐式转换，但是不保证成功。原生类型从窄类型到宽类型的转换称为隐式转换，反之，则不允许。

隐式转换：

![](images\隐式转换.png)

原生数据类型：

![](images\HQL原生数据类型.png)

复杂数据类型：

![](images\HQL复杂数据类型.png)

### 4.7.2. HQL读写文件机制

SerDe是Serializer、Deserializer的简称，目的是用于序列化和反序列化。序列化是对象转化为字节码的过程；而反序列化是字节码转换为对象的过程。

Hive使用SerDe（和FileFormat）读取和写入行对象。

> Read：
>
> HDFS Files --> InputFileFormat --> <key, value> --> Deserializer(反序列化) --> Row object

> Write:
>
> Row object --> Serializer(序列化) --> <key, value> --> OutputFileFormat --> HDFS files

### 4.7.3. DDL

**完整语法**

![](images\DDL完整语法.png)

> 蓝色字体是建表语法的关键字，用于指定某些功能。
> [ ]中括号的语法表示可选。
> |表示使用的时候，左右语法二选一。
> 建表语句中的语法顺序要和语法树中顺序保持一致。



**分隔符指定语法**

语法格式

```sql
ROW FORMAT DELIMITED | SERDE

ROW FORMAT DELIMITED  表示使用LazySimpleSerDe类进行序列化解析数据
 
ROW FORMAT SERDE      表示使用其他SerDe类进行序列化解析数据
```

ROW FORMAT DELIMITED具体的子语法

```shell
row format delimited
[fields terminated by char]  #指定字段之间的分隔符
[collection items terminated by char]  #指定集合元素之间的分隔符
[map keys terminated by char]         #指定map类型kv之间的分隔符
[lines terminated by char]            #指定换行符
```

**默认分隔符**

Hive在建表的时候，如果没有row format语法，则该表使用==\001默认分隔符==进行字段分割；

如果此时文件中的数据字段之间的分隔符也是\001 ，那么就可以直接映射成功。

==针对默认分隔符，其是一个不可见分隔符，在代码层面是\001表示==

在vim编辑器中，连续输入ctrl+v 、ctrl+a；

在实际工作中，Hive最喜欢的就是\001分隔符，在清洗数据的时候，==有意识==的把数据之间的分隔符指定为\001;

### 4.7.4. Hive中的表种类

#### 4.7.4.1. 外部表、内部表

```sql
--创建内部表
create table student_inner(Sno int,Sname string,Sex string,Sage int,Sdept string) row format delimited fields terminated by ',';

--创建外部表 关键字external
create external table student_external(Sno int,Sname string,Sex string,Sage int,Sdept string) row format delimited fields terminated by ',';

--上传文件到内部表、外部表中
hadoop fs -put students.txt /user/hive/warehouse/itheima.db/student_inner
hadoop fs -put students.txt /user/hive/warehouse/itheima.db/student_external

--针对内部表、外部表 进行drop删除操作
drop table student_inner;  --内部表在删除的时候 元数据和数据都会被删除
drop table student_external; --外部表在删除的时候 只删除元数据  而HDFS上的数据文件不会动
```

可以通过命令去查询表的元数据信息 获取表的类型

```sql
desc formatted table_name;

MANAGED_TABLE     内部表、受控表(所谓的受控指定是表对应的HDFS上的数据受到我的控制)
EXTERNAL_TABLE    外部表
```



#### 4.7.4.2. 分区表

分区表（Partitioned Table）是一种数据组织结构，用于将表的数据按照特定的列值划分为多个分区（Partitions）。每个分区相当于一个独立的子目录，其中包含符合特定分区条件的数据。

分区表的主要目的是提高查询效率和数据管理的灵活性。通过将数据按照某个列的值进行分区，可以将数据划分为更小的数据块，这样在查询时可以仅扫描特定分区的数据，而无需扫描整个表。这种分区方式能够显著减少查询的数据量，提高查询性能。

分区表在 Hive 中的创建和使用都需要指定分区列，这个列可以是表中的任意列，通常是与查询条件经常相关的列。例如，如果有一个包含销售数据的表，你可以按照日期列对其进行分区，每个分区代表一天的销售数据。

创建分区表时，需要使用 `PARTITIONED BY` 子句指定分区列的定义。例如：

```sql
# 创建分区表
CREATE TABLE sales (
  id INT,
  product STRING,
  transaction_date STRING,
  amount DOUBLE
)
PARTITIONED BY (sale_date STRING);

# 静态加载数据到分区表
load data local inpath '/root/hivedata/sale_date.txt' into table sales partition(sale_date='2023-06-20');

load data local inpath '/root/hivedata/sale_date.txt' into table sales partition(sale_date='2023-06-21');

load data local inpath '/root/hivedata/sale_date.txt' into table sales partition(sale_date='2023-06-22');
```

在这个例子中，`sales` 表是一个分区表，根据 `sale_date` 列进行分区。

并将3天数据分为三个分区，静态加载到分区表中，但静态分区不适用于动态变化的分区，例如按日期分区，每天都有新的分区创建。

在查询分区表时，可以使用 `WHERE` 子句指定特定的分区条件来过滤数据。例如：

```sql
SELECT * FROM sales WHERE sale_date = '2023-06-20';
```

这将只返回 `sale_date` 列等于 `'2023-06-20'` 的数据，而不会扫描整个表的数据。

通过使用分区表，可以更有效地管理和查询大型数据集，提高数据查询性能和灵活性。同时，需要注意在设计和使用分区表时需要根据具体业务需求和查询模式进行合理的分区策略选择。



**动态分区插入数据**

设置允许动态分区、设置动态分区模式

```sql
--动态分区
set hive.exec.dynamic.partition=true; --注意hive3已经默认开启了
set hive.exec.dynamic.partition.mode=nonstrict;

--模式分为strict严格模式  nonstrict非严格模式
严格模式要求 分区字段中至少有一个分区是静态分区。


--举个栗子
set hive.exec.dynamic.partition.mode=strict;  --设置为严格模式


Error: Error while compiling statement: FAILED: SemanticException [Error 10096]: Dynamic partition strict mode requires at least one static partition column. To turn this off set hive.exec.dynamic.partition.mode=nonstrict (state=42000,code=10096)

--说动态分区在严格模式下 要求至少有一个分区字段为静态分区字段  
--如果不想这么做  就必须把模式设置为非严格


t_1(xxxx) partitioned by (month string,day string);

insert into t_1  partition(month="202112",day="18") -- 两个分区字段都是静态
insert into t_1  partition(month="202112",day)
insert into t_1  partition(month,day="18")   --至少一个是静态的
insert into t_1  partition(month,day)  --都是动态的
```

动态分区加载数据

> ==insert + select== 
>
> 插入的数据来自于后面的查询语句返回的结果。
>
> 查询返回的内容，其字段类型、顺序、个数要和待插入的表保持一致。

```sql
--创建一张新的分区表 t_all_hero_part_dynamic
create table t_all_hero_part_dynamic(
    id int,
    name string,
    hp_max int,
    mp_max int,
    attack_max int,
    defense_max int,
    attack_range string,
    role_main string,
    role_assist string
) partitioned by (role_dong string)
row format delimited
fields terminated by "\t";

--执行动态分区插入  --注意 分区值并没有手动写死指定
insert into table t_all_hero_part_dynamic partition(role_dong) 
select tmp.*,tmp.role_main from t_all_hero tmp; --查询返回10个字段


--查询验证结果
select * from t_all_hero_part_dynamic;

---严格模式下报错信息
Dynamic partition strict mode requires at least one static partition column. To turn this off set hive.exec.dynamic.partition.mode=nonstrict
```

> 在执行动态分区插入数据的时候，如果是严格模式strict，要求至少一个分区为静态分区？
>
> partition(guojia="zhongguo",sheng) --第一个分区写死了（静态） 符合严格模式。
>
> partition(guojia,sheng)  --两个分区都是动态确定的  需要非严格模式

分区表的使用--分区裁剪

```sql
--非分区表 全表扫描过滤查询
select count(*) from t_all_hero where role_main="archer" and hp_max >6000;

--分区表 先基于分区过滤 再查询
select count(*) from t_all_hero_part where juesedingwei="sheshou" and hp_max >6000;
```

#### 4.7.4.3. 分桶表

从语法层面解析分桶含义

```sql
CLUSTERED BY xxx INTO N BUCKETS
--根据xxx字段把数据分成N桶
--根据表中的字段把数据文件成为N个部分

t_user(id int,name string);
--1、根据谁分？
 CLUSTERED BY xxx ；  xxx必须是表中的字段
--2、分成几桶？
 N BUCKETS   ；N的值就是分桶的个数
--3、分桶的规则？
clustered by id into 3 bucket

hashfunc(分桶字段)  %  N bucket  余数相同的来到同一个桶中
1、如果分桶的字段是数字类型的字段，hashfunc(分桶字段)=分桶字段本身
2、如果分桶的字段是字符串或者其他字段，hashfunc(分桶字段) = 分桶字段.hashcode
```

分桶的创建

```sql
CREATE TABLE itheima.t_usa_covid19_bucket(
      count_date string,
      county string,
      state string,
      fips int,
      cases int,
      deaths int)
CLUSTERED BY(state) INTO 5 BUCKETS; --分桶的字段一定要是表中已经存在的字段

--根据state州分为5桶 每个桶内根据cases确诊病例数倒序排序
CREATE TABLE itheima.t_usa_covid19_bucket_sort(
     count_date string,
     county string,
     state string,
     fips int,
     cases int,
     deaths int)
CLUSTERED BY(state)
sorted by (cases desc) INTO 5 BUCKETS;--指定每个分桶内部根据 cases倒序排序
```

分桶表的数据加载

```sql
--step1:开启分桶的功能 从Hive2.0开始不再需要设置
set hive.enforce.bucketing=true;

--step2:把源数据加载到普通hive表中
CREATE TABLE itheima.t_usa_covid19(
       count_date string,
       county string,
       state string,
       fips int,
       cases int,
       deaths int)
row format delimited fields terminated by ",";

--将源数据上传到HDFS，t_usa_covid19表对应的路径下
hadoop fs -put us-covid19-counties.dat /user/hive/warehouse/itheima.db/t_usa_covid19

--step3:使用insert+select语法将数据加载到分桶表中
insert into t_usa_covid19_bucket select * from t_usa_covid19;

select * from t_usa_covid19_bucket limit 10;
```

分桶表的使用

```sql
--基于分桶字段state查询来自于New York州的数据
--不再需要进行全表扫描过滤
--根据分桶的规则hash_function(New York) mod 5计算出分桶编号
--查询指定分桶里面的数据 就可以找出结果  此时是分桶扫描而不是全表扫描
select *
from t_usa_covid19_bucket where state="New York";
```

> 分桶表也是一种优化表，可以**==减少join查询时笛卡尔积的数量==**、==提高抽样查询的效率==。
>
> 分桶表的字段必须是表中已有的字段；
>
> 分桶表需要使用间接的方式才能把数据加载进入：insert+select 
>
> 在join的时候，针对join的字段进行分桶，可以提高join的效率 减少笛卡尔积数量。

### 4.7.5. DDL其他操作

> 因为Hive建表、加载数据及其方便高效；在实际的应用中，==如果建表有问题，通常可以直接drop删除重新创建加载数据==。时间成本极低。
>
> 如果表是外部表的话，更加完美了。

Database 数据库 DDL操作

```sql
--创建数据库
create database if not exists itcast
comment "this is my first db"
with dbproperties ('createdBy'='Allen');

--描述数据库信息
describe database itcast;
describe database extended itcast;
desc database extended itcast;

--切换数据库
use default;
use itcast;
create table t_1(id int);

--删除数据库
--注意 CASCADE关键字慎重使用
DROP (DATABASE|SCHEMA) [IF EXISTS] database_name [RESTRICT|CASCADE];
drop database itcast cascade ;


--更改数据库属性
ALTER (DATABASE|SCHEMA) database_name SET DBPROPERTIES (property_name=property_value, ...);
--更改数据库所有者
ALTER (DATABASE|SCHEMA) database_name SET OWNER [USER|ROLE] user_or_role;
--更改数据库位置
ALTER (DATABASE|SCHEMA) database_name SET LOCATION hdfs_path;
```

Table 表 DDL操作

```sql
--下面这两个需要记住
--查询指定表的元数据信息
desc formatted itheima.t_all_hero_part;
show create table t_all_hero_part;

--1、更改表名
ALTER TABLE table_name RENAME TO new_table_name;
--2、更改表属性
ALTER TABLE table_name SET TBLPROPERTIES (property_name = property_value, ... );
--更改表注释
ALTER TABLE student SET TBLPROPERTIES ('comment' = "new comment for student table");
--3、更改SerDe属性
ALTER TABLE table_name SET SERDE serde_class_name [WITH SERDEPROPERTIES (property_name = property_value, ... )];
ALTER TABLE table_name [PARTITION partition_spec] SET SERDEPROPERTIES serde_properties;
ALTER TABLE table_name SET SERDEPROPERTIES ('field.delim' = ',');
--移除SerDe属性
ALTER TABLE table_name [PARTITION partition_spec] UNSET SERDEPROPERTIES (property_name, ... );

--4、更改表的文件存储格式 该操作仅更改表元数据。现有数据的任何转换都必须在Hive之外进行。
ALTER TABLE table_name  SET FILEFORMAT file_format;
--5、更改表的存储位置路径
ALTER TABLE table_name SET LOCATION "new location";

--6、更改列名称/类型/位置/注释
CREATE TABLE test_change (a int, b int, c int);
// First change column a's name to a1.
ALTER TABLE test_change CHANGE a a1 INT;
// Next change column a1's name to a2, its data type to string, and put it after column b.
ALTER TABLE test_change CHANGE a1 a2 STRING AFTER b;
// The new table's structure is:  b int, a2 string, c int.
// Then change column c's name to c1, and put it as the first column.
ALTER TABLE test_change CHANGE c c1 INT FIRST;
// The new table's structure is:  c1 int, b int, a2 string.
// Add a comment to column a1
ALTER TABLE test_change CHANGE a1 a1 INT COMMENT 'this is column a1';

--7、添加/替换列
--使用ADD COLUMNS，您可以将新列添加到现有列的末尾但在分区列之前。
--REPLACE COLUMNS 将删除所有现有列，并添加新的列集。
ALTER TABLE table_name ADD|REPLACE COLUMNS (col_name data_type,...);
```

Partition分区 DDL操作

> 比较重要的是==增加分区==、==删除分区==操作

```sql
--1、增加分区
--step1: 创建表 手动加载分区数据
drop table if exists t_user_province;
create table t_user_province (
    num int,
    name string,
    sex string,
    age int,
    dept string) partitioned by (province string);

load data local inpath '/root/hivedata/students.txt' into table t_user_province partition(province ="SH");


--step2:手动创建分区的文件夹 且手动上传文件到分区中 绕开了hive操作  发现hive无法识别新分区
hadoop fs -mkdir /user/hive/warehouse/itheima.db/t_user_province/province=XM
hadoop fs -put students.txt /user/hive/warehouse/itheima.db/t_user_province/province=XM


--step3：修改hive的分区，添加一个分区元数据
ALTER TABLE t_user_province ADD PARTITION (province='XM') location
    '/user/hive/warehouse/itheima.db/t_user_province/province=XM';


----此外还支持一次添加多个分区
ALTER TABLE table_name ADD PARTITION (dt='2008-08-08', country='us') location '/path/to/us/part080808'
    PARTITION (dt='2008-08-09', country='us') location '/path/to/us/part080809';


--2、重命名分区
ALTER TABLE t_user_province PARTITION (province ="SH") RENAME TO PARTITION (province ="Shanghai");

--3、删除分区
ALTER TABLE table_name DROP [IF EXISTS] PARTITION (dt='2008-08-08', country='us');
ALTER TABLE table_name DROP [IF EXISTS] PARTITION (dt='2008-08-08', country='us') PURGE; --直接删除数据 不进垃圾桶 有点像skipTrash

--4、修复分区
MSCK [REPAIR] TABLE table_name [ADD/DROP/SYNC PARTITIONS];
--详细使用见课件资料

--5、修改分区
--更改分区文件存储格式
ALTER TABLE table_name PARTITION (dt='2008-08-09') SET FILEFORMAT file_format;
--更改分区位置
ALTER TABLE table_name PARTITION (dt='2008-08-09') SET LOCATION "new location";
```

#### 4.7.5.1.  show语法

> show databases    数据库
>
> show tables         表
>
> show partitions   表的所有分区  注意必须是分区表才可以执行该语法
>
> ==desc formatted table_name;  查看表的元数据信息==
>
> show create table table_name;  获取表的DDL建表语句
>
> show functions;   函数方法

```sql
--1、显示所有数据库 SCHEMAS和DATABASES的用法 功能一样
show databases;
show schemas;

--2、显示当前数据库所有表/视图/物化视图/分区/索引
show tables;
SHOW TABLES [IN database_name]; --指定某个数据库

--3、显示当前数据库下所有视图
--视图相当于没有数据临时表  虚拟表
Show Views;
SHOW VIEWS 'test_*'; -- show all views that start with "test_"
SHOW VIEWS FROM test1; -- show views from database test1
SHOW VIEWS [IN/FROM database_name];

--4、显示当前数据库下所有物化视图
SHOW MATERIALIZED VIEWS [IN/FROM database_name];

--5、显示表分区信息，分区按字母顺序列出，不是分区表执行该语句会报错
show partitions table_name;
show partitions itheima.student_partition;

--6、显示表/分区的扩展信息
SHOW TABLE EXTENDED [IN|FROM database_name] LIKE table_name;
show table extended like student;
describe formatted itheima.student;

--7、显示表的属性信息
SHOW TBLPROPERTIES table_name;
show tblproperties student;

--8、显示表、视图的创建语句
SHOW CREATE TABLE ([db_name.]table_name|view_name);
show create table student;

--9、显示表中的所有列，包括分区列。
SHOW COLUMNS (FROM|IN) table_name [(FROM|IN) db_name];
show columns  in student;

--10、显示当前支持的所有自定义和内置的函数
show functions;

--11、Describe desc
--查看表信息
desc extended table_name;
--查看表信息（格式化美观）
desc formatted table_name;
--查看数据库相关信息
describe database database_name;
```

### 4.7.6. DML语法

#### insert插入数据

**==insert+select==**

> ==在hive中，insert主要是结合 select 查询语句使用，将查询结果插入到表中==。

保证后面select**查询语句返回的结果字段个数、类型、顺序和待插入表一致**；

如果不一致，Hive会尝试帮你转换，但是不保证成功；

insert+select也是在数仓中ETL数据常见的操作。

```sql
--step1:创建一张源表student
drop table if exists student;
create table student(num int,name string,sex string,age int,dept string)
row format delimited
fields terminated by ',';
--加载数据
load data local inpath '/root/hivedata/students.txt' into table student;

select * from student;

--step2：创建一张目标表  只有两个字段
create table student_from_insert(sno int,sname string);
--使用insert+select插入数据到新表中
insert into table student_from_insert
select num,name from student;

select *
from student_from_insert;
```



Multi Inserts ==多重插入==

- 功能：==**一次扫描，多次插入**==

- 例子

  ```sql
  create table source_table (id int, name string) row format delimited fields terminated by ',';
  
  create table test_insert1 (id int) row format delimited fields terminated by ',';
  create table test_insert2 (name string) row format delimited fields terminated by ',';
  
  
  --普通插入：
  insert into table test_insert1 select id from source_table;
  insert into table test_insert2 select name from source_table;
  
  --在上述需求实现中 从同一张表扫描了2次 分别插入不同的目标表中 性能低下。
  
  --多重插入：
  from source_table                     
  insert overwrite table test_insert1 
  select id
  insert overwrite table test_insert2
  select name;
  --只需要扫描一次表  分别把不同字段插入到不同的表中即可 减少扫描次数 提高效率
  ```



Dynamic partition inserts ==动态分区插入==

- 何谓动态分区，静态分区

  ```sql
  针对的是分区表。
  --问题：分区表中分区字段值是如何确定的？
  
  1、如果是在加载数据的时候人手动写死指定的  叫做静态分区 
  load data local inpath '/root/hivedata/usa_dezhou.txt'  into table t_user_double_p partition(guojia="meiguo",sheng="dezhou");
  
  2、如果是通过insert+select 动态确定分区值的，叫做动态分区
  insert table partition (分区字段) +select 
  ```

- 例子

  ```sql
  --1、首先设置动态分区模式为非严格模式 默认已经开启了动态分区功能
  set hive.exec.dynamic.partition = true;
  set hive.exec.dynamic.partition.mode = nonstrict;
  
  --2、当前库下已有一张表student
  select * from student;
  
  --3、创建分区表 以sdept作为分区字段
  create table student_partition(Sno int,Sname string,Sex string,Sage int) partitioned by(Sdept string);
  
  --4、执行动态分区插入操作
  insert into table student_partition partition(Sdept)
  select num,name,sex,age,dept from student;
  --其中，num,name,sex,age作为表的字段内容插入表中
  --dept作为分区字段值
  
  select *
  from student_partition;
  
  show partitions student_partition;
  ```

#### insert导出数据

功能：把select查询的结果导出成为一个文件。

注意：**==导出操作是一个overwrite操作==**，可能会让你凉凉。慎重！！！！

语法

```sql
--当前库下已有一张表student
select * from student_hdfs;

--1、导出查询结果到HDFS指定目录下
insert overwrite directory '/tmp/hive_export/e1' select num,name,age from student_hdfs limit 2;   --默认导出数据字段之间的分隔符是\001

--2、导出时指定分隔符和文件存储格式
insert overwrite directory '/tmp/hive_export/e2' row format delimited fields terminated by ','
stored as orc
select num,name,age from student_hdfs limit 2;

--3、导出数据到本地文件系统指定目录下
insert overwrite local directory '/root/hive_export/e1' select num,name,age from student_hdfs limit 2;
```

### 4.7.7. Hive SQL：DQL

select语法树

```sql
SELECT [ALL | DISTINCT] select_expr, select_expr, ...
FROM table_reference
JOIN table_other ON expr
[WHERE where_condition]
[GROUP BY col_list [HAVING condition]]
[CLUSTER BY col_list
| [DISTRIBUTE BY col_list] [SORT BY| ORDER BY col_list]
]
[LIMIT number]
```

#### CLUSTER BY 分桶查询

语法

```sql
select * from student;  --普桶查询
select * from student cluster by num; --分桶查询 根据学生编号进行分桶查询

--Q:分为几个部分？ 分的规则是什么？
分为几个部分取决于reducetask个数
分的规则和分桶表的规则一样 hashfunc(字段)  %  reducetask个数
```

reducetask个数是如何确定的？ reducetask个数就决定了最终数据分为几桶。

```sql
--如果用户没有设置,不指定reduce task个数。则hive根据表输入数据量自己评估
--日志显示：Number of reduce tasks not specified. Estimated from input data size: 1
select * from student cluster by num;

--手动设置reduce task个数
--日志显示：Number of reduce tasks not specified. Defaulting to jobconf value of: 2
set mapreduce.job.reduces =2;
select * from student cluster by num;
----分桶查询的结果真的根据reduce tasks个数分为了两个部分，并且每个部分中还根据了字段进行了排序。

--总结：cluster by xx  分且排序的功能
	  分为几个部分 取决于reducetask个数
	  排序只能是正序 用户无法改变
	   
--需求：把student表数据根据num分为两个部分，每个部分中根据年龄age倒序排序。	
set mapreduce.job.reduces =2;
select  * from student cluster by num order by age desc;
select  * from student cluster by num sort by age desc;
--FAILED: SemanticException 1:50 Cannot have both CLUSTER BY and SORT BY clauses

```

==DISTRIBUTE BY+SORT BY==

功能：相当于把cluster by的功能一分为二。

- distribute by只负责分;
- sort by只负责分之后的每个部分排序。
- 并且分和排序的字段可以不一样。

```sql
--当后面分和排序的字段是同一个字段 加起来就相等于cluster by
CLUSTER BY(分且排序) = DISTRIBUTE BY（分）+SORT BY（排序） 

--下面两个功能一样的
select  * from student cluster by num;
select  * from student distribute by num sort by num;

--最终实现
select  * from student distribute by num sort by age desc;
```

ORDER BY

```sql
--首先我们设置一下reducetask个数，随便设置
--根据之前的探讨，貌似用户设置几个，结果就是几个，但是实际情况如何呢？
set mapreduce.job.reduces =2;
select  * from student order by age desc;

--执行中日志显示
Number of reduce tasks determined at compile time: 1 --不是设置了为2吗 

--原因：order by是全局排序。全局排序意味着数据只能输出在一个文件中。因此也只能有一个reducetask.
--在order by出现的情况下，不管用户设置几个reducetask,在编译执行期间都会变为一个，满足全局。
```

order by 和sort by

- order by负责==全局排序==  意味着整个mr作业只有一个reducetask 不管用户设置几个 编译期间hive都会把它设置为1。
- sort by负责分完之后 局部排序。

#### union联合查询

union联合查询

> UNION用于将来自==多个SELECT语句的结果合并为一个结果集==。

```sql
--语法规则
select_statement UNION [ DISTINCT|ALL ] select_statement UNION [ALL | DISTINCT] select_statement ...;

--使用DISTINCT关键字与使用UNION默认值效果一样，都会删除重复行。
select num,name from student_local
UNION
select num,name from student_hdfs;
--和上面一样
select num,name from student_local
UNION DISTINCT
select num,name from student_hdfs;

--使用ALL关键字会保留重复行。
select num,name from student_local
UNION ALL
select num,name from student_hdfs limit 2;

--如果要将ORDER BY，SORT BY，CLUSTER BY，DISTRIBUTE BY或LIMIT应用于单个SELECT
--请将子句放在括住SELECT的括号内
SELECT num,name FROM (select num,name from student_local LIMIT 2)  subq1
UNION
SELECT num,name FROM (select num,name from student_hdfs LIMIT 3) subq2;

--如果要将ORDER BY，SORT BY，CLUSTER BY，DISTRIBUTE BY或LIMIT子句应用于整个UNION结果
--请将ORDER BY，SORT BY，CLUSTER BY，DISTRIBUTE BY或LIMIT放在最后一个之后。
select num,name from student_local
UNION
select num,name from student_hdfs
order by num desc;
```

#### CTE表达式（with）

> 通用表表达式（CTE）是一个临时结果集，该结果集是从==WITH子句中指定的简单查询==
> ==派生而来的==，该查询紧接在SELECT或INSERT关键字之前。
>
> 通俗解释：sql开始前定义一个SQL片断，该SQL片断可以被后续整个SQL语句所用到，并且可以多次使用。

```sql
--select语句中的CTE
with q1 as (select num,name,age from student where num = 95002)
select *
from q1;

-- from风格
with q1 as (select num,name,age from student where num = 95002)
from q1
select *;

-- chaining CTEs 链式
with q1 as ( select * from student where num = 95002),
     q2 as ( select num,name,age from q1)
select * from (select num from q2) a;

-- union
with q1 as (select * from student where num = 95002),
     q2 as (select * from student where num = 95004)
select * from q1 union all select * from q2;

-- ctas  
-- creat table as select 创建一张表来自于后面的查询语句  表的字段个数 名字 顺序和数据行数都取决于查询
-- create table t_ctas as select num,name from student limit 2;

create table s2 as
with q1 as ( select * from student where num = 95002)
select * from q1;

-- view
create view v1 as
with q1 as ( select * from student where num = 95002)
select * from q1;

select * from v1;
```

#### Hive join方法

语法树

```sql
join_table:
    table_reference [INNER] JOIN table_factor [join_condition]
  | table_reference {LEFT|RIGHT|FULL} [OUTER] JOIN table_reference join_condition
  | table_reference LEFT SEMI JOIN table_reference join_condition
  | table_reference CROSS JOIN table_reference [join_condition] (as of Hive 0.10)
 
join_condition:
    ON expression
```

具体6种join方式，重点掌握  ==inner 和left join==。

```sql
--Join语法练习 建表
drop table if exists employee_address;
drop table if exists employee_connection;
drop table if exists employee;

--table1: 员工表
CREATE TABLE employee(
   id int,
   name string,
   deg string,
   salary int,
   dept string
 ) row format delimited
fields terminated by ',';

--table2:员工家庭住址信息表
CREATE TABLE employee_address (
    id int,
    hno string,
    street string,
    city string
) row format delimited
fields terminated by ',';

--table3:员工联系方式信息表
CREATE TABLE employee_connection (
    id int,
    phno string,
    email string
) row format delimited
fields terminated by ',';

--加载数据到表中
load data local inpath '/root/hivedata/employee.txt' into table employee;
load data local inpath '/root/hivedata/employee_address.txt' into table employee_address;
load data local inpath '/root/hivedata/employee_connection.txt' into table employee_connection;

select * from employee;
+--------------+----------------+---------------+------------------+----------------+
| employee.id  | employee.name  | employee.deg  | employee.salary  | employee.dept  |
+--------------+----------------+---------------+------------------+----------------+
| 1201         | gopal          | manager       | 50000            | TP             |
| 1202         | manisha        | cto           | 50000            | TP             |
| 1203         | khalil         | dev           | 30000            | AC             |
| 1204         | prasanth       | dev           | 30000            | AC             |
| 1206         | kranthi        | admin         | 20000            | TP             |
| 1201         | gopal          | manager       | 50000            | TP             |
| 1202         | manisha        | cto           | 50000            | TP             |
| 1203         | khalil         | dev           | 30000            | AC             |
| 1204         | prasanth       | dev           | 30000            | AC             |
| 1206         | kranthi        | admin         | 20000            | TP             |
+--------------+----------------+---------------+------------------+----------------+

select * from employee_address;


select * from employee_connection;

```



```sql
--1、内连接  inner join == join
  返回左右两边同时满足条件的数据
  
select e.*,e_a.*
from employee e inner join employee_address e_a
on e.id =e_a.id;

--等价于 inner join
select e.*,e_a.*
from employee e join employee_address e_a
on e.id =e_a.id;

--等价于 隐式连接表示法
select e.*,e_a.*
from employee e , employee_address e_a
where e.id =e_a.id;

  
--2、左连接  left join  ==  left OUTER join
  左表为准，左表全部显示，右表与之关联 满足条件的返回，不满足条件显示null
  
select e.*,e_conn.*
from employee e left join employee_connection e_conn
on e.id =e_conn.id;

--等价于 left outer join 左外连接
select e.id,e.*,e_conn.*
from employee e left outer join  employee_connection e_conn
on e.id =e_conn.id;  
  
--3、右连接  right join  ==  right OUTER join 右外连接
  右表为准，右表全部显示，左表与之关联 满足条件的返回，不满足条件显示null
 
select e.id,e.*,e_conn.*
from employee e right join employee_connection e_conn
on e.id =e_conn.id;

--等价于 right outer join
select e.id,e.*,e_conn.*
from employee e right outer join employee_connection e_conn
on e.id =e_conn.id;

--4、外连接 全外连接 full join == full outer join
FULL OUTER JOIN 关键字只要左表（table1）和右表（table2）其中一个表中存在匹配，则返回行.
FULL OUTER JOIN 关键字结合了 LEFT JOIN 和 RIGHT JOIN 的结果。

select e.*,e_a.*
from employee e full outer join employee_address e_a
on e.id =e_a.id;
--等价于
select e.*,e_a.*
from employee e full join employee_address e_a
on e.id =e_a.id;

--5、左半连接 left semi join

select *
from employee e left semi join employee_address e_addr
on e.id =e_addr.id;

--相当于 inner join,但是只返回左表全部数据， 只不过效率高一些
select e.*
from employee e inner join employee_address e_addr
on e.id =e_addr.id;

--6、交叉连接cross join
将会返回被连接的两个表的笛卡尔积，返回结果的行数等于两个表行数的乘积。对于大表来说，cross join慎用。
在SQL标准中定义的cross join就是无条件的inner join。返回两个表的笛卡尔积,无需指
定关联键。
在HiveSQL语法中，cross join 后面可以跟where子句进行过滤，或者on条件过滤。
```

**Join语法注意事项**

允许使用复杂的联接表达式；

同一查询中可以连接2个以上的表；

如果每个表在联接子句中使用相同的列，则Hive将多个表上的联接转换为单个MR作业

join时的最后一个表会通过reducer流式传输，并在其中缓冲之前的其他表，因此，将大表放置在最后有助于减少reducer阶段缓存数据所需要的内存

在join的时候，可以通过语法STREAMTABLE提示指定要流式传输的表。如果省略STREAMTABLE提示，则Hive将流式传输最右边的表。

### 4.7.8. Hive 客户端与参数

#### 第一代客户端功能

> ==批处理==：一次连接，一次交互， 执行结束断开连接
> ==交互式处理==：保持持续连接， 一直交互
>
> 注意：如果说hive的shell客户端 指的是第一代客户端bin/hive
>
> 而第二代客户端bin/beeline属于JDBC客户端 不是shell。



==**bin/hive**==

功能1：作为==第一代客户端== 连接访问==metastore服务==，使用Hive。交互式方式

功能2：启动hive服务

```shell
/export/server/apache-hive-3.1.2-bin/bin/hive --service metastore 
/export/server/apache-hive-3.1.2-bin/bin/hive --service hiveserver2 
```

功能3：批处理执行Hive SQL

```shell
#-e 执行后面的sql语句
/export/server/apache-hive-3.1.2-bin/bin/hive  -e 'select * from itheima.student'

#-f 执行后面的sql文件
vim hive.sql
select * from itheima.student limit 2

/export/server/apache-hive-3.1.2-bin/bin/hive  -f hive.sql

#sql文件不一定是.sql 要保证文件中是正确的HQL语法。

#-f调用sql文件执行的方式 是企业中hive生产环境主流的调用方式。
```

#### 参数配置方式与优先级

有哪些参数可以配置？

```
https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties
```

配置方式有哪些？  注意配置方式影响范围影响时间是怎样？

方式1：配置文件  con/==hive-site.xml==

```
影响的是基于这个安装包的任何使用方式。
```

方式2：配置参数 ==--hiveconf==

```shell
/export/server/apache-hive-3.1.2-bin/bin/hive --service metastore  

/export/server/apache-hive-3.1.2-bin/bin/hive --service hiveserver2  --hiveconf hive.root.logger=DEBUG,console

#影响的是session会话级别的
```

方式3：==set命令==

==session会话级别的==，设置完之后将会对后面的sql执行生效。session结束 set设置的参数将失效。

也是推荐搭建使用的设置参数方式。谁需要、谁设置、谁生效

总结：

- 从方式1到方式3  ==影响的范围是越来越小的==。
- 从方式1到方式3  优先级越来越高。set命令设置的会覆盖其他的。
- Hive作为的基于Hadoop的数仓，也会==把Hadoop 的相关配置 解析加载==进来。

### 4.7.9. 函数与分类标准

内置的函数（==build in func==）

> 所谓的内置指的是hive开发好，可以直接上手使用的；

- 内置函数往往根据函数的应用功能类型来分类
- 日期函数、数字函数、字符串函数、集合函数、条件函数....



用户定义函数（==user-defined function==）

> 用户编程实现函数的逻辑在hive中使用。

- UDF根据函数==输入行数和输出行数==进行分类

- UDF 、UDAF、UDTF

  ```shell
  #1、UDF（User-Defined-Function）普通函数 一进一出  输入一行数据输出一行数据
  
  0: jdbc:hive2://node1:10000> select split("allen woon hadoop"," ");
  +----------------------------+--+
  |            _c0             |
  +----------------------------+--+
  | ["allen","woon","hadoop"]  |
  +----------------------------+--+
  
  #2、UDAF（User-Defined Aggregation Function）聚合函数，多进一出 输入多行输出一行
  
  count sum max  min  avg
  
  #3、UDTF（User-Defined Table-Generating Functions）表生成函数 一进多出 输入一行输出多行
  
  explode 、parse_url_tuple
  ```



==**UDF分类标准的扩大化**==

- 本来，udf/udtf/udaf3个标准是针对用户自定义函数分类的；
- 但是，现在可以将这个分类标准扩大到==hive中所有的函数，包括内置函数和自定义函数==；
- 不要被UD这两个字母所影响。  Built-in Aggregate Functions (UDAF).



函数相关的常用帮助命令

```sql
--显示所有的函数和运算符
show functions;
--查看运算符或者函数的使用说明
describe function +;
desc function 
--使用extended 可以查看更加详细的使用说明
describe function extended count;
```

#### 字符串函数

```hive
--字符串截取函数：substr(str, pos[, len]) 或者  substring(str, pos[, len])
select substr("angelababy",-2); --pos是从1开始的索引，如果为负数则倒着数
select substr("angelababy",2,2);

--正则表达式替换函数：regexp_replace(str, regexp, rep)
select regexp_replace('100-200', '(\\d+)', 'num'); --正则分组

--正则表达式解析函数：regexp_extract(str, regexp[, idx]) 提取正则匹配到的指定组内容
select regexp_extract('100-200', '(\\d+)-(\\d+)', 2);

--URL解析函数：parse_url 注意要想一次解析出多个 可以使用parse_url_tuple这个UDTF函数
select parse_url('http://www.itcast.cn/path/p1.php?query=1', 'HOST');

--分割字符串函数: split(str, regex)
select split('apache hive', '\\s+');--匹配一个或者多个空白符

--json解析函数：get_json_object(json_txt, path)
--$表示json对象
select get_json_object('[{"website":"www.itcast.cn","name":"allenwoon"}, {"website":"cloud.itcast.com","name":"carbondata 中文文档"}]', '$.[1].website');

```

#### 时间日期、数值

Date Functions 日期函数

> 日期和时间戳数字之间的转换 
>
> ==unix_timestamp==  日期转unix时间戳
>
> ==from_unixtime==  unix时间戳转日期
>
> ==date_add== 
>
> ==date_sub==  
>
> ==datediff==

```sql
--获取当前日期: current_date
select current_date();
--获取当前时间戳: current_timestamp
--同一查询中对current_timestamp的所有调用均返回相同的值。
select current_timestamp();
--获取当前UNIX时间戳函数: unix_timestamp
select unix_timestamp();
--日期转UNIX时间戳函数: unix_timestamp
select unix_timestamp("2011-12-07 13:01:03");
--指定格式日期转UNIX时间戳函数: unix_timestamp
select unix_timestamp('20111207 13:01:03','yyyyMMdd HH:mm:ss');
--UNIX时间戳转日期函数: from_unixtime
select from_unixtime(1620723323);
select from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
--日期比较函数: datediff  日期格式要求'yyyy-MM-dd HH:mm:ss' or 'yyyy-MM-dd'
select datediff('2012-12-08','2012-05-09');
--日期增加函数: date_add
select date_add('2012-02-28',10);
--日期减少函数: date_sub
select date_sub('2012-01-1',10);
```

---

Mathematical Functions 数学函数

> ==round== 取整
>
> ==rand== 取随机值

```sql
--取整函数: round  返回double类型的整数值部分 （遵循四舍五入）
select round(3.1415926);
--指定精度取整函数: round(double a, int d) 返回指定精度d的double类型
select round(3.1415926,4);
--向下取整函数: floor
select floor(3.1415926);
select floor(-3.1415926);
--向上取整函数: ceil
select ceil(3.1415926);
select ceil(-3.1415926);
--取随机数函数: rand 每次执行都不一样 返回一个0到1范围内的随机数
select rand();
--指定种子取随机数函数: rand(int seed) 得到一个稳定的随机数序列
select rand(5);
```

#### 条件转换、集合、加密

Conditional Functions 条件函数

> ==都重要==。尤其是case when

```sql
--if条件判断: if(boolean testCondition, T valueTrue, T valueFalseOrNull)
select if(1=2,100,200);
select if(sex ='男','M','W') from student limit 3;

--空判断函数: isnull( a )
select isnull("allen");
select isnull(null);

--非空判断函数: isnotnull ( a )
select isnotnull("allen");
select isnotnull(null);

--空值转换函数: nvl(T value, T default_value)
select nvl("allen","itcast");
select nvl(null,"itcast");

--非空查找函数: COALESCE(T v1, T v2, ...)
--返回参数中的第一个非空值；如果所有值都为NULL，那么返回NULL
select COALESCE(null,11,22,33);
select COALESCE(null,null,null,33);
select COALESCE(null,null,null);

--条件转换函数: CASE a WHEN b THEN c [WHEN d THEN e]* [ELSE f] END
select case 100 when 50 then 'tom' when 100 then 'mary' else 'tim' end;
select case sex when '男' then 'male' else 'female' end from student limit 3;
```

-----

Type Conversion Functions 类型转换函数

- 前置知识：Hive中支持类型的隐式转换  有限制  自动转换  不保证成功  就显示null

- ==cast显示类型转换函数==

  ```sql
  --任意数据类型之间转换:cast
  select cast(12.14 as bigint);
  select cast(12.14 as string);
  select cast("hello" as int);
  +-------+
  |  _c0  |
  +-------+
  | NULL  |
  +-------+
  ```

----

Data Masking Functions 数据脱敏函数  

> mask脱敏 掩码处理
>
> 数据脱敏：==让敏感数据不敏感==   13455667788 --->134****7788

```sql
--mask
--将查询回的数据，大写字母转换为X，小写字母转换为x，数字转换为n。
select mask("abc123DEF");
select mask("abc123DEF",'-','.','^'); --自定义替换的字母

--mask_first_n(string str[, int n]
--对前n个进行脱敏替换
select mask_first_n("abc123DEF",4);

--mask_last_n(string str[, int n])
select mask_last_n("abc123DEF",4);

--mask_show_first_n(string str[, int n])
--除了前n个字符，其余进行掩码处理
select mask_show_first_n("abc123DEF",4);

--mask_show_last_n(string str[, int n])
select mask_show_last_n("abc123DEF",4);

--mask_hash(string|char|varchar str)
--返回字符串的hash编码。
select mask_hash("abc123DEF");

```

-----

Misc. Functions 其他杂项函数、加密函数

```sql
--如果你要调用的java方法所在的jar包不是hive自带的 可以使用add jar添加进来
--hive调用java方法: java_method(class, method[, arg1[, arg2..]])
select java_method("java.lang.Math","max",11,22);

--反射函数: reflect(class, method[, arg1[, arg2..]])
select reflect("java.lang.Math","max",11,22);

--取哈希值函数:hash
select hash("allen");

--current_user()、logged_in_user()、current_database()、version()

--SHA-1加密: sha1(string/binary)
select sha1("allen");

--SHA-2家族算法加密：sha2(string/binary, int)  (SHA-224, SHA-256, SHA-384, SHA-512)
select sha2("allen",224);
select sha2("allen",512);

--crc32加密:
select crc32("allen");

--MD5加密: md5(string/binary)
select md5("allen");
```

### 4.7.10. UDTF表生成函数

#### explode函数

功能：

```sql
explode() takes in an array (or a map) as an input and outputs the elements of the array (map) as separate rows.

--explode接收map array类型的参数 把map或者array的元素输出，一行一个元素。

explode(array(11,22,33))         11
	                             22
	                             33
	                             
	                             
select explode(`array`(11,22,33,44,55));
select explode(`map`("id",10086,"name","allen","age",18));	                             
```

栗子

> 将NBA总冠军球队数据使用explode进行拆分，并且根据夺冠年份进行倒序排序。

```sql
--step1:建表
create table the_nba_championship(
           team_name string,
           champion_year array<string>
) row format delimited
fields terminated by ','
collection items terminated by '|';

--step2:加载数据文件到表中
load data local inpath '/root/hivedata/The_NBA_Championship.txt' into table the_nba_championship;

--step3:验证
select * from the_nba_championship;

--step4:使用explode函数对champion_year进行拆分 俗称炸开
select explode(champion_year) from the_nba_championship;

--想法是正确的 sql执行确实错误的
select team_name,explode(champion_year) from the_nba_championship;
--错误信息
UDTF's are not supported outside the SELECT clause, nor nested in expressions
UDTF 在 SELECT 子句之外不受支持，也不在表达式中嵌套？？？
```

如果数据不是map或者array 如何使用explode函数呢？

> 想法设法使用split subsrt regex_replace等函数组合使用 把数据变成array或者map.

```sql
create table the_nba_championship_str(
           team_name string,
           champion_year string
) row format delimited
fields terminated by ',';

load data local inpath '/root/hivedata/The_NBA_Championship.txt' into table the_nba_championship_str;

select team_name,explode(split(champion_year, "|")) from the_nba_championship;
```

#### lateral view侧视图

> 侧视图的原理是==将UDTF的结果构建成一个类似于视图的表，然后将原表中的每一行和UDTF函数输出的每一行进行连接，生成一张新的虚拟表==

背景

UDTF函数生成的结果可以当成一张虚拟的表，但是无法和原始表进行组合查询

```sql
select name,explode(location) from test_message;
--这个sql就是错误的  相当于执行组合查询 
```

从理论层面推导，对两份数据进行join就可以了

但是，hive专门推出了lateral view侧视图的语，满足上述需要。

功能：==把UDTF函数生成的结果和原始表进行关联，便于用户在select时间组合查询==、  lateral view是UDTf的好基友好搭档，实际中经常配合使用。

语法：

```sql
--lateral view侧视图基本语法如下
select …… from tabelA lateral view UDTF(xxx) 别名 as col1,col2,col3……;

--针对上述NBA冠军球队年份排名案例，使用explode函数+lateral view侧视图，可以完美解决
select a.team_name ,b.year
from the_nba_championship a lateral view explode(champion_year) b as year;

--根据年份倒序排序
select a.team_name ,b.year
from the_nba_championship a lateral view explode(champion_year) b as year
order by b.year desc;

--统计每个球队获取总冠军的次数 并且根据倒序排序
select a.team_name ,count(*) as nums
from the_nba_championship a lateral view explode(champion_year) b as year
group by a.team_name
order by nums desc;
```

### 4.7.11. 行列转换

#### collect多行转单列

==**数据收集函数**==

```sql
collect_set --把多行数据收集为一行  返回set集合  去重无序
collect_list --把多行数据收集为一行  返回list集合  不去重有序
```

字符串拼接函数

```sql
concat  --直接拼接字符串
concat_ws --指定分隔符拼接

select concat("it","cast","And","heima");
select concat("it","cast","And",null);

select concat_ws("-","itcast","And","heima");
select concat_ws("-","itcast","And",null);
```

栗子

```sql
--原表
+----------------+----------------+----------------+--+
| row2col2.col1  | row2col2.col2  | row2col2.col3  |
+----------------+----------------+----------------+--+
| a              | b              | 1              |
| a              | b              | 2              |
| a              | b              | 3              |
| c              | d              | 4              |
| c              | d              | 5              |
| c              | d              | 6              |
+----------------+----------------+----------------+--+

--目标表
+-------+-------+--------+--+
| col1  | col2  |  col3  |
+-------+-------+--------+--+
| a     | b     | 1-2-3  |
| c     | d     | 4-5-6  |
+-------+-------+--------+--+

--建表
create table row2col2(
                         col1 string,
                         col2 string,
                         col3 int
)row format delimited fields terminated by '\t';

--加载数据到表中
load data local inpath '/root/hivedata/r2c2.txt' into table row2col2;
select * from row2col2;

--最终SQL实现
select
    col1,
    col2,
    concat_ws(',', collect_list(cast(col3 as string))) as col3
from
    row2col2
group by
    col1, col2;
```

#### 单列转多行（explode、lateral view）

技术原理： explode+lateral view

例子

```sql
--原表
+-------+-------+--------+--+
| col1  | col2  |  col3  |
+-------+-------+--------+--+
| a     | b     | 1,2,3  |
| c     | d     | 4,5,6  |
+-------+-------+--------+--+

--目标表
+----------------+----------------+----------------+--+
| row2col2.col1  | row2col2.col2  | row2col2.col3  |
+----------------+----------------+----------------+--+
| a              | b              | 1              |
| a              | b              | 2              |
| a              | b              | 3              |
| c              | d              | 4              |
| c              | d              | 5              |
| c              | d              | 6              |
+----------------+----------------+----------------+--+

--创建表
create table col2row2(
                         col1 string,
                         col2 string,
                         col3 string
)row format delimited fields terminated by '\t';

--加载数据
load data local inpath '/root/hivedata/c2r2.txt' into table col2row2;

select * from col2row2;

select explode(split(col3,',')) from col2row2;

--SQL最终实现
select
    col1,
    col2,
    lv.col3 as col3
from
    col2row2
        lateral view
            explode(split(col3, ',')) lv as col3;
```

#### json格式数据处理

在hive中，没有json类的存在，一般使==用string类型来修饰==，叫做json字符串，简称==json串==。

在hive中，处理json数据的两种方式

hive内置了两个用于==解析json的函数==

```sql
json_tuple
--是UDTF 表生成函数  输入一行，输出多行  一次提取读个值  可以单独使用 也可以配合lateral view侧视图使用

get_json_object
--是UDF普通函数，输入一行 输出一行 一次只能提取一个值 多次提取多次使用
```

使用==[JsonSerDe](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-JSON) 类解析==，在加载json数据到表中的时候完成解析动作

```sql
--创建表
create table tb_json_test1 (
    json string
);

--加载数据
load data local inpath '/root/hivedata/device.json' into table tb_json_test1;

select * from tb_json_test1;

-- get_json_object UDF函数 最大弊端是一次只能解析提取一个字段
select
    --获取设备名称
    get_json_object(json,"$.device") as device,
    --获取设备类型
    get_json_object(json,"$.deviceType") as deviceType,
    --获取设备信号强度
    get_json_object(json,"$.signal") as signal,
    --获取时间
    get_json_object(json,"$.time") as stime
from tb_json_test1;

--json_tuple 这是一个UDTF函数 可以一次解析提取多个字段
--单独使用 解析所有字段
select
    json_tuple(json,"device","deviceType","signal","time") as (device,deviceType,signal,stime)
from tb_json_test1;

--搭配侧视图使用
select
    json,device,deviceType,signal,stime
from tb_json_test1
         lateral view json_tuple(json,"device","deviceType","signal","time") b
         as device,deviceType,signal,stime;


--方式2： 使用JsonSerDe类在建表的时候解析数据
--建表的时候直接使用JsonSerDe解析
create table tb_json_test2 (
                               device string,
                               deviceType string,
                               signal double,
                               `time` string
)
    ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe'
    STORED AS TEXTFILE;

load data local inpath '/root/hivedata/device.json' into table tb_json_test2;

select * from tb_json_test2;
```

### 4.7.12. 窗口函数

window function 窗口函数、开窗函数、olap分析函数。

窗口：可以理解为操作数据的范围，窗口有大有小，本窗口中操作的数据有多有少。

可以简单地解释为类似于聚合函数的计算函数，但是通过GROUP BY子句组合的常规聚合会隐藏正在聚合的各个行，最终输出一行；而==窗口函数聚合后还可以访问当中====的各个行，并且可以将这些行中的某些属性添加到结果集中==。

```sql
--建表加载数据
CREATE TABLE employee(
       id int,
       name string,
       deg string,
       salary int,
       dept string
) row format delimited
    fields terminated by ',';

load data local inpath '/root/hivedata/employee.txt' into table employee;

select * from employee;

----sum+group by普通常规聚合操作------------
select dept,sum(salary) as total from employee group by dept;

select id,dept,sum(salary) as total from employee group by dept; --添加id至结果，错误sql

+-------+---------+
| dept  |  total  |
+-------+---------+
| AC    | 60000   |
| TP    | 120000  |
+-------+---------+

----sum+窗口函数聚合操作------------
select id,name,deg,salary,dept,sum(salary) over(partition by dept) as total from employee;

+-------+-----------+----------+---------+-------+---------+
|  id   |   name    |   deg    | salary  | dept  |  total  |
+-------+-----------+----------+---------+-------+---------+
| 1204  | prasanth  | dev      | 30000   | AC    | 60000   |
| 1203  | khalil    | dev      | 30000   | AC    | 60000   |
| 1206  | kranthi   | admin    | 20000   | TP    | 120000  |
| 1202  | manisha   | cto      | 50000   | TP    | 120000  |
| 1201  | gopal     | manager  | 50000   | TP    | 120000  |
+-------+-----------+----------+---------+-------+---------+
```

---

窗口函数语法规则

> ##### 具有==OVER语句==的函数叫做窗口函数。

```sql
Function OVER ([PARTITION BY <...>] [ORDER BY <....>] [<window_expression>])

--1、Function可以是下面分类中的任意一个
	--聚合函数：比如sum、max、avg、max、min等
    --排序函数：比如rank、row_number等
    --分析函数：比如lead、lag、first_value等

--2、OVER 窗口函数语法关键字与标识

--3、PARTITION BY <...>功能类似于group by，用于指定分组，相同的分为一组。如果没有指定PARTITION BY，那么整张表的所有行就是一组；

--4、ORDER BY <....> 用于指定每个分组内的数据排序规则 ，默认是升序ASC，支持ASC、DESC；

--5、window_expression window表达式，也叫window子句，用于指定每个窗口中操作的数据范围
```

建表加载数据  后续练习使用

```sql
---建表并且加载数据
create table website_pv_info(
   cookieid string,
   createtime string,   --day
   pv int
) row format delimited
fields terminated by ',';

create table website_url_info (
    cookieid string,
    createtime string,  --访问时间
    url string       --访问页面
) row format delimited
fields terminated by ',';


load data local inpath '/root/hivedata/website_pv_info.txt' into table website_pv_info;
load data local inpath '/root/hivedata/website_url_info.txt' into table website_url_info;

select * from website_pv_info;
select * from website_url_info;
```

#### 聚合函数

语法

```sql
sum|max|min|avg  OVER ([PARTITION BY <...>] [ORDER BY <....>] [<window_expression>])
```

重点：==**有PARTITION BY 没有PARTITION BY的区别；有ORDER BY没有ORDER BY的区别**==。

有没有partition by 影响的是全局聚合 还是分组之后 每个组内聚合。

有没有==**order by的区别**==：

- 没有order by，默认是rows between，首行到最后行，这里的"行"是物理上的行；
- 有order by，默认是range between，首行到当前行，这里的"行"是逻辑上的行，由字段的值的区间range来划分范围。

栗子

```sql
--1、求出每个用户总pv数  sum+group by普通常规聚合操作
select cookieid,sum(pv) as total_pv from website_pv_info group by cookieid;
+-----------+-----------+
| cookieid  | total_pv  |
+-----------+-----------+
| cookie1   | 26        |
| cookie2   | 35        |
+-----------+-----------+


--2、sum+窗口函数 
需要注意：这里都没有使用window子句指定范围，那么默认值是rows还是range呢？？？

--当没有order by也没有window子句的时候，默认是rows between,从第一行到最后一行，即分组内的所有行聚合。
--sum(...) over( )
select cookieid,createtime,pv,
       sum(pv) over() as total_pv
from website_pv_info;

--sum(...) over( partition by... )
select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid) as total_pv 
from website_pv_info;


--当有order by但是缺失window子句的时候，默认是range between，为第一行的值到当前行的值构成的区间
--sum(...) over( partition by... order by ... )
select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid order by createtime) as current_total_pv
from website_pv_info;

--上述是根据creattime排序，因此range区间是由createtime的字段值来划分，第一行到当前行。



--下面是根据pv排序，因此range区间是由pv的字段值来划分，第一行到当前行。
--下面两个sql等价
select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid order by pv) as current_total_pv
from website_pv_info; --这属于有order by没有 window子句 默认range

select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid order by pv range between unbounded preceding and current row) as current_total_pv
from website_pv_info;


--这是手动指定根据rows来划分范围
select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid order by pv rows between unbounded preceding and current row ) as current_total_pv
from website_pv_info;
```

#### window子句

> ##### 直译叫做window表达式 ，通俗叫法称之为window子句。

功能：控制窗口操作的范围。

语法

```ini
unbounded 无边界
preceding 往前
following 往后
unbounded preceding 往前所有行，即初始行
n preceding 往前n行
unbounded following 往后所有行，即末尾行
n following 往后n行
current row 当前行
 
语法
(ROWS | RANGE) BETWEEN (UNBOUNDED | [num]) PRECEDING AND ([num] PRECEDING | CURRENT ROW | (UNBOUNDED | [num]) FOLLOWING)

(ROWS | RANGE) BETWEEN CURRENT ROW AND (CURRENT ROW | (UNBOUNDED | [num]) FOLLOWING)
(ROWS | RANGE) BETWEEN [num] FOLLOWING AND (UNBOUNDED | [num]) FOLLOWING
```

栗子

> 这里以rows between为例来讲解窗口范围的划分，rows表示物理层面上的行，跟字段值没关系。

```sql
--默认从第一行到当前行
select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid order by createtime) as pv1  
from website_pv_info;

--第一行到当前行 等效于rows between不写 默认就是第一行到当前行
select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid order by createtime rows between unbounded preceding and current row) as pv2
from website_pv_info;

--向前3行至当前行
select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid order by createtime rows between 3 preceding and current row) as pv4
from website_pv_info;

--向前3行 向后1行
select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid order by createtime rows between 3 preceding and 1 following) as pv5
from website_pv_info;

--当前行至最后一行
select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid order by createtime rows between current row and unbounded following) as pv6
from website_pv_info;

--第一行到最后一行 也就是分组内的所有行
select cookieid,createtime,pv,
       sum(pv) over(partition by cookieid order by createtime rows between unbounded preceding  and unbounded following) as pv6
from website_pv_info;
```

#### 排序函数

功能：主要对数据分组排序之后，组内顺序标号。

核心函数：==**row_number**==、rank、dense_rank 

适合场景：==**分组TopN问题**==（不是全局topN）

栗子

```sql
SELECT
    cookieid,
    createtime,
    pv,
    RANK() OVER(PARTITION BY cookieid ORDER BY pv desc) AS rn1,
    DENSE_RANK() OVER(PARTITION BY cookieid ORDER BY pv desc) AS rn2,
    ROW_NUMBER() OVER(PARTITION BY cookieid ORDER BY pv DESC) AS rn3
FROM website_pv_info;

--需求：找出每个用户访问pv最多的Top3 重复并列的不考虑
SELECT * from
(SELECT
    cookieid,
    createtime,
    pv,
    ROW_NUMBER() OVER(PARTITION BY cookieid ORDER BY pv DESC) AS seq
FROM website_pv_info) tmp where tmp.seq <4;
```

==ntile==函数

功能：将分组排序之后的数据分成指定的若干个部分（若干个桶）

规则：尽量平均分配 ，优先满足最小的桶，彼此最多不相差1个。

栗子

```sql
--把每个分组内的数据分为3桶
SELECT
    cookieid,
    createtime,
    pv,
    NTILE(3) OVER(PARTITION BY cookieid ORDER BY createtime) AS rn2
FROM website_pv_info
ORDER BY cookieid,createtime;

--需求：统计每个用户pv数最多的前3分之1天。
--理解：将数据根据cookieid分 根据pv倒序排序 排序之后分为3个部分 取第一部分
SELECT * from
(SELECT
     cookieid,
     createtime,
     pv,
     NTILE(3) OVER(PARTITION BY cookieid ORDER BY pv DESC) AS rn
 FROM website_pv_info) tmp where rn =1;
```

#### lag、lead函数

经典用法：查询用户连续登录

```hive
--LAG 用于统计窗口内往上第n行值
SELECT cookieid,
       createtime,
       url,
       ROW_NUMBER() OVER(PARTITION BY cookieid ORDER BY createtime) AS rn,
       LAG(createtime,1,'1970-01-01 00:00:00') OVER(PARTITION BY cookieid ORDER BY createtime) AS last_1_time,
       LAG(createtime,2) OVER(PARTITION BY cookieid ORDER BY createtime) AS last_2_time
FROM website_url_info;


--LEAD 用于统计窗口内往下第n行值
SELECT cookieid,
       createtime,
       url,
       ROW_NUMBER() OVER(PARTITION BY cookieid ORDER BY createtime) AS rn,
       LEAD(createtime,1,'1970-01-01 00:00:00') OVER(PARTITION BY cookieid ORDER BY createtime) AS next_1_time,
       LEAD(createtime,2) OVER(PARTITION BY cookieid ORDER BY createtime) AS next_2_time
FROM website_url_info;

--FIRST_VALUE 取分组内排序后，截止到当前行，第一个值
SELECT cookieid,
       createtime,
       url,
       ROW_NUMBER() OVER(PARTITION BY cookieid ORDER BY createtime) AS rn,
       FIRST_VALUE(url) OVER(PARTITION BY cookieid ORDER BY createtime) AS first1
FROM website_url_info;

--LAST_VALUE  取分组内排序后，截止到当前行，最后一个值
SELECT cookieid,
       createtime,
       url,
       ROW_NUMBER() OVER(PARTITION BY cookieid ORDER BY createtime) AS rn,
       LAST_VALUE(url) OVER(PARTITION BY cookieid ORDER BY createtime) AS last1
FROM website_url_info;
```

### 4.7.13. Hive调优

#### 文件存储格式

列式存储、行式存储

Hive中表的数据存储格式，不是只支持text文本格式，还支持其他很多格式。

hive表的文件格式是如何指定的呢？ 建表的时候通过==STORED AS 语法指定。如果没有指定默认都是textfile==。

Hive中主流的几种文件格式。

textfile 文件格式 

==ORC==、Parquet 列式存储格式。

```
都是列式存储格式，底层是以二进制形式存储。数据存储效率极高，对于查询贼方便。
二进制意味着肉眼无法直接解析，hive可以自解析。
```

栗子

> 分别使用3种不同格式存储数据，去HDFS上查看底层文件存储空间的差异。

```sql
--1、创建表，存储数据格式为TEXTFILE
create table log_text (
track_time string,
url string,
session_id string,
referer string,
ip string,
end_user_id string,
city_id string
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE;  --如果不写stored as textfile 默认就是textfile

--加载数据
load data local inpath '/root/hivedata/log.data' into table log_text;

--2、创建表，存储数据格式为ORC
create table log_orc(
track_time string,
url string,
session_id string,
referer string,
ip string,
end_user_id string,
city_id string
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
STORED AS orc ;

--向表中插入数据 思考为什么不能使用load命令加载？ 因为load是纯复制移动操作 不会调整文件格式。
insert into table log_orc select * from log_text;

--3、创建表，存储数据格式为parquet
create table log_parquet(
track_time string,
url string,
session_id string,
referer string,
ip string,
end_user_id string,
city_id string
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
STORED AS PARQUET ;

--向表中插入数据 
insert into table log_parquet select * from log_text ;
```

