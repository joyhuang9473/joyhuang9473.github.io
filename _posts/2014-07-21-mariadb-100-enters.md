---
layout: post
title: 'MariaDB 10.0 enters'
date: 2014-07-21 14:53
comments: true
tags: [Arch, MariaDB10.0, multi-source replication, Cassandra integration, engine independent statistics]
---
最近幫 Arch 更新時才發現 MariaDB 已經到 10.0 了，記得之前還是 MariaDB 5.5，想說是不是自己太久沒更新

但看 MariaDB 官網的 Download list ，的確是從 5.5 升到 10.0 及 10.1

[MariaDB - All Releases](https://downloads.mariadb.org/mariadb/+releases/)

但為甚麼不將新版本取名為 MariaDB 5.6 而是直接跳到 MariaDB 10.0 ?

因此不小心好奇了一下，尋找它的版本命名由來，所幸找到一篇翻譯文，翻得還蠻清楚的，以下摘錄：

開源中國社區：[MariaDB 10.0 和 MySQL 5.6 有何不同](http://www.oschina.net/translate/mariadb-10-0-and-mysql-5-6)
原文：[MariaDB 10.0 and MySQL 5.6](http://blog.mariadb.org/mariadb-10-0-and-mysql-5-6/)

> 1. MySQL5.6 的代码库的文件结构已经被改动了。比如单个代码文件已经被分成多个，又或者是某些代码已经被重新归类到了不同的文件内。所以要把MariaDB 去配合现在这个文件结构一定是一个非常消耗时间的过程。

> 2. MairaDB 5.5 已经有大量的代码不同于MySQL 5.5 的版本，而且也有很多的新的特征被整合到MariaDB 5.5 中，而这些特征直到 5.6 版本才出现在MySQL中。所以我们在比较同样功能的MySQL 和MariaDB的版本，同时在完成设计和QA方面的审核后，一个很明显的结论是MariaDB会是一个更好的产品。

> 由于我们引入了一些新功能（像 [multi-source replication](https://mariadb.com/kb/en/mariadb/mariadb-documentation/replication-cluster-multi-master/replication/multi-source-replication/)多源复制, [Cassandra integration](https://mariadb.com/kb/en/mariadb/mariadb-documentation/mariadb-storage-engines/storage-engines-cassandra-storage-engine/), [engine independent statistics](https://mariadb.com/kb/en/mariadb/mariadb-documentation/optimization-and-tuning/engine-independent-table-statistics/)独立统计系统等），所以我们需要搞个新版本。通常当你引入新功能时，你需要新建个版本。

> 下个版本称作“MariaDB5.6”是不准确的，因为他不是基于Mysql5.6，取而代之，我们决定版本号调为10.0

恩，因此簡而言之，MariaDB 並不是基於 Mysql 5.6 ，並且多了 multi-source replication, Cassandra integration, engine independent statistics 等新功能，故將版本號一口氣提升到 10.0 ，作為 MariaDB 邁入另一個里程碑的紀念（?）

那麼在 Arch 的 MariaDB 升級上面，官方要我們 restart mysqld.service 和 run mysql_upgrade

before

    [user@localhost ~]$ sudo systemctl status mysqld
    ...
    Jul 16 13:48:59 localhost mysqld[203]: Version: '5.5.37-MariaDB-log'  socket: '/run/mysqld/mysqld.sock'  ...erver

after

    [user@localhost ~]$ sudo systemctl status mysqld
    ...
    Jul 21 14:43:40 localhost mysqld[5451]: Version: '10.0.12-MariaDB-log'  socket: '/run/mysqld/mysqld.sock'...erver

[Arch News : MariaDB 10.0 enters [extra]](https://www.archlinux.org/news/mariadb-100-enters-extra/)
[What is MariaDB 10.0?](https://mariadb.com/kb/en/mariadb/what-is-in-the-different-mariadb-releases/what-is-mariadb-100/)

