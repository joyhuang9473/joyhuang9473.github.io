---
layout: post
title: 'AIS3 2015 Writeup: crypto2'
date: 2015-07-27 12:00
comments: true
tags: [ais3, ais3-2015]
categories: [post-ctf]
---
## RSA Cracking

Keynote:

- a 768 bit RSA crack when all you have is the file you want to decrypt, and the public key

Reference:

- http://m0x39.blogspot.tw/2012/12/0x00-introduction-this-post-is-going-to.html
- http://blog.orange.tw/2014/10/hack-in-box-2014-ctf-writeup-keygenme.html

Tools:

- rsatool.py: https://github.com/ius/rsatool.git
- Factordb: http://www.factordb.com
- rsacrack.py: 

usage: cat file | python rsacrack.py -d [private key exponent] [public key modulus]

<script src="https://gist.github.com/joyhuang9473/d77f9428d3c507989714.js"></script>

- p = randomly chosen prime
- q = randomly chosen prime
- n = modulus for public and private keys(n=pq) 
- f(n)=(p-1)(q-1) :: f(n) counts the number of positive integers less than or equal to n that are relatively prime to n
- e = exponent (chosen as 1 < e < f(n) && greatest common divisor of (e, f(n)) = 1... so e and f(n) are coprime) this is the public key exponent
- d = e^-1(mod f(n)) or (de) = 1 mod f(n)  --- this is the private key exponent

在 rsa.py 裡已經有 public key 的 n, e ，藉由 [Factordb](http://www.factordb.com "Factordb") 找出 p,q 兩個大質數

使用 rsatool.py 找出 private key 的 n, d

	$ python rsatool.py -p 800644567978575682363895000391634967 -q 83024947846700869393771322159348359271173 -n 66473473500165594946611690873482355823120606837537154371392262259669981906291 -e 65537
	Using (p, q) to initialise RSA instance

	n =
	92f6a717a4ca87fbb4e008b2ba036d8fc5ca22c8bb61060fef170ce6792ec573

	e = 65537 (0x10001)

	d =
	480c35d4888c65e8073f81e424ff42c28879294c3c4954a295bf3880decf0659

	p = 800644567978575682363895000391634967 (0x9a32d32db1c5be9aeac5de0daa5017)

	q =
	f3fd0751a4697130a74c96ce57bad29305

p.s 83024947846700869393771322159348359271173 (0xf3fd0751a4697130a74c96ce57bad29305)

使用 rsacrack.py

	$ cat flag.enc | python rsacrack.py -d 480c35d4888c65e8073f81e424ff42c28879294c3c4954a295bf3880decf0659 92f6a717a4ca87fbb4e008b2ba036d8fc5ca22c8bb61060fef170ce6792ec573 | strings
	AIS3{rsaaaaaaaaA_orz}

p.s

n = 0x92f6a717a4ca87fbb4e008b2ba036d8fc5ca22c8bb61060fef170ce6792ec573
= 66473473500165594946611690873482355823120606837537154371392262259669981906291
