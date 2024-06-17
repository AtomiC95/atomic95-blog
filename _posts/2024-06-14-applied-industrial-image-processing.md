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
**last updated: 2024-06-17**

Hello! Welcome to this blog where we delve into the workings of industrial cameras and their application in classical image processing techniques. We also explore cutting-edge methods utilizing Convolutional Neural Networks (CNNs). Whether you're looking to build a solid foundation in image processing or expand your knowledge with modern approaches, you've come to the right place. Happy reading!

# Introduction

Applied Industrial Image Processing (AIIP) is the field focused on extracting information from images. The typical workflow involves capturing images under optimal lighting conditions and camera settings. The next step is image segmentation, such as binarization or edge detection, to eliminate 'noise' from the image. This process allows the classifier to make accurate decisions based on the cleaned and segmented image data.

## Image Processing Systems

There are three commonly used types of Industrial Image Processing Systems (IPS).

1. **Computer-based System:** This setup uses an external light source and a camera connected to a computer with installed software that can grab frames from the camera. The advantages include scalable computational power, flexibility in hardware selection, and direct visualization via a graphical user interface (GUI). However, the downsides are the high conceptual effort and increased physical space usage.

2. **Smart Camera:** This system integrates a complete image processing unit, usually including a light source and a lens, within a single casing. Compared to the computer-based system, the smart camera setup requires minimal physical space, making it easy to integrate into most factory environments. But withit comes also some downside frist it is a proprietry software and not all features that somebody might want are included, so there is a dependency and the costs of such a system are usually bigger than the first setup but the needed knowledge is smaller.

![smart-camera](/atomic95-blog/assets/img/smart-camera.png)

4. **Embedded Vision Systems:** Last but not least, there are also embedded vision systems, which are smaller than the other setups and cost less due to their microcontroller-based approach. The only real downside is the high integration effort.

![embedded-vision-system](/atomic95-blog/assets/img/embedded-vision-system.png)
# Lightsources

The spektrum of lightsources is divers as the spreptrum of light itself. In this blog we are going to focus on LED's because they are wiedly used in the domain of AIIP.

*Enviromental light is a disturbance for image capturing*

## Light Emitting Diode

tldr; creating light in different colors through electron-hole-combinations. Band gap of the semiconductor $\to$ wavelength $\to$ colour of light.

$$E_{g}=hf=\frac{hc}{\lambda}$$

$\to$

$$\lambda = \frac{hc}{E_{g}}$$

![band gaps for different elements](/atomic95-blog/assets/img/tableLEDs.png)

For a deeper dive into LED's look [here](https://en.wikipedia.org/wiki/Light-emitting_diode).

## Light Guidance

A right light direction is essential for to get a clear information from the extracted features.

There are many type of Light Guidance:

1. *diffuse  illumination*
		the object is not directly illuminated, it is indirect illuminated with a diffusor. **a diffusor is a component which scatters light (milkglass)**
		**properties:** homogeneous alignment, cracks are illuminated from all side, light intensity is reduced due to diffusor.
		
		![diffusor](/atomic95-blog/assets/img/diffusor.png)
		
1. *direct illumination*
		**properties:** high intensity, location-dependent angle of incidence $\to$ only matt objects.
		
		![direct illumination](/atomic95-blog/assets/img/directillumination.png)

1. *focused illumination*
		**properties:** high intensity due to focused illumination
		
		![focusedIllumination](/atomic95-blog/assets/img/focusedillumination.png)

1. *collimated lighting* 
		The light source is within the focal point of the lens
		**properties:** Images generated that way are rich in contrast. Used in combination with telecentric lenses.
		
		![collimated lighting](/atomic95-blog/assets/img/collimiert.png)
		
1. **structured lighting**
		defined patterns are projected on the target.