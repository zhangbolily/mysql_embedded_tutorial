---
description: 本教程的主题不是在嵌入式平台进行数据库开发。
---

# 一、课程简介



1. 什么是MySQL Embedded？

MySQL是当下热门的网络应用数据库，经常被用作网站后台数据库、线上服务的后端数据平台。在这些应用场景中，MySQL一般是作为服务端出现的，客户端通过网络连接向服务器请求数据。MySQL Embedded（嵌入式的MySQL）则与之不同，它可以把MySQL服务器完全嵌入到你的应用程序中。无需通过网络连接来获取数据，你的应用可以像MySQL服务端一样直接读取本地数据文件，进行数据的查询、修改等操作。

这就是MySQL Embedded，一种嵌入式的数据库。另一个广为人知的嵌入式数据库就是SQLite，在很多需要小型的数据存储场景中都可以看到它。不过相对于SQLite而言，MySQL的嵌入式版本没有损失服务器版本的重要特性，高并发、行级锁等特性全部得到了保留，而这些特性是SQLite完全没有的。

MySQL嵌入式版本最大的优势不仅是其性能表现比其他的嵌入式数据库更加优异，拥有诸多其他数据库不支持的高级特性，更重要的在于它的开发成本上。MySQL嵌入式版本的函数接口和服务器版本是完全一致的，您无需重新学习如何使用这些API。两者之间主要的不同点仅仅在于配置MySQL数据库连接的方式。在您配置并且启动嵌入式MySQL之后，可以像服务器版本一样使用MySQL。

2. 我将学到什么？

本教程分为入门课程、中级课程、高级课程。

入门课程会分为两部分：第一部分是熟悉MySQL Embedded的相关概念、配置好开发环境；第二部分首先一步步引导您启动第一个嵌入式MySQL程序，然后通过一些基础案例帮助您理解MySQL嵌入式版本的基本概念、运行机制。

中级课程建立在入门课程基础之上，你必须拥有入门课程的知识基础才能进入这一课程的学习。中级课程通过一些案例，完成MySQL高并发程序的开发，着力于应用MySQL的一些高级特性。

高级课程需要您对MySQL有更深入的理解，我们会在高级课程中应用InnoDB存储引擎进行高级嵌入式数据库的开发。

3. 学习这个教程的知识基础

* 掌握基本的SQL语句，例如创建数据库、建表、插入数据、查询数据、修改数据
* 拥有良好的C++基础
* 了解Linux平台下的多线程机制

