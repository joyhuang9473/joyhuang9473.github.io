---
layout: post
title: 'AIS3 2015 Writeup: crypto1'
date: 2015-07-27 12:00
comments: true
tags: [ais3, ais3-2015]
categories: [post-ctf]
---
## Reference:

Keynote:

- filename

Reference:

- https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher

Tools:

- Vigenere Cipher Decoder http://www.dcode.fr/vigenere-cipher
- Vigenère Cipher Codebreaker http://www.mygeocachingprofile.com/codebreaker.vigenerecipher.aspx

藉由第一個連結找出可能的 key length，再由第二個連結，設定 key size 後找出所有的可能，並搜尋 "the key is" 找出可辨識的字串

![vigenere_key_length_in_ais3's_crypto_question](http://i.imgur.com/IdI4AD1.png)

![vigenere_decode_in_ais3's_crypto_question](http://i.imgur.com/xhFbfMR.png)