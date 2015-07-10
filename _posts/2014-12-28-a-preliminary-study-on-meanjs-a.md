---
layout: post
title: '初探 MEAN stack (一)'
date: 2014-12-28 14:05
comments: true
tags: [MEAN, Full stack]
---
最近看到 [Bossable.com: 30 day MEAN STACK Honolulu CHALLENGE](https://www.youtube.com/playlist?list=PL6rhBJX0L3TWYrwrQIi1_MzQDvVhkUVPI) 教學視頻，想說就來了解一下什麼是 MEAN stack 吧，將來也會配合這視頻，記錄一下學習的歷程，希望能真的在 30 天以內學好 MEAN.js :)

首先先推這篇文章，寫得簡單易懂！

[擁抱Javascript全端開發 - MEAN stack 工程師，你跟上了沒~](http://adon988.logdown.com/posts/247366-mean-stack-engineers-clean-title)

**MEAN**

    - MongoDB
    - Express
    - AngularJS
    - Node.js

**Full stack**

> 對於Javascript前後端通吃的特性，可以稱做 "Javascript全端能力(full stack JavaScript)"或者"純Javascript解決方案(pure JavaScript solutions)"
> Full stack工程師

MEAN.JS: http://meanjs.org/docs.html
bossable.com: http://www.bossable.com/

-- clear --

**Getting started with the MEAN stack**

## Prerequisites

- nodejs 
- mongoDB
- bower
- grunt

(nodejs的安裝不敘述了，而 mongoDB 的部分採用線上免費的 [mongolab](https://mongolab.com) ，大概有 500MB 空間可用)


	$ npm install -g bower

    $ npm install -g grunt-cli

## Install the MEAN.JS generator

另外還安裝了 Yo Generator ，將來會用它來取得最新的 MEAN.JS

> The recommended way would be to use the official Yo Generator which will generate the latest stable copy of the MEAN.JS boilerplate and supply multiple sub-generators to ease your daily development cycles. 

    $ npm install -g yo

    $ npm install -g generator-meanjs

## Create your MEAN App

    cd /path/to/project
    yo meanjs

## set up database

這裡我改用 mongolab ，以下文中有簡單的使用教學：

[MongoDB Tutorial（1）雲端時代的 MongoDB 環境建置](http://www.codedata.com.tw/database/mongodb-tutorial-1-setting-up-cloud-env/)

    # edit /path/to/project/config/env/development.js
    'use strict';

    module.exports = {
        db: 'mongodb://<dbuser>:<dbpassword>@something.mongolab.com:49130/mydatabase',
        app: {
                title: 'blog - Development Environment'
        },

# start

    $ grunt

這樣就可以看到簡單的範例網頁了