---
layout: post
title: 'Upgrade Gitlab 7.0 to 7.2'
date: 2014-09-08 16:14
comments: true
tags: [GitLab]
---
> update: 2014-10-08

> 正確的更新方式應該為 先從 7.0 升到 7.1 ，再升到 7.2，且按照官方的文件執行即可

-ERROR-

整個升級過程其實還算順利，只不過 7.2 的資料表 `projects` 增加了一個欄位 `star_count`，似乎是用來計算有多少人""star" 這個專案，而 backup restore 的過程中卻會把 7.2 的資料表取代成 7.0 的資料表版本，所以程式會找不到 `projects`.`star_count` 這個欄位，一進到 gitlab 的專案列表就會出現 500

查詢 log:

    ActionView::Template::Error (Mysql2::Error: Unknown column 'projects.star_count' in 'field list'
    ...

後來的做法就是手動替該資料表加上 `star_count` 欄位囉

    #SQL
    ALTER TABLE projects ADD star_count int(11) NOT NULL DEFAULT '0';
    CREATE INDEX index_projects_on_star_count USING btree ON projects (star_count);

-//ERROR-

reference:

[gitlab: backup](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/raketasks/backup_restore.md)

[ruby on rails: add_index](http://apidock.com/rails/v4.0.2/ActiveRecord/ConnectionAdapters/SchemaStatements/add_index)

[mysql: alter column](http://dev.mysql.com/doc/refman/5.1/en/alter-table.html)
