---
layout: post
title: '遠端 Ubuntu 14.04 桌面'
date: 2014-12-27 03:18
comments: true
tags: [ubuntu, xrdp, Xfce4]
---
最近因為期末專題的關係，選用了 Ubuntu 14.04 作為系統環境，而由於在下做的是跟影像辨識有關的題目，考量之後要秀出影像結果等需要，就來處理一下遠端桌面的功能，好讓我能帶著 MBP 去 demo :)

原本想說 ubuntu 這麼多人用，應該只要稍微設定一下就能用遠端桌面了吧，沒想到弄起來還是挺麻煩的 ==

首先還是先介紹可以正常運作的教學：

[Ubuntu 14.04 – How to install xrdp in Ubuntu 14.04](http://c-nergy.be/blog/?p=5305)

其實主要精神就是 **安裝 xrdp ，改用 Xfce4** 作為桌面環境（desktop environment）

另外還有可能碰到的問題是，每當關閉遠端連線後，下次再遠端桌面登入卻是不同的 session ，就是重新遠端後看到的卻不是上一次遠端的桌面，那解決方法就是：

[How do I set up xrdp session that reuses an existing session?](http://askubuntu.com/questions/133343/how-do-i-set-up-xrdp-session-that-reuses-an-existing-session)

Note:

> that only works if there's already an existing session though. The first time in, there's no session so it fails to connect to port 5912.

似乎還不是一個很好的辦法，之後再找找囉。

-- clear --

修改 /etc/xrdp/xrdp.ini

    [xrdp1]
    name=sesman-vnc
    lib=libvnc.so
    username=ask
    password=ask
    ip=127.0.0.1
    port=5910 #原本的值為 -1

至於為甚麼不能用 ubuntu 本身的 Unity 作為桌面環境，雖然還不確定原因，但感覺是 Unity, Gnome 對 xrdp 的支援程度有關，總之試過 gnome-session 的寫法，遠端後的結果都不樂觀，都會是 **灰底畫面，還可以顯示的 'X' 游標**

（以下寫法都不能正常運作遠端桌面功能）

~/.xsession file :

    # Uncomment one of list items below, if you really want to try and test

    #gnome-session --session=gnome-classic
    #gnome-session --session=gnome-fallback
    #gnome-session –-session=ubuntu-2d
