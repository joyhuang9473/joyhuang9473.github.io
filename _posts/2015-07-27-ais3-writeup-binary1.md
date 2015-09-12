---
layout: post
title: 'AIS3 2015 Writeup: binary1'
date: 2015-07-27 12:00
comments: true
tags: [ais3, ais3-2015]
categories: [post-ctf]
---
## Strings

Keynote:

- 動態分析

Tools:

- ollyDbg201h

把 bin1.exe 丟到 ollydbg ，搜尋 string 'AIS3' 就可以找到 flag

![bin1_exe_strings_in_ais3's_binary_question](http://i.imgur.com/nnfBQ1S.png)

有稍微的漏字，但就依照 flag 上的語義自己填補了

p.s

ollyDbg110 的 strings 比 ollyDbg201h 較不完整

ollyDbg201h 的 strings 仍然會漏字，仍不清楚原因