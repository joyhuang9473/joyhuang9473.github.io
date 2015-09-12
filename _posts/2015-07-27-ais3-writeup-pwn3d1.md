---
layout: post
title: 'AIS3 2015 Writeup: pwn3d1'
date: 2015-07-27 12:00
comments: true
tags: [ais3, ais3-2015]
categories: [post-ctf]
---
## Buffer Overflow Attack

Keynote:

- stack

Tools:

- pwntool

sub_4006AD:

![pwn1_asm_in_ais3's_binary_question](http://i.imgur.com/uPnmKhO.png)

![pwn1_boa_in_ais3's_pwn3d_question](http://i.imgur.com/ed2urWa.png)

stack ??

	-----ret-----
	4
	----var_4----
	16
	----var_20---
	4
	-----rbp-----
	20
	-----rsp-----
