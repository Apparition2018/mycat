# MyCat
分布式数据库系统中间层

---
## 参考网站
1.[MyCat1.6权威指南](https://github.com/MyCATApache/Mycat-Server)
---
## MyCat 介绍
>### MyCat 作用
>1. 实现数据库的读写分离
>2. 支持读负载均衡
>3. 支持后端 MySQL 高可用
>4. 数据库垂直拆分
>    - 把相互并不影响的模块单独拆分出来，形成不同的库，如：用户库，订单库，支付库
>    - 经常一起查询的列放在一起
>    - text，blob 等大字段拆分出到附加表中
>5. 数据库水平拆分（分库分表）
>6. 数据库连接池
>7. 支持通过 jdbc 连接多种数数据库
>### MyCat 应用场景
>1. 需要进行读写分离的场景
>2. 需要进行分库分表的场景
>3. 多租户场景
>4. 数据统计系统
>5. HBASE 的一种替代方案
>6. 需要使用同样的方式查询多种数据库的场景
>### MyCat 优势
>1. 基于阿里的 Cobar 系统开发
>2. 开发社区活跃
>3. 完全开源可以自定义开发
>4. 支持多种关系型及 NoSQL 数据库
>5. 使用 Java 开发，可以部署在多种系统上
>6. 具有在多种行业和项目中应用的成功案例
---
## MyCat 基础
>### 基本概念
>- 逻辑库：对应多个数据库
>- 逻辑表：对应多个数据库中的表
>### 关键特性
>- 支持 SQL92 标准
>- 支持 MySQL 集群
>- 支持 JDBC 连接数据库
>- 支持 NoSQL 数据库
>- 支持自动故障切换，高可用性
>- 支持读写分离
>- 支持全局表
>- 支持独有的基于 ER 关系的分片策略
>- 支持一致性 HASH 分片
>- 支持多平台，部署简单方便
>- 支持全局序列号
>### 安装 MyCat
>1. 安装 Java 环境，下载 MyCat
>   1. yum install java-1.8.0-openjdk java-1.8.0-openjdk-devel
>   2. cd /home/ljh/下载
>   2. wget http://dl.mycat.org.cn/1.6.7.6/20201126013625/Mycat-server-1.6.7.6-release-20201126013625-linux.tar.gz
>   3. tar zxf Mycat-server-1.6.7.6-release-20201126013625-linux.tar.gz
>   4. mv mycat /usr/local
>2. 新建 MyCat 用户（Linux 下建议为每个一款软件建立独立的运行账号）
>   1. adduser mycat
>   2. chown mycat:mycat -R mycat，更改文件拥有者
>3. 配置环境变量
>   1. which java
>   2. ls -l /usr/bin/java
>   3. ls -l /etc/alternatives/java
>   4. vi /etc/profile
>       1. export JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk.x86_64
>       2. export MYCAT_HOME=/usr/local/mycat
>4. 启动 MyCat
>   1. su mycat
>   2. $MYCAT_HOME/bin/startup_nowrap.sh
>### MyCat 配置文件
>1. schema.xml: 配置逻辑库表及数据节点
>   - &lt;schema&gt;&lt;table&gt;&lt;/table&gt;&lt;/schema&gt; 定义逻辑库表
>   - &lt;dataNode&gt;&lt;/dataNode&gt; 定义数据节点
>   - &lt;dataHost&gt;&lt;/dataHost&gt; 定义数据节点的物理数据源
>2. rule.xml: 配置表的分片规则
>   - &lt;tableRule name=""&gt;&lt;/tableRule&gt; 定义表使用的分片规则
>   - &lt;function name=""&gt;&lt;/function&gt; 定义分片算法
>3. server.xml: 配置服务器权限
>   - &lt;system&gt;&lt;property name=""&gt;&lt;/property&gt;&lt;/system&gt; 定义系统配置
>   - &lt;user&gt;&lt;/user&gt; 定义连接 MyCat 的用户
---