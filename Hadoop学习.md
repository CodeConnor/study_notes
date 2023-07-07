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



