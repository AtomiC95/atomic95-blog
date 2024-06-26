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
**last updated: 2024-06-26**

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

1. *diffuse  illumination*<br>
		the object is not directly illuminated, it is indirect illuminated with a diffusor. **a diffusor is a component which scatters light (milkglass)**<br>
		**properties:** homogeneous alignment, cracks are illuminated from all side, light intensity is reduced due to diffusor.
		
	![diffusor](/atomic95-blog/assets/img/diffusor.png)
		
1. *direct illumination*<br>
		**properties:** high intensity, location-dependent angle of incidence $\to$ only matt objects.
		
	![direct illumination](/atomic95-blog/assets/img/directillumination.png)

1. *focused illumination*<br>
		**properties:** high intensity due to focused illumination
		
	![focusedIllumination](/atomic95-blog/assets/img/focusedillumination.png)

1. *collimated lighting*<br>
		The light source is within the focal point of the lens.<br>
		**properties:** Images generated that way are rich in contrast. Used in combination with telecentric lenses.
		
	![collimated lighting](/atomic95-blog/assets/img/collimiert.png)
		
## Surface Structure

To decide which kind of illumination is best suited for your specific use case, you need to know the surface structure of your target.

a rough classification is: <br>
	- matt flat surface<br>
		**properties:** scattering surface - illumination is non-critical<br> 
	- glossy flat surface<br>
		**properties:** target acts as mirror $\to$ light source is visible in image - light has to be scattered with a diffusor<br>
	- matt uneven surface<br>
		**properties:** depending on the angle of incidence shadow cast possible.<br>
	- glossy uneven surface<br>
		 **properties:** light has to be diffused -> spezial illumination hardware like a dome lighting.<br>
## light solutions

### coaxial lighting
Coaxial lighting creates homogeneous illumination on a target object. <br>
![coaxial lighting](/atomic95-blog/assets/img/coaxial-lighting.png)
### coaxial lighting (collimated)
only plain horizontal areas appear bright.<br>
![coacial-lighting-collimated](/atomic95-blog/assets/img/coaxial-lighting-collimated.png)
### dome lighting
Constructive avoidance of inhomogeneous illumination.<br>
![dome lighting](/atomic95-blog/assets/img/dome-lighting.png)
### bright field illumination
Horizontal areas appear bright and scratches appear dark. <br>
![bright field illumination](/atomic95-blog/assets/img/bright-field.png)
### dark field illumination 
Only scattering features appear bright $\to$ Usefull for finding scratches. <br>
![dark field illumination](atomic95-blog/assets/img/dark field.png)
# Lens and Camera

In this chapter we want to answer the following questions: <br>
- What is a central projection?
- Why is a lens optic more widely used than a pinhole camera?
- How is the illistration law derived and where it is applied?
- How an aperture influences the depth of field?
- what the depth of field is, name its influencing parameters and calculate the depth of field
- for what a telecentric lens is used.
## pinhole camera

With a pinhole camera it is possible to capture light trough a hole and to project on a 2 dimensional area. Because of the properties of light knowing the relative position of the target object in regards of the pinhole it is possible to determine properties of the projected object on the 2D area. <br>
This is called central projection. It says that the distance from the object to the pinhole on the x-axis $x_{c}$ divided by the distance $z_{c}$ on the z-axis is equals the relation $\frac{x}{z}$ whereby x stands for the distance between projection and pinhole on the x-axis and z for the distance on the z-axis. Also because the origin of the coordinates lies on the pinhole we need to use a negative sign for the projection side. <br>

$$\frac{x_{c}}{z_{c}}=-\frac{x}{z}$$
<br>
The same applies for the y-axis. <br>

$$\frac{y_{c}}{z_{c}}=-\frac{y}{z}$$
<br>
=><br>
With size ratio $V=-\frac{b}{g}$<br>
![pinhole-schematic](/atomic95-blog/assets/img/pinhole.png)<br>
## lenses

lenses are a special components that are used for a targeted refraction of light. All parallel incoming beams meet a the focal point. <br>
![lens-schematic](/atomic95-blog/assets/img/lens-schematic.png)
Lenses are always preferred against pinhole cameras because, a pinhole camera delivers only a sharp image when it has a very small pinhole. The downside of having a very small pinhole is that less light is used for the image, therefore it is very dark. <br>
When dealing with thin lenses, usually a lens is called thin when the thickness of the lens is much smaller than the focal point, then it is possible to use the illustration law. <br>
$$\frac{1}{f}=\frac{1}{g}+\frac{1}{b}$$
![illustration law](/atomic95-blog/assets/img/illustrationlaw.png)<br>
**statements from the illustration law** <br>
*cause of depth of field* <br>
Target is sharp when it has the distance g.<br>
$$g=\frac{b*f}{b-f}$$<br>
*focus*<br>
Object can only be sharp when the distance from the sensor and the main plain of the lens have a distance of b. <br>
$$b=\frac{f*g}{g-f}=\frac{f}{1-\frac{f}{g}}$$<br>
special case: <br>
g $\to$ $\infty$ : b $\cong$ f<br>
g $\to$ f : b $\to$ $\infty$ <br>
*object selection*<br>
It is possible to determine the focal point of the lens through the target distance g and the distance between sensor and main plain of the lens.<br>
$$f=\frac{g*b}{g+b}$$<br>
*Enlargement*<br>
$V=\frac{b}{g}=\frac{f}{g-f}$<br>
with g >> f <br>
$V=\frac{f}{g}$<br>
$\to$ enlargment is proportional to focal point<br>
## depth of field (DOF)

