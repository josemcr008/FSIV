


# SESION 1

## Colors descritors
Para diferenciar una imagen rotada(bandera que sea la misma rotada), dividimos la imagen en regiones y se calcula el histograma de cada region. A estos se les llama **local descriptors**.


## Texture descriptors
 * Vector con cosas: media, varianza, entropia...
 * We can use the gradients(another vector). We use the derivatives. For each pixel i have the magnitude and the orientation. We get the histogram(again a vector) in which we can see the grades of the lines.


## Shape descriptors
* Una forma con una fórmula chunga




# Assignment 1
* We are going to use a method based on image difference. Basically is calculate the difference between the frame t and t+1. This method is a bit noisy. To remove the noise we use opening+closing.
* We can use another method. The diffence between the image and the background. To make this more robust, we estimate a gaussian model (mean, standar derivation).


# SESION 2

 * Gradient: describe a direccional change of the instenstiy of an image -> Sobel filter.  We can obtein the **shape** of the differents objects that we have on the image.  `orientation = atan(gy/gx)`

 * Laplacian-of-Gaussian. We obtein the edges of the object

0  1  0
1 -4  1
0  1   0

Another way to compute this is using the difference of gaussian

    LoG = G2 - G1 // G2 and G1 must have differents values of sigma

## Canny edge detectors
* Improve the edge cuality in order to find. We obtain Em(magnitude) and Ed(direction)
* Non-maxima suppresion: reduce the width of the edges to one pixel.
	* Discretize the gradient directions in 4 main directions.
	* Create a new image Eg' whose value are 1,2,3,4 according to the nearest angle.
	* Scan Em(matrix that has the magnitude of the image) and Eg'  to create a new image Em' as follows:
		* Em'(x,y)= 0 if Em(x,y) is smaller than at least one of the neighbours in the direction normal to the gradient
		* Em'(x,y=)= Em(x,y) otherwise.
* Hysteresis: we use 2 threshold. tl < tu.
	* pixel > tu -> edge
	* pixel < tl -> no edge
	* tu < pixel < tl -> edge if the pixel is conected with a valid pixel (checking the gradient direction)

How to select the thresholds? select threshold as percentiles of the grey-level distribution

# Sesion 3

## Optical flow
A pattern of apparent motion of the object. We use to obtain objects that are moving in two images. OF is a vector. Three assumptions:
 * Brightness does not change from frame to frame.
 * Small movements.
 * Neighboring points belong to sme surface and have similar motion.

`I(x(t),t) = I(x(t+dt),t+dt)`

I = intensity
x = spacial position
t = time  
dt = increment of time

two points : (2,10) , (4,12)
The optical flow will be: (2,10) - (4,12) = (2,2) = (u,v)

## Segmentation based on colors