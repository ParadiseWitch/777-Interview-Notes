---
description: 全是从面经里扒拉出来的面试题
---

# 常见问题

> 看面经感觉字节问数据库问得比较少

## 索引结构

## MySQL 怎么判断一条查询语句命中索引

## 索引

> 相关问题：
>
> * 优缺点、什么场景适合等等
> * 索引的作用、特点、哪种数据加索引比较好
> * 什么时候索引失效

## **范式**

## **事务**

## 数据库**频繁读数据**，可以用什么方式来优化

## 手写SQL语句，分组查询

## 数据库原子性

## 数据库inner join、left join、right join分别是干嘛的

## 数据库事务

## SQL 语句，group by

## 为什么需要 rollback

## MySQL不同引擎的区别

## 不同引擎的索引区别 

## 存储过程

## MySQL的多线程并发是怎么做的

## MySQL线程池怎么设计的

## 你数据库中表是怎么设计的，表与表怎么关联的



Tencent

如果数据量比较大的情况下，你会怎么建索引？// 

博客的正文用哪一种数据类型来存的？对这个类型建索引会遇到什么问题？// 

你的 MySQL 用的什么引擎？简单介绍一下 Inno DB？Inno DB 的索引是怎么实现的？

// 默认的就是innodb

了不了解主键索引和聚簇索引？// [link](https://baike.baidu.com/item/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B4%A2%E5%BC%95)

这时候另一个面试官发话了，问有没有可能一种查询不需要回表也能直接返回数据？

那这个联合索引可能有个顺序，你一般怎么设计？哪个放前面？你会基于什么考虑？

如果我想用 order by 关键字来排序，我怎么利用索引来排序？就是怎么利用这个组合索引来排序？

一条 SQL 语句可能执行比较慢，你会怎么来排查？在 explain 里面查询它的执行计划，是怎么知道它用到哪些索引？

项目用的什么数据库 //mysql

存储 sql 查询语句怎么写，两张表，左连接

有些SQL比较慢，你咋办？为什么有的SQL这么慢，说说你觉得导致SQL很慢的原因

我看你还会这个MySQL，那我们来问问MySQL中的锁。你知道有哪些锁吗？

行锁有啥用啊，相对于表锁？

知道MySQL主要的两种引擎吗，MySIAM和InnoDB的区别，使用场景？谁有表锁？

看你了解InnoDB，那你具体说说InnoDB吧。

三大范式

索引

怎么知道命中索引
