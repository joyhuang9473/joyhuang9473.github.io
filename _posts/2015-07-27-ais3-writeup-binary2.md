---
layout: post
title: 'AIS3 2015 Writeup: binary2'
date: 2015-07-27 12:00
comments: true
tags: [ais3, ais3-2015]
categories: [post-ctf]
---
## Shellcode to bin

Keynote:

- shellcode
- xor

Reference:

- http://theloshackers.blogspot.tw/2013/08/convert-hex-shellcode-to-binary-mode.html

Tools:

- ida64
- XOR Calculator online https://xor.pw/
- Hex to ASCII text converter http://www.rapidtables.com/convert/number/hex-to-ascii.htm

將 shellcode 輸出成 bin

	$ echo -ne "{ shellcode }" > sc.bin

再丟到 ida 找到這個片段

![sc_shellcode_to_bin_in_ais3's_binary_question](http://i.imgur.com/0WraX3i.png)

總共有 40 個字元在堆疊中，藉由 [rsi+rdx] 逐一讀取 stack 中的字元並與 0CCh 做 xor，直到 dl 為 37 (25h)，也就是第 37 個字元為止

	# origin

	414141C6B1B9A3B5
	93BEA3AA93A8A0BC
	A1A5BF93BFA593A9
	A8A3AFA0A0A9A4BF
	93A7A3B7FF9F858D

	# after xor
	#[] : ignored

	[    ]0a7d756f79
	5f726f665f646c70
	6d69735f73695f65
	646f636c6c656873
	5f6b6f7b33534941

Little Endian 系統，反向讀取並將 hex 轉為 ascii 就可以看到 flag

![sc_converted_hex_to_ascii_in_ais3's_binary_question](http://i.imgur.com/ohf0t1o.png)