only objects with a distance $g=\frac{b*f}{b-f}$ can be displayed sharp. But this distance can have a small tolerance called $\epsilon$ . The reason for that is that the light still hits the pixel which has some kind of dimensions.<br>
![dof](/atomic95-blog/assets/img/dof.png)<br>
*Tolerable deviation from the focal plane on the far and near sides:*<br>
$$\triangle g=\frac{\epsilon *g}{\frac{d*f}{g-f}\pm \epsilon}$$<br>
Usually applies $\epsilon$ << $\frac{d*f}{g-f}$ $\to$ $k*\frac{g(g-f)}{f²}*\epsilon$<br>
with $k=\frac{f}{D}$<br>
D is the aperture value. The values are potencies of $\sqrt{2}$. That means when increasing the aperture value, the area doubles.<br>
![aperture-value](/atomic95-blog/assets/img/apetrue-values.png)<br>
## telecentric lens

One of the limitation of normal lens is that the enlargement is dependent of the distance of the target. This can be overcome with *telecentric lens*. <br>
![telecentric-lens](/atomic95-blog/assets/img/telecentric-lens.png)<br>
### Camera

#### consumer camera's<br>
	- focus is on resolution
	- integrated image compression (JPEG)
	- read image slow
#### IP-cameras for monitoring<br>
	- compression of images for a lower bandwith
	- images capturing only when movement is detected
#### indutrial camera<br>
	- focus is on unadulterated image reproduction
	- no data compression
	- high frame rate

### Sensor technology

There are two dominant sensor technologies: *Charged Coupled Device* (CCD) classic technology for high-end cameras. Displaced by CMOS. 

#### disadvantages compared to CCD
- low Fill factor (Proportion of the light-sensitive area in the total area)
#### advantages compared to CCD
- higher frame rate
- region of interest and reduce noise due to average with more pixels (binning)
- no to low blooming effect
- low energy consumption
- preprosessing on the chip
#### Rolling Shutter
sequential reading of rows $\to$ distortion by very fast movments
newer versions of CMOS-sensor also have *Global Shutter*<br>
### characteristic of camera's

#### physical basis

The foundation of light measurement is the property of light of being a particle flow. <br>
The detection of light on a Sensor is a statistical process. <br>
The expected value $\mu_{p}$ is the number of photons which meet on a surface proportional to $A$ (Area), $t$ (Duration), E (Intensity).<br>
$$\mu_{p}=\frac{E*A*t}{E_{Photon}}=\frac{E*A*t}{h*\frac{c}{\lambda}}$$<br>
This is a poisson-distibution, it applies for the varianz: $\sigma²=\mu_{p}$<br>
$\to$ varianz is a measure for light-noise.<br>
$\to$ *quantum efficiency $\eta$* describes how many photons generate a electron-hole-pair.<br>
### Photon-Transfer-Method

![photon-transfer-method](photon-tranfer-method.png)<br>
$\mu_{p}$ stands for the photons which are detected by the collector. $\sigma²$ describes the varianz. The photons are converted to a electric signal with a so called quantum efficiency $\eta$. A dark noise is added to the electric signal. This electric nois comes from thermal heating within the camera. Those signals are added up and then empowered with the gain $K$. The resulting signal is then quantized, this also adds a quantization noise. The resulting signal is a digital gray value $\mu_{g}$. <br>
- $\mu_{e}=\eta*\mu_{p}$<br>
- $\mu_{g}=K*(\mu_{e}+\mu_{d})$<br>
**SNR (Signal-Noise-Ratio)**

$$SNR=\frac{\eta*\mu}{\sqrt{\sigma²_{d}+\frac{\sigma²_{p}}{K²}+\eta*\mu_{p}}}$$<br>
- SNR is almost not dependent of K<br>
- If illumination intensity is *high* $\to$ $SNR=\sqrt{ \eta*\mu_{p} }$<br>
	- That means that if the light source is good, nearly every camera has the same SNR.<br>
- If illumination intensity is *low* $\to$ $SNR=\frac{\eta*\mu_{p}}{\sqrt{\sigma²_{d}+\frac{\sigma²_{d}}{K²} }}$<br>
	- proportional to illumination intensity
	- proportional to photon number
		- It is important that the pixel area is large enough.
