---
layout: post
title: 'AIS3 2015 Writeup: misc2'
date: 2015-07-27 12:00
comments: true
tags: [ais3, ais3-2015]
categories: [post-ctf]
---
## Known-plaintext attack

Keynote:

- cracking ZIP Files
- you need to have one of the original files contained in the encrypted archive

Reference:

- https://www.hackthis.co.uk/articles/known-plaintext-attack-cracking-zip-files

Tools:

- pkcrack

一開始先確認 facebook.zip 為 zip 檔

{% raw %}
	$ file facebook.zip

	facebook.zip: Zip archive data, at least v1.0 to extract
{% endraw %}

打開後發現有加密，試著看壓縮檔裡面有什麼檔案

{% raw %}
	$ unzip -l facebook.zip

	Archive:  facebook.zip
	  Length     Date   Time    Name
	 --------    ----   ----    ----
	       38  07-15-15 18:15   key.txt
	        0  07-15-15 18:13   p960x960/
	    26664  10-30-13 08:19   p960x960/851556_443281069111871_602278786_n.png
	 --------                   -------
	    26702                   3 files
{% endraw %}

藉由網路上的教學

> you need to have one of the original files contained in the encrypted archive
> What you are going to do with it is you are going to compress it using the same compression method as the protected file. Remember this, otherwise it won't work. So after you do that, move both your zip files, the encrypted one and the plaintext zip

去 google 找 851556_443281069111871_602278786_n.png

![851556_443281069111871_602278786_n.png](https://fbcdn-dragon-a.akamaihd.net/hphotos-ak-prn1/p960x960/851556_443281069111871_602278786_n.png)

壓縮該檔案（包含完整路徑）

{% raw %}
	$ zip -r plaintext.zip p960x960/851556_443281069111871_602278786_n.png
	$ file plaintext.zip

	Archive:  plaintext.zip
	  Length     Date   Time    Name
	 --------    ----   ----    ----
	    26664  07-25-15 00:09   p960x960/851556_443281069111871_602278786_n.png
	 --------                   -------
	    26664                   1 file
{% endraw %}

執行 pccrack

{% raw %}
pkcrack -C facebook.zip -c "p960x960/851556_443281069111871_602278786_n.png" -P plaintext.zip -p "p960x960/851556_443281069111871_602278786_n.png" -d decrypted.zip -a
{% endraw %}

解壓縮 decrypted.zip，裡面的 key.txt 就放著 flag