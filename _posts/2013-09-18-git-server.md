---
layout: post
title: 'Git-server'
date: 2013-09-18 09:27
comments: true
tags: [Git]
---
[https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md](https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md)

	sudo pacman -S python-docutils

	mail server: postfix

	sudo pacman -S postfix

2. Ruby

	cd ~
	mkdir ruby && cd ruby
	curl --progress ftp://ftp.ruby-lang.org/pub/ruby/2.0/ruby-2.0.0-p247.tar.gz | tar xz
	cd ruby-2.0.0-p247
	./configure


[error]

Make GitLab start on boot:

	sudo update-rc.d gitlab defaults 21