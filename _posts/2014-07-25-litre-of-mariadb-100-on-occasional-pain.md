---
layout: post
title: '升上 MariaDB 10.0 後，Redmine 又爆了'
date: 2014-07-25 09:22
comments: true
tags: [Redmine, Arch, MariaDB10.0, mysql2]
---
上次小弟才剛升級完 MariaDB 10.0 ，原本想說都沒事，網路服務都很正常，沒想到今天一重開機，Redmine 就爆了

又是 Redmine

又是 Redmine

又是 Redmine

    require': Incorrect MySQL client library version! This gem was compiled for 5.5.34-MariaDB but the client library is 10.0.10-MariaDB. (RuntimeError) from /usr/local/rvm/gems/ruby-2.1.0/gems/mysql2-0.3.15/lib/mysql2.rb:8:in'

類似這樣的訊息

＝＝ 恩，好啦，其實整件事情跟 Redmine 本身是沒關係的

-clear-

那麼網路上查了一下，原來是之前安裝的 mysql2(gem) 適用於 MariaDB 5.5，由於我升到 MariaDB 10.0 ，所以我要再重新

> compile mysql2 against MariaDB 10.0.10

網路上已經有相關的 issue : [Error while connecting MariaDB v10.0.10](https://github.com/brianmario/mysql2/issues/506)

那做法上就是移除之前的 mysql2，重新 compile mysql2 並加上 --with-mysql-config 參數

	# Reinstall mysql2 with Configuration options --with-mysql-config On Arch Linux

    [redmine@localhost ~] gem uninstall mysql2
    [redmine@localhost ~] gem install mysql2 -- --with-mysql-config=/usr/bin/mysql_config
    [redmine@localhost ~] cd /path/to/redmine/project
    [redmine@localhost redmine] bundle config build.mysql2 --with-mysql-config=/usr/bin/mysql_config
    [redmine@localhost redmine] bundle update

> Note:<br/>
> bundle config build.mysql2 --with-mysql-config=/usr/bin/mysql_config
> 
> After running this command, every time bundler needs to install the mysql gem, it will pass along the flags you specified.

這樣基本上就完成了，接著執行 rake 產生 secret token

    [redmine@localhost redmine]$ rake generate_secret_token

回到 sudoer 用 systemctl 重新執行 redmine ，我的 redmine 就回來囉～

    [sudoer@localhost ~]$ sudo systemctl restart redmine

###Note###

[brianmario/mysql2](https://github.com/brianmario/mysql2#configuration-options) ：A modern, simple and very fast Mysql library for Ruby - binding to libmysql

[Force re-installing the MySQL gem](https://wincent.com/wiki/Force_re-installing_the_MySQL_gem)

[BUNDLE-CONFIG](http://bundler.io/v1.3/man/bundle-config.1.html)