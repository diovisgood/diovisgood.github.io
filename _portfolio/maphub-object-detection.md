---
title: "Object detection for MapHub"
date: 2021-11-04
excerpt: "Object detection model to detect buildings, coconut palms, etc. in GeoTIFF files"
categories: machine-learning
tags: pytorch detection yolo opencv docker python geotiff
sidebar:
  - title: "Period"
    text: "Sep 2021 - Oct 2021"
  - title: "Technologies"
    text: "**PyTorch**, **YOLOv5**, **OpenCV**, **Docker**, **Python**, **GeoTIFF**"
  - title: "Role"
    text: "Machine Learning Engineer"
  - title: "Responsibilities"
    text: "Creating object detection model"
---

Sometimes developer companies, farmers, or city mayors want to have a bird's view photos of their land.
On the other side, there are people who can launch their flying drones to collect aerial imagery
to produce GeoTIFF.

One [team](https://maphub.online){:target="_blank"} wants to make a service, so these two can easily find each other and close deals.
They asked me to create an object detection model to detect buildings, coconut palms, etc. in GeoTIFF files. 

I wrote utility to grab image patches from GeoTIFF files and constructed the training dataset. 
Then I used a [YOLOv5](https://github.com/ultralytics/yolov5/){:target="_blank"} project to train the model,
as its [license](https://github.com/ultralytics/yolov5/blob/master/LICENSE){:target="_blank"}
allows commercial usage.
I wrote my own code which runs model on multiple patches of source image
and implements non-maximum suppression algorithm to produce the final predictions list.
After that I created script to build a lightweight docker image ready for deployment.

## Challenges

First challenge was that GeoTIFF files are typically very huge.
For example: `40,000 x 50,000` pixels, `RGBA`, with file sizes 1...3 Gb.

Typically, the [GDAL](https://gdal.org/){:target="_blank"} library is used to work with GeoTIFF,
but it is too huge, and I've met some memory issues when tried to use it.
I found a lightweight [library](https://github.com/KipCrossing/geotiff/){:target="_blank"},
which is capable of loading some patches from large GeoTIFF files.

Second challenge was that inference code from `YOLOv5` is not capable
of processing large GeoTIFF files part by part.

That is why I created my own code which runs model on multiple patches of source image
and implements
[non-maximum suppression algorithm](https://learnopencv.com/non-maximum-suppression-theory-and-implementation-in-pytorch/){:target="_blank"}
to produce the final predictions list.

Third challenge was to build a docker image of some reasonable size.
As, docker images with PyTorch library can grow up to 2.5...3 Gb!

I exported model into [ONNX](https://onnxruntime.ai/){:target="_blank"} format,
and constructed a lightweight docker image of only 300 Mb.
