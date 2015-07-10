---
layout: post
title: 'Install docker on Arch Linux'
date: 2014-06-28 05:20
comments: true
tags: 
---
Install docker in Arch
1. Search image or Create a Base Image

Note: Base Image https://docs.docker.com/terms/image/#base-image-def

#Search image

: sudo docker search <image_name>

ex.

	sudo docker search arch

	sudo docker pull base/arch

	sudo docker run base/arch echo "Hello World!"

Tip:
The command docker run takes a minimum of two arguments:
1) an image name, and
2) the command you want to execute within that image.

登入 image

	sudo docker run -i -t base/arch /bin/bash

登出 image

	# exit

Note:
Unlike VMs, containers don’t need to boot up or shut down the whole OS. Unless you’re running a process in it, your container isn’t taking up any resources apart from some disk space. Once our bash process has finished, your container is closed.

Commit

	sudo docker commit 85eed1376ab3 centos:LAMP

#Create a Base Image

[http://docs.docker.com/reference/commandline/cli/](http://docs.docker.com/reference/commandline/cli/)

[http://blog.blackwhite.tw/2013/12/docker.html](http://blog.blackwhite.tw/2013/12/docker.html)

[http://www.slideshare.net/ya790026/docker-33456641](http://www.slideshare.net/ya790026/docker-33456641)