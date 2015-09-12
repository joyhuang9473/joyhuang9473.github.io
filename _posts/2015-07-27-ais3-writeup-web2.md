---
layout: post
title: 'AIS3 2015 Writeup: web2'
date: 2015-07-27 12:00
comments: true
tags: [ais3, ais3-2015]
categories: [post-ctf]
---
## JSFuck

Keynote:

- 可以只用 6 個字符 \[\]()!+ 來編寫 JavaScript 程序

Reference:

- http://www.jingwentian.com/t-413
- http://codegolf.stackexchange.com/questions/28714/convert-jsfuck-to-normal-js

剛開始看到 code 時覺得是 javascript，試著把它跑起來

{% raw %}
	<!-- test.html -->
	<html>
	<head></had>
	<body>
	<script>
	{ web2.txt }
	</script>
	</body>
	</html>
{% endraw %}

結果出現了一個 ^_^ ，確定是一個可執行的 javascript

{% raw %}
	^_^
{% endraw %}

網路上得知 JSFuck，藉由他人所寫的 script ，把 jsfuck 轉換為一般 javaScript

{% raw %}
	<!- jsfuck-decoder.html ->
	<html>
	<head></had>
	<body>
	<script>
	alert(/\n(.+)/.exec(eval(prompt().slice(0,-2)))[1]);
	</script>
	</body>
	</html>
{% endraw %}

輸出結果

![jsfuck_in-ais3's_web_question](http://i.imgur.com/uGgznIH.png)