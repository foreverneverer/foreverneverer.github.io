# 2024年2月
- 2024-02-30 where和prewhere的区别是：前者作用在读取后数据结果集跳过CPU计算行，后者作用在数据源用于跳过IO读取行.但是前者往往利用索引加速查询，也可以跳过部分IO读取行
- 2024-02-29 CBO基于成本的优化，可以理解动态预估查询开销，而RBO基于特定规则进行优化，不如前者灵活
- 2024-02-28 计算下推包括：投影下推（Projection Pushdown）选择下推（Selection Pushdown）聚合下推（Aggregation Pushdown）排序下推（Sort Pushdown）连接下推（Join Pushdown）分布式数据洗牌下推（Distributed Data Shuffle Pushdown）选择位图下推（Selection Bitmap Pushdown）：[计算下推的分类](https://kimi.moonshot.cn/share/cpshtcf2337j30lspvvg)
- 2024-02-27 Rockset的核心不同点是能够构建全部的能够自动在任何数据（包括结构化、半结构化、地理和时间序列数据）上构建Converged Index™，并使用大量的空间持久化这些索引
- 2024-02-26 谓词是返回 bool 型（或可隐式转换为 bool 型）的函数。一般来说，where 中的条件单元都是谓词：=, >, <, >=, <=, BETWEEN, LIKE, IS [NOT] NULL <>, IN, OR, NOT IN, NOT LIKE，谓词下推是指将查询语句中的过滤表达式尽可能下推到距离数据源最近的地方做计算，以尽早完成数据的过滤，进而显著地减少数据传输或计算的开销。下推前：`select count(1) from t1 A join t3 B on A.a = B.a where A.b > 100 and B.b > 100`; 下推后：`select count(1) from (select * from t1 where a>100) A join (select *  from t3 where b<100) B on A.a = B.a`; [MySQL生态现有计算下推方案汇总](https://dbkernel.com/2024/03/06/mysql-pushdown-summary/)
- 2024-02-25 Clickhouse的索引主要包括稀疏索引(一级索引)，和跳数索引（二级索引），其中注意二级索引中的index_granularity和granularity区别，前者就是常见的8192行，后者其实是mark数。最常见的为minmax索引：[ClickHouse的索引深入了解](https://zhuanlan.zhihu.com/p/658631866)
- 2024-02-24 SQL执行被分为编译型和向量化执行两种模式，使用融合模式可以加速数据读取：[Incremental Fusion: Unifying Compiled and Vectorized Query Execution](https://www.cs.cit.tum.de/fileadmin/w00cfj/dis/papers/inkfuse.pdf)
- 2024-02-23 [SALI](https://arxiv.org/pdf/2308.15012?) 为了提高索引的性能和效率，业内引进了学习索引，通过学习模型来预测数据存储位置，进一步提高查找效率，[GITHUB](https://github.com/cds-ruc/SALI)
- 2024-02-22 [Lion](https://arxiv.org/pdf/2403.11221)通过预先调整分区位置，使得分布式事务的分区尽量放置在同一节点避免分布式事务的影响
- 2024-02-21 [hudi,iceberg,paimon比较](https://mp.weixin.qq.com/s/NIpud2kbiJJNOsje0Honyw), 很详细尤其是最后的对比
- 2024-02-20 [Doris支持Variant](https://cdn.selectdb.com/static/0409_Apache_Doris_Variant_a5ca19cdcc.pdf)，类似Bytehouse的隐式MAP列，实际为隐式JSON列，更为灵活
- 2024-02-19 本地版CK一致性问题是由于数据的只能保证最终一致性：(1) 数据的变更只能等待后台合并才能一致 (2) 分布式表的数据写入是异步的。参见：[ClickHouse-数据一致性](https://www.cnblogs.com/EnzoDin/p/16251252.html)
- 2024-02-19 析构函数请确保不能有异常，以免资源释放被中断引起内存泄漏
- 2024-02-18 clickhouse cloud已经支持了DistributedCacheService: [ClickHouse Cloud Update Call]( https://www.youtube.com/watch?v=Ew8vHeyyahI)
- 2024-02-17 [PG生态新玩家ParadeDB](https://mp.weixin.qq.com/s/bx2dRxlrtLcM6AD2qsplQQ)
- 2024-02-16 snowflake推出[marketplace](https://www.snowflake.com/en/data-cloud/marketplace/)用于提供数据和原生APP，如covid-19的流行病学数据可以免费获取
- 2024-02-15 [Streamlit](https://github.com/streamlit/streamlit) — A faster way to build and share data apps
- 2024-02-14 snowflake推出[SPI指标](https://www.snowflake.com/blog/measuring-performance-improvements-spi/)用于衡量过去客户稳定负载下的性能提升，同时维护[文档记录各项优化措施](https://docs.snowflake.com/en/release-notes/performance-improvements)
- 2024-02-13 SelectDB发布[X2Doris](https://www.selectdb.com/blog/160)，加速数据迁移
- 2024-02-12 数据库勿删恢复方案包括：基于快照的恢复和基于增量日志的恢复，PolarDB支持Query级别的日志恢复操作，命名为[SQL闪回](https://help.aliyun.com/zh/polardb/polardb-for-xscale/use-sql-flashback-1)
- 2024-02-11 [OceanBase 4.2.2 GA 发布，全新特性快速预览！](https://open.oceanbase.com/blog/9147296848)

# 2024年1月
- 2024-01-26 [CXL技术可以解决内存池化的需求，数据中心利用CXL做解耦和池化，CXL技术能够让不同的资源从紧耦合变成松耦合，让相同的资源变成池化资源，会形成CPU资源池、GPU资源池以及内存资源池，各个资源池通过CXL连接。](https://www.elecfans.com/d/2210036.html)，CIDR2024展示了利用CXL集成数据库的一些探索：[Database Kernels: Seamless Integration of Database Systems and Fast Storage via CXL](https://www.cidrdb.org/cidr2024/papers/p43-lee.pdf)
- 2024-01-25 [weakptr一般和sharedptr配合使用而不增加引用计数](https://blog.csdn.net/qq_38410730/article/details/105903979)：（1）解决循环引用的问题（2）使用lock()解决多线程中共享对象安全问题。
- 2024-01-24 [AWS re:Invent2023 Aurora 发布了啥？](http://mysql.taobao.org/monthly/2023/12/01/)：但个人对分布式事务和主从切换这个主题不甚了解，需后续关注
- 2024-01-23 [MotherDuck: DuckDB in the cloud and in the client](https://www.cidrdb.org/cidr2024/papers/p46-atwal.pdf) [中文](https://zhuanlan.zhihu.com/p/679197332)，配合这个文章食用可能会更好：[万字解读：A轮就融资￥3亿+的MotherDuck到底是个啥？](https://www.rachellaw.xyz/2023/MotherDuck), 但通篇读下来，并没有GET到其优势在哪，就主打一个可以利用本地计算机+云上的HybridQuery？
- 2024-01-22 [大模型时代，Databricks 向左，Snowflake 向右](https://zhuanlan.zhihu.com/p/677745764), 文中阐述了大模型时代两家公司对AI的投入和方向，实话实话，没有太理解，好像一个是做方案产品，一个是增强AI引擎？
- 2024-01-14 glibc2.17的fseek会导致频繁的mmap和munmap，进而获取mmap_sem的写锁，使得pagefault无法获取mmap_sem的读锁，导致两个调用栈锁争用过高，[最终产生了CPU利用率不高的问题，升级glibc2.35可以解决](https://zhuanlan.zhihu.com/p/669173594)
- 2024-01-12 了解学习了向量数据库，以及向量搜索。向量搜索可以把文本、语音、图像等转换为向量然后使用向量最近邻检索（KNN）来实现近似查询：[AI大模型与向量数据库 PGVECTOR](https://mp.weixin.qq.com/s?__biz=MzU5ODAyNTM5Ng==&mid=2247485589&idx=1&sn=931f2d794e9b8486f623f746db9f00cd&scene=21#wechat_redirect)
- 2024-01-11 了解一种新的HDD技术SMR，可以降低成本10%左右，但可能需要上层研发新的引擎替换EXT4：[阿里](https://www.usenix.org/system/files/fast23-zhou-su.pdf)；[谷歌](https://blog.google/products/google-cloud/dynamic-hybrid-smr-ocp-proposal-improve-data-center-disk-drives/)；[DropBox](https://dropbox.tech/infrastructure/four-years-of-smr-storage-what-we-love-and-whats-next)
- 2024-01-10 [CMAKE编译链接动态库可以使用脚本控制暴露的函数](https://www.gnu.org/software/gnulib/manual/html_node/LD-Version-Scripts.html)， [否则会出现不同库中重名函数冲突的问题](https://stackoverflow.com/questions/37051635/several-shared-object-using-same-proto-leading-the-the-error-file-already-exist).

