---
layout: post
title: 'Install Caffe and ImageNet model '
date: 2014-12-24 16:40
comments: true
tags: [caffe, deep_learning, imagenet]
---
原本想安裝在 Windows，不過過程實在是太不順利了，最後還是依照網路上的一篇教學文，安裝在 Ubuntu 14.04 上，只差在它是用虛擬機，我是用實機安裝。

教學文如下，
[BVLC/caffe Ubuntu 14.04 VirtualBox VM](https://github.com/BVLC/caffe/wiki/Ubuntu-14.04-VirtualBox-VM)

> This is a guide to setting up Caffe in a 14.04 virtual machine with CUDA 6.5 and the system Python for getting started with examples and PyCaffe.

過程中還蠻順利的，除了

- Modify python/classify.py to add the --print_results option

這一步需要自己稍微修改一下 code ，那麼我就分享在 gist 上囉
[custom classify.py in BVLC/caffe: <path_to_caffe>/python/classify.py](https://gist.github.com/Kai-Yu-Huang/6ae7ac4c496c6c4c18f9)
