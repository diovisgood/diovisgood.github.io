---
date: 2019-05-10
title: "Agender Project"
excerpt: "This is a small demo project to try and test OpenCV library, implement on-the-fly face detection, age and gender estimation using pre-trained models."
categories: machine-learning
tags: detection haar face tensorflow opencv python
sidebar:
  - title: "Period"
    text: "Apr 2019 - May 2019"
  - title: "Technologies"
    text: "**Tensorflow**, **OpenCV**, **Python**"
---

![](/assets/img/agender_output1.gif)

This is a small demo project to try and test **OpenCV** library
and also implement on-the-fly **face detection, age and gender estimation
using pre-trained models**.

In this work I studied 12 existing projects for age and gender estimation.
I have discovered that there are a lot of good models with high accuracy,
that are yet **too big and slow** to compute.

On the other hand there are some small models with lower accuracy,
that could be used for **real-time** video processing.

I have successfully used two such models for real-time estimation of age and gender using only average CPU:
- **SSR-Net** by Tsun-Yi Yang, Yi-Hsuan Huang, Yen-Yu Lin, Pi-Cheng Hsiu, Yung-Yu Chuang.
- **ConvNet** by Gil Levi and Tal Hassner.

I achieved some decent results.

[Read the Full Story]({% post_url 2019-05-10-age-gender-estimation %}){: .btn .btn--info}

[View Project on Github](https://github.com/diovisgood/agender/){: .btn .btn--primary target="_blank"}
