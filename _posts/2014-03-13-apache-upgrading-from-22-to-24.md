---
layout: post
title: 'Apache Upgrading from 2.2 to 2.4'
date: 2014-03-13 16:27
comments: true
tags: [Apache]
---
2014-03-14

今天剛更新完 apache ，啟動時出現錯誤訊息：

> Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.

後來發現原來是

> libphp5.so included with php-apache does not work with mod_mpm_event

解決辦法：

replace

	LoadModule mpm_event_module modules/mod_mpm_event.so

to

	LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

而且 Access rule 也有些修改

2.2 configuration:

    Order deny,allow
    Deny from all

2.4 configuration:

    Require all denied

2.2 configuration:

    Order allow,deny
    Allow from all

2.4 configuration:

    Require all granted

參考資料：

[http://httpd.apache.org/docs/2.4/upgrading.html](http://httpd.apache.org/docs/2.4/upgrading.html)

[https://wiki.archlinux.org/index.php/LAMP#PHP](https://wiki.archlinux.org/index.php/LAMP#PHP)

[https://bbs.archlinux.org/viewtopic.php?id=178124&p=1](https://bbs.archlinux.org/viewtopic.php?id=178124&p=1)