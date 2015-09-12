---
layout: post
title: 'AIS3 2015 Writeup: binary3'
date: 2015-07-27 12:00
comments: true
tags: [ais3, ais3-2015]
categories: [post-ctf]
---
## 64bit assembly code

Keynote:

- little endian
- xor

Tools:

- ida64
- XOR Calculator online https://xor.pw/
- Hex to ASCII text converter http://www.rapidtables.com/convert/number/hex-to-ascii.htm

主要觀察 check1, check2, gg function

check1:

![stupid_v2_check1_func_in_ais3's_binary_question](http://i.imgur.com/MxSrGW4.png)

check2:

![stupid_v2_check2_func_in_ais3's_binary_question](http://i.imgur.com/kTJEAKj.png)

gg:

![stupid_v2_gg_func_in_ais3's_binary_question](http://i.imgur.com/8crNjMj.png)

在 check1 時，to_reg function 會將 input 存入 rdx，key 的值為 0DDDDAAAADADADDAAh，經過運算：

	key = (input) XOR 0DDDDAAAADADADDAAh

進入 check2 ，call gg function 並且 ax = 0 時即可進到正確的段落 "Yeah, It's a flag !!! ..."

進入 gg function，分兩次檢查 key 的值，總之 key 的值要為 0BFB7B8CEh 和 0BCB4DEC4h 的連接

	key = (input) XOR 0DDDDAAAADADADDAAh
	    = 0BCB4DEC4BFB7B8CEh

所以可得 input 值為 06169746e656d6564h 並拿去轉成 ascii，注意 little endian，反向讀取:

	dementia

得到一個癡呆 :)

flag: AIS3{dementia}


