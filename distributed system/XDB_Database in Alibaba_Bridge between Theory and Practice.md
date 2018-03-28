# XDB:Database in Alibaba:Bridge between Theory and Practice
## new spring for system
## 挑战
### 冷热
### 迁移
* 高可用，赋值，一致性
### 软硬件结合
* rdma
* oracle之类的久远不适用
### 子主题 4
## X-DB
### 分布式数据库
### 核心技术
* 高可用
    * X-Paxos
        * 节点角色
            * proposer
            * accepter
            * learner
            * state machine
概要组合
            * proposer
            * accepter
            * learner
            * state machine
        * 干掉同步等待
* 分布式
    * GMS/LMS
* 存储引擎
    * X-Engine
        * 为高性能低成本设计
        * 数据自动冷热分层
        * 基于数据分层架构下的计算和存储优化
        * 
* 存储计算分离
* 异构计算加速
* SQL Engine
### Paxos
### Tuning Paxos for hight-throughput with batching and pipelining
### raft
* 支不支持空洞和乱序
### index
* data locality
* Cache craftiness for fast multicore key-value storage
* improving index performance through prefetching
### log
* 子主题 1
### 行存列存 - 数据的访问Pattern
### 冷热识别、anti-caching
### 自适应编码
### pelonton: the self-driving data base management system
### the case for learned index structure
### machine learning for systems and systems for machine learning
概要P
### Paxos
### Tuning Paxos for hight-throughput with batching and pipelining
### raft
### index
### log
### 行存列存 - 数据的访问Pattern
### 冷热识别、anti-caching
### 自适应编码
### pelonton: the self-driving data base management system
### the case for learned index structure
### machine learning for systems and systems for machine learning
### 做到极致
* 延时不影响吞吐
### 加快犯错速度，马上实施，恢复手段，业务信任
### ddl 慢 阻塞dml
### 计算存储分离
* serverless
    * 无状态的计算节点
* filtering pushdown
    * 查询过滤条件、下沉无关数据
### 异构计算加速
* FPGA加速、GPU加速
    * 适合大并发、计算密集型、逻辑简单
        * 压缩、解压、后端、merge
### 分布式
* 事物
    * 2PC vs OCC
        * 冲突-2PC（锁）；无冲突-OCC（无锁）
* 一致读
    * 问题：无法定序
    * TrueTime vs 中心化 vs 因果一致性
        * 同步硬件TrueTime
        * 因果一致性：有关系的有顺序，无关系无顺序。但是无法解决外部一致性
### 智能化DB
* 自运维
## DB新技术奠基之作
### HStore
### Hekaton
### HyPer
### HANA
### voteDB
## OLTP through the looking glass, and what we found there
### decoupling
### 2b3l
