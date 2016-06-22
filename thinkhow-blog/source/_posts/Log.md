---
title: The importance of Log in Distributed Systems
date: 2016-06-22 00:24:26
tags:
---
来自Linkedin工程师Jay Kreps的一篇关于Log的文章：
https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying

这篇文章是我在进行深入研究Kafka前读的一篇文章，讲的是Log在Distributed Systems中的作用以及用Database作为一个类比讲述Log的作用。

### What is a log?
`A log is perhaps the simplest possible storage abstraction. It is an append-only, totally-ordered sequence of records ordered by time.`
简单来说，Log就是一个带有自增序列的消息。这里的序列有点像我们在DS中学到的Logical Clock。

### Clarify something that is a bit confusing
`Log VS. unstructured error messages`
不同于平常我们经常见到的比如说运行异常的error log，这里讲的Log我觉得更像是"Transction"。下面就会体会到了。

### Logs in databases
`The usage in databases has to do with keeping in sync the variety of data structures and indexes in the presence of crashes. To make this atomic and durable, a database uses a log to write out information about the records they will be modifying, before applying the changes to all the various data structures it maintains.`
还记得我们在DS中学的Transction的四个性质吗？没错就是ACID。这里说Log的作用是为了实现A(Atomic)和D(Durability)。是不是感觉有点像简化版的Transction了呢？

`Over-time the usage of the log grew from an implementation detail of ACID to a method for replicating data between databases. It turns out that the sequence of changes that happened on the database is exactly what is needed to keep a remote replica database in sync.`
有点不理解，但这里我感觉作者讲的Log就是Transction。

### Logs in distributed systems
`If two identical, deterministic processes begin in the same state and get the same inputs in the same order, they will produce the same output and end in the same state.`
关键词：Deterministic

` The purpose of the log here is to squeeze all the non-determinism out of the input stream to ensure that each replica processing this input stays in sync.`
其实，说的就是利用Log来实现DS的consistency嘛！

### "state machine model (active-active model)"　VS. "primary-backup model (active-passive model)"
其实就是Master-slaver和Peer-to-peer的对比。
State machine model是先写进log，然后每个Peer读Log从而更新自己的State。
Primary-backup model是先由Master写进log, Slaver再去读和更新自己的State。

要注意的是，这里举的例子说的是：
State Machine model的log记录的是《操作》，每个Peer读log后都去执行这个操作。
Primary-backup model是让Master直接执行操作得到结果，每个Slaver去读这个结果而不用执行操作。

### Changelog 101: Tables and Events are Dual
你有一个记录了所有操作的Log的话，那么这个系统的任何时候的状态都可以通过这个Log得到。

`So in this sense you can see tables and events as dual: tables support data at rest and logs capture change. The magic of the log is that if it is a complete log of changes, it holds not only the contents of the final version of the table, but also allows recreating all other versions that might have existed.`
Table是最后的结果，而Log是每一次的变化。这里有没有让你想起一个东西？对！就是版本控制(Version Control)。

`There is a close relationship between source control and databases. Version control solves a very similar problem to what distributed data systems have to solve—managing distributed, concurrent changes in state. A version control system usually models the sequence of patches, which is in effect a log. You interact directly with a checked out "snapshot" of the current code which is analogous to the table. You will note that in version control systems, as in other distributed stateful systems, replication happens via the log: when you update, you pull down just the patches and apply them to your current snapshot.`
直接看吧。。。
