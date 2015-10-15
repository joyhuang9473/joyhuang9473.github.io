---
layout: post
title: 'Tips for plotting data with Octave tool'
date: 2015-10-14 12:00
comments: true
tags: [machine-learning, Coursera, Stanford]
categories: [post-machine-learning]
---

## plot

<script src="https://gist.github.com/joyhuang9473/354d98be80095a79de28.js"></script>

![myPlot.png](http://i.imgur.com/TxbyfmH.png)

## subplot

<script src="https://gist.github.com/joyhuang9473/a6345811b775990bd00b.js"></script>

![mySubplot.png](http://i.imgur.com/xMocAUb.png)

## imagesc

<script src="https://gist.github.com/joyhuang9473/dce0a2d27258a6ac72ac.js"></script>

![magicImagesc.png](http://i.imgur.com/FIFF5X3.png)
![magicImagescWithColorbar.png](http://i.imgur.com/NbsTEXK.png)
![magicImagescWithColorbarGray.png](http://i.imgur.com/tt7TGvM.png)

## figure

<script src="https://gist.github.com/joyhuang9473/38c5e1958f21dfaaf82d.js"></script>

![magicImagescInFigure1.png](http://i.imgur.com/IZ678Z7.png)
![magicImagescGrayInFigure2.png](http://i.imgur.com/2I138Ys.png)

### Troubleshoot:

> When I print figure on OSX Yosemite, the graph is solid black.

Because

the gnuplot 5 bug:

- http://savannah.gnu.org/bugs/?44458

reference:

- http://stackoverflow.com/questions/28133022/octave-on-osx-yosemite-print-outputs-doc-but-graph-is-solid-black

solution:

- downgrading to gunplot version 4.6.6

<script src="https://gist.github.com/joyhuang9473/464bc3f814fa2d07564c.js"></script>