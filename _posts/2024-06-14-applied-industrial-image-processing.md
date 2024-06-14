---
layout: post
title: Applied industrial image processing
author: Nikolas Rieder
categories: journal
tags:
  - documentation
  - image
  - industrial
image: aibv_title.png
last updated: 2024-06-14
---
Hello! Welcome to this blog where we delve into the workings of industrial cameras and their application in classical image processing techniques. We also explore cutting-edge methods utilizing Convolutional Neural Networks (CNNs). Whether you're looking to build a solid foundation in image processing or expand your knowledge with modern approaches, you've come to the right place. Happy reading!

# Introduction

Applied Industrial Image Processing (AIIP) is the field focused on extracting information from images. The typical workflow involves capturing images under optimal lighting conditions and camera settings. The next step is image segmentation, such as binarization or edge detection, to eliminate 'noise' from the image. This process allows the classifier to make accurate decisions based on the cleaned and segmented image data.

## image processing systems

There are three commonly used types of Industrial Image Processing Systems (IPS).

1. **Computer-based System:** This setup uses an external light source and a camera connected to a computer with installed software that can grab frames from the camera. The advantages include scalable computational power, flexibility in hardware selection, and direct visualization via a graphical user interface (GUI). However, the downsides are the high conceptual effort and increased physical space usage.

2. **Smart Camera:** This system integrates a complete image processing unit, usually including a light source and an objective lens, within a single casing. Compared to the computer-based system, the smart camera setup requires minimal physical space, making it easy to integrate into most factory environments. But withit comes also some downside frist it is a proprietry software and not all features that somebody might want are included, so there is a dependency and the costs of such a system are usually bigger than the first setup but the needed knowledge is smaller.
![smart-camera](/atomic95-blog/assets/img/smart-camera.png)
4. **Embedded Vision Systems:** Last but not least, there are also embedded vision systems, which are smaller than the other setups and cost less due to their microcontroller-based approach. The only real downside is the high integration effort.
![embedded-vision-system](/atomic95-blog/assets/img/embedded-vision-system)