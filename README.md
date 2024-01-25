# 2024年1月
- 2024-01-25 [weakptr一般和sharedptr配合使用而不增加引用计数](https://blog.csdn.net/qq_38410730/article/details/105903979)：（1）解决循环引用的问题（2）使用lock()解决多线程中共享对象安全问题。
- 2024-01-24 [AWS re:Invent2023 Aurora 发布了啥？](http://mysql.taobao.org/monthly/2023/12/01/)：但个人对分布式事务和主从切换这个主题不甚了解，需后续关注
- 2024-01-23 [MotherDuck: DuckDB in the cloud and in the client](https://www.cidrdb.org/cidr2024/papers/p46-atwal.pdf) [中文](https://zhuanlan.zhihu.com/p/679197332)，配合这个文章食用可能会更好：[万字解读 | A轮就融资￥3亿+的MotherDuck到底是个啥？](https://www.rachellaw.xyz/2023/MotherDuck), 但通篇读下来，并没有GET到其优势在哪，就主打一个可以利用本地计算机+云上的HybridQuery？
- 2024-01-14 glibc2.17的fseek会导致频繁的mmap和munmap，进而获取mmap_sem的写锁，使得pagefault无法获取mmap_sem的读锁，导致两个调用栈锁争用过高，[最终产生了CPU利用率不高的问题，升级glibc2.35可以解决](https://zhuanlan.zhihu.com/p/669173594)
- 2024-01-12 了解学习了向量数据库，以及向量搜索。向量搜索可以把文本、语音、图像等转换为向量然后使用向量最近邻检索（KNN）来实现近似查询：[AI大模型与向量数据库 PGVECTOR](https://mp.weixin.qq.com/s?__biz=MzU5ODAyNTM5Ng==&mid=2247485589&idx=1&sn=931f2d794e9b8486f623f746db9f00cd&scene=21#wechat_redirect)
- 2024-01-11 了解一种新的HDD技术SMR，可以降低成本10%左右，但可能需要上层研发新的引擎替换EXT4：[阿里](https://www.usenix.org/system/files/fast23-zhou-su.pdf)；[谷歌](https://blog.google/products/google-cloud/dynamic-hybrid-smr-ocp-proposal-improve-data-center-disk-drives/)；[DropBox](https://dropbox.tech/infrastructure/four-years-of-smr-storage-what-we-love-and-whats-next)
- 2024-01-10 [CMAKE编译链接动态库可以使用脚本控制暴露的函数](https://www.gnu.org/software/gnulib/manual/html_node/LD-Version-Scripts.html)， [否则会出现不同库中重名函数冲突的问题](https://stackoverflow.com/questions/37051635/several-shared-object-using-same-proto-leading-the-the-error-file-already-exist).

