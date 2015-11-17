---
layout: post
title: 'Standord Machine Learning Class: Week2 Assignment'
date: 2015-10-18 12:00
comments: true
tags: [machine-learning, Coursera, Stanford]
categories: [post-machine-learning]
---

## ex1.m

> implement linear regression and get to see it work on data.

- Plot Data

![ex1_plotting_data.png](http://i.imgur.com/cGSkGLC.png)

- Plot the linear fit

![ex1_plot_linear_regression.png](http://i.imgur.com/II2aa9J.png)

- Visualizing J(theta0, theta1) by surf

![ex1_visualizing_J_theta0_theta1_by_surf.png](http://i.imgur.com/0ZXUHFY.png)

- Visualizing J(theta0, theta1) by contour

![ex1_visualizing_J_theta0_theta1_by_contour.png](http://i.imgur.com/0K8xVUV.png)

## ex1_multi.m

- Plot the convergence graph with different learning rates

![ex1_multi_plot_the_convergence_graph.png](http://i.imgur.com/6KExXgJ.png)

## Troubleshoot:

1 . When you run the submit script, if you are seeing error messages that contain any of these phrases...

> urlread, curl, urlreadwrite, peer certificate, CA certificate, unsupported protocol, JSONparser

> ...here are some issues you can check.

> Are you using Octave 4.0.0? You will need to install [this](https://drive.google.com/file/d/0B6lXyE7fgSlXZjlqQ3FIRExmTDA/view?usp=sharing). Follow the instructions in the readme.txt file. Restart Octave after installing the patch. There is a bug in the printf() function, it will be fixed in Octave 4.0.1. The error "JSONparser:invalidFormat: Outer level structure must be an object or an array" error is caused by this bug. 

- reference: [https://www.coursera.org/learn/machine-learning/discussions/vgCyrQoMEeWv5yIAC00Eog](https://www.coursera.org/learn/machine-learning/discussions/vgCyrQoMEeWv5yIAC00Eog)

2 . What is the idea of mean normalization? Is it necessary?

yumi:

> I think that feature scaling is to change the contours of the cost function from ellipse to circle to speed up the convergence. But *mean normalization will only affect the center of the circle*. So I don't understand why we need to ensure that all the features centered around the same value.

Andy Timmons:

> Yumi is right, it is in fact unneccesary. However, you get style points for having a well balanced equation.

> What is at issue is that you use the same alpha for all equations. So, if you select alpha, you want it to be equally valid for all equations, hence the same range. As Tom Mosher said, centering your problem around zero is just what you do.

> Its like taking a picture and putting the object in the middle of the frame. You can get the picture with the object to the left or right, but its just sloppy.

> Applying the equation x-u/s for each parameter means that you dont have to think about what to do for each parameter, its a general equation that can be applied to all with out trying to think "how do I normalize and scale this column", it helps in making a general program that works for all cases.

- reference: [https://www.coursera.org/learn/machine-learning/module/vW94N/discussions/fDrcz2_uEeWdPxJ-h_8T7w](https://www.coursera.org/learn/machine-learning/module/vW94N/discussions/fDrcz2_uEeWdPxJ-h_8T7w)

3 . Predicted price different when I use gradient descent method and normal equations

Because of error price equation. Hint: Normalizing data

<script src="https://gist.github.com/joyhuang9473/70ff08a77597f684988c.js"></script>
