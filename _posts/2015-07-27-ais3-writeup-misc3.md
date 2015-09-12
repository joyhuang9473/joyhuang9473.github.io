---
layout: post
title: 'AIS3 2015 Writeup: misc3'
date: 2015-07-27 12:00
comments: true
tags: [ais3, ais3-2015]
categories: [post-ctf]
---
## File extension

Keynote:

- gzip, tar, bmp

Tools:

- stegsolve.jar: A steganographic image analyzer, solver and data extractor for challanges.

查看 c4 檔案類型

	$ file c4

	c4: gzip compressed data, from Unix

重新命名 c4 為 c4.gz

	$ gzip -d c4

	gzip: c4: unknown suffix -- ignored

	$ mv c4 c4.gz
	$ gzip -d c4.gz

解壓出一個 tar archive 的 c4，且 c4 裡面又包了 c4 ，為避免 overwrite ，改名再解壓

	$ tar -zxvf c4

	x c4: Refusing to overwrite archive
	tar: Error exit delayed from previous errors.

	$ tar -tvf c4
	-rw-rw-r--  0 orange orange 345654 Jul 21 18:02 c4

	$ mv c4 c4.tar
	$ tar -zxvf c4.tar

	x c4

	$ file c4

	c4: PC bitmap, Windows 3.x format, 480 x 240 x 24

此時 c4 為 bmp 圖片檔，隱約可以看到有字位於左下角

![c4_bmp_in_ais3's_misc_question](http://imgur.com/LDlMjBq.png)

利用 stegsolve.jar 去處理圖片，在 Red plane 2 模式時就可以清楚看到字了

![c4_solved_bmp_in_ais3's_misc_question](http://imgur.com/ALDem6N.png)