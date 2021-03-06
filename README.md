
# *框架描述*
 >+ 该框架是解决分布式系统中的分布式事务问题,该框架是保证分布式事务的强一致性,事务日志数据存储于redis,
    为了保障redis的高可用可把redis部署为redis cluster模式以及开发混合持久化机制,可把redis部署为当日志
    数据量比较大的时候数据基于纯内存操作,有助于提升框架的性能,其中在在代码层面上设置了redis的key的过期
    时间,以防redis数据过多导致内存溢出或者导致频繁的 full gc,在数据存储在redis过程中,如果存储失败,则会
    触发重试逻辑,从而保证数据同步的成功,但是这用又引入了一个新的问题,如果数据一直重试,导致框架一直处于
    重试逻辑从而影响系统的性能,所以在这一方面的逻辑在后面进行优化
   
# *使用详解*
 >+ 详细请看mitbook-test工程
 
# 设计原理
 >+ 目前不提供原理讲解,可自行阅读源码理解原理,后面的设计文档会进一步完善
 
# *支持db*
 >+ 市面上的db都支持,只要是符合jdbc规范的数据库都支持
 
# *技术选型*
 >+ springboot,aop,redis等等
 
# 测试地址
 >+ *<http://localhost:8066/order/saveOrder?orderNo=12222&userId=1000&productId=1&productNum=1>*
 
# *注意*
 >+ 未经本人允许请勿用于商业
 >+ 该框架目前性能不是很好,后期会通过rpc或者netty来解决性能问题
 >+ mitbook-test工程中存在订单扣减问题,不必在意,这不是该分布式框架问题,而是订单扣减库存问题,故不作处理
 >+ 如果看日志打印的英文不懂,请看:*https://github.com/mitbook/mitbook-mountain/commit/6e136e7f3b1313b68c94761cad16c05e68212e3d*
 
# *集成第三方框架使用*
 1. 引入maven依赖
 ``` java
 
 <dependency>
    <groupId>com.mitbook</groupId>
    <artifactId>mitbook-stater</artifactId>
    <version>1.0</version>
  </dependency>
  
  ```
  2. 在启动类上加上@EnableGlobalTransactional注解,就能解决分布式事务问题
  
# *代码贡献说明*
 >+ 如源码爱好者有更好思想,欢迎来扰,本人以真诚的谢意欢迎您来贡献
 >+ 如发现bug请及时与我联系,本人看到消息会在第一时间联系你,帮您解决问题
 >+ 本框架只应用于学习,不应用商业,如需应用商业,请与本人联系,谢谢
 
# *建议*
 >+ 建议使用redis cluster架构模式来保障redis的高可用(可开启redis的混合持久化来保证redis的高可用)
