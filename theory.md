# Computer Vision Notes

This is a compilation of concise information on techniques used in computer vision.

The goal of these notes is to give readers enough information to describe different techniques used in computer vision, and how they work as well as giving OpenCV code snippets that can be used to implement the techniques.

---

## Images

### Image Basics

An image is a continuous function of two coordinates (i,j) in the image plane.  

To process an image on a digital computer, it must be:
* Sampled into a matrix of M rows & N columns.
* Quantised so that each element of the matrix is given an integer value.

Digital image sensors consist of a 2D array of photosensitive elements.

**Luminance** is the intensity of light emitted from a surface per unit area in a given direction.

**Chrominance** is the colorimetric difference between the given colour in a television picture and a standard colour of equal luminance.

Sampling in images sensors means that pixels represent the average luminance or chrominance value over a discrete area which could have multiple light sources in the real world.

Higher resolution images take more computing power to process.

Each pixel in a digital image is a function of scene brightness. The brightness values of a scene are continuous, but the values need to be sampled to become discrete.

### Colour images

A **Multispectral** image (also referred to as a Colour image) is one that captures image data within specific wavelength ranges across the electromagnetic spectrum.

A colour image represents both luminance and chrominance (colour information) within a scene.

Colour images have multiple channels, whereas grayscale images have only one channel.

A **Grayscale** image represents the luminance (Y) at every point in a scene.

Colour images with the same sampling and quantisation as grayscale images are bigger, as they have multiple channels.

Humans are sensitive to light at wavelengths between 400nm and 700nm.

The wavelengths for Red, Green and Blue are 700nm, 546.1nm and 435.8nm respectively.

**RGB** (Red-Green-Blue) images have three channels corresponding to the red, green and blue wavelengths.

There are colours that can not be represented by an RGB image with 256 values in each channel.

RGB images can be converted to grayscale using a formula such as:  
`Y = 0.299R + 0.587G + 0.114B`.

Because the photosensitive elements for each component (red, green & blue) can not be at the exact same position in space in an image sensor, the values for each component for a pixel is made up from the elements somewhat near its position.

**CMY** (Cyan-Magenta-Yellow) is a subtractive colour scheme where the values C, M & Y are subtracted from pure white in order to get the required colour.

The CMY colour scheme is used in printing because RGB starts from Black, whereas CMY starts from white and paper is ordinarily white.

To convert from an RGB image to a CMY image, simply use the formula:  
`C=255-R, M=255-G, Y=255-B`.

The *YUV* colour model is used for analogue TV signals and is comprised of luminance, blue minus luminance and red minus luminance.

The formula to change an RGB image into a YUV image is:  
```
Y = 0.299R + 0.587G + 0.114B
U = 0.429*(B-Y)
V = 0.877*(R-Y)
```

**Hue** is defined technically as "the degree to which a stimulus can be described as similar to or different from stimuli that are described as red, green, blue, and yellow".

**Hue** describes colour of an image and ranges from 0 to 360 degrees.

In theory, luminance typically ranges from 0 to 1 (usually represented digitally as 0-255).

**Saturation** is the degree of strength or purity of a colour and in theory ranges from 0 to 1.

The **HLS** (Hue-Luminance-Saturation) model is frequently used in computer vision.

This is the formula to convert an RGB image into a HLS image:
<img src="/Users/GeoffreyNatin/Documents/GithubRepositories/vision/assets/images/rgbtohsl.png" />

### Image Noise

**Noise** is anything that degrades an image from being ideal.

The two most common types of noise in images are **Gaussian Noise** and **Salt & Pepper Noise**.

**Impulse Noise** is corruption of individual pixels where their brightness differs significantly from the pixels nearby.

Salt and Pepper noise is a type of Impulse Noise.

**Additive Noise** models, `actual_img(i,j) = ideal_img(i,j)+noise_img(i,j)`, are appropriate for images with data-independent noise.

**Multiplicative Noise** models, `actual_img(i,j) = ideal_img(i,j) + ideal_img(i,j)*noise_img(i,j)`, are appropriate for images with data-dependant noise.

Different noise reducing techniques are appropriate in different circumstances, due to assumptions in the techniques or the nature of the image data.

**Image Averaging** can be done to reduce image noise if there are multiple images of the same scene.

**Local Averaging** involves giving each pixel a value which is computed by averaging the nearby pixel values.

**Gaussian Smoothing** is a form of local averaging where the average is computed using weights, with nearby pixels having more of an effect on the average.

Local averaging introduces blurring into images.

A **Rotating Mask** is a nonlinear operator that applies one of nine possible local averaging  filters (such as those below, for example) depending on which image region is most homogeneous.
<img src="/Users/GeoffreyNatin/Documents/GithubRepositories/vision/assets/images/rotating-mask.png" />

Averaging with a rotating mask is effective at suppressing noise and sharpening the images, but is computationally more expensive than local averaging.

**Median Filtering** involves setting pixel values to the median of the values of nearby pixels.

---

## Image Histograms

An **Image Histogram** is an abstraction of an image where the frequency of each image (bright- ness/intensity) value is determined.

Image histograms contain global information about the image and that is completely independent of the position and orientation of objects in the scene.

Images with identical histograms can be very different.

In image histograms, **Bins** are ranges of values within the histogram.

**Histogram Smoothing** involves taking an image histogram and replacing each value with the average of the nearby values.

The choice of colour model for image histograms can have a huge effect on the usefulness of the colour histogram.

It is easier for humans to distinguish large differences in images, so if the distribution of grey-scales in an image is improved, this can lead to a better understanding of the image for humans.

**Histogram Equalisation** involves improving the distribution of grey-scales in an image by creating a more even spread of the luminance values in the image using the image's luminance histogram.

**Histogram Comparisons** can be used to measure similarities of images.

**Back Projection** is a way to select particular colours from an image. Back projection involves taking a representative sample set of the colours to be selected, creating a histogram of the samples and normalising the histogram so that the maximum value is 1. Then the values in the histogram can be treated as probabilities that correspond to the likelihood that a given value is of the particular colour.

The number of histogram bins and the colour space used can have a big impact on the effectiveness of back projection.

**K-Means Clustering** involves selecting a number of colours that best represent all the colours in an image.

In K-Means Clustering, k *exemplars* (colours) that best represent the colours in the image are searched for. The colour of each pixel in the image is referred to as a *pattern*, and groups of patterns associated with a particular exemplar are called a *cluster*.

K-Means Clustering works as follows:
1. Random exemplars are chosen randomly.
2. For each pattern, allocate it to the nearest exemplars
3. Re-compute the exemplar as the centre of gravity of the patterns associated with it
4. Repeat steps 2-3 until the exemplars converge
5. Re-allocate all the patterns to their nearest exemplar

K-Means Clustering is an example of unsupervised learning.

---
