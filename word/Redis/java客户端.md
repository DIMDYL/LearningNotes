## 常用的Redis java客户端

Spring提供了SpringDataRedis操作jedis和lettuce

#### jedis

以redis命名的方法名称，学习成本低，但是jredis是线程不安全的，多线程环境下要基于连接池来使用

#### lettuce

是基础netty实现的，支持同步，异步和响应式编程方式是线程安全的，支持redis的哨兵模式、集群模式和管道模式

#### redisson

基于redis实现的分布式、可伸缩的java数据结构集合、包含map、Queue、Lock、Semaphore、AtomicLong等功能