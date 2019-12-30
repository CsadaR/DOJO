---
title: Image Processing in Python
tags: python,image-processing
url: https://www.datacamp.com/courses/image-processing-in-python
---

# 1. Introducing Image Processing and scikit-image
## Is this gray or full of color?
```python
np.shape(coffee_image)
np.shape(coins_image)
```

## RGB to grayscale
```python
# Import the modules from skimage
from skimage import data, color

# Load the rocket image
rocket = data.rocket()

# Convert the image to grayscale
gray_scaled_rocket = color.rgb2grey(rocket)

# Show the original image
show_image(rocket, 'Original RGB image')

# Show the grayscale image
show_image(gray_scaled_rocket, 'Grayscale image')
```

## Flipping out
```python
# Flip the image vertically
seville_vertical_flip = np.flipud(flipped_seville)

# Flip the image horizontally
seville_horizontal_flip = np.fliplr(seville_vertical_flip)

# Show the resulting image
show_image(seville_horizontal_flip, 'Seville')
```

## Histograms
```python
# Obtain the red channel
red_channel = image[:, :, 0]

# Plot the red histogram with bins in a range of 256
plt.hist(red_channel.ravel(), bins=256)

# Set title and show
plt.title('Red Histogram')
plt.show()
```

## Apply global thresholding
```python
# Import the otsu threshold function
from skimage.filters import threshold_otsu

# Make the image grayscale using rgb2gray
chess_pieces_image_gray = rgb2gray(chess_pieces_image)

# Obtain the optimal threshold value with otsu
thresh = threshold_otsu(chess_pieces_image_gray)

# Apply thresholding to the image
binary = chess_pieces_image_gray > thresh

# Show the image
show_image(binary, 'Binary image')
```

## When the background isn't that obvious
```python
# Import the otsu threshold function
from skimage.filters import threshold_otsu

# Obtain the optimal otsu global thresh value
global_thresh = threshold_otsu(page_image)

# Obtain the binary image by applying global thresholding
binary_global = page_image > global_thresh

# Show the binary image obtained
show_image(binary_global, 'Global thresholding')

##
# Import the local threshold function
from skimage.filters import threshold_local

# Set the block size to 35
block_size = 35

# Obtain the optimal local thresholding
local_thresh = threshold_local(page_image, block_size, offset=10)

# Obtain the binary image by applying local thresholding
binary_local = page_image > local_thresh

# Show the binary image
show_image(binary_local, 'Local thresholding')
```

## Trying other methods
```python
# Import the try all function
from skimage.filters import try_all_threshold

# Import the rgb to gray convertor function 
from skimage.color import rgb2gray

# Turn the fruits image to grayscale
grayscale = rgb2gray(fruits_image)

# Use the try all method on the grayscale image
fig, ax = try_all_threshold(grayscale, verbose=False)

# Show the resulting plots
plt.show()
```

## Apply thresholding
```python
# Import threshold and gray convertor functions
from skimage.filters import threshold_otsu
from skimage.color import rgb2gray

# Turn the image grayscale
tools_image = rgb2gray(tools_image)

# Obtain the optimal thresh
thresh = threshold_otsu(tools_image)

# Obtain the binary image by applying thresholding
binary_image = tools_image > thresh

# Show the resulting binary image
show_image(binary_image, 'Binarized image')
```

# 2. Filters, Contrast, Transformation and Morphology
## Edge detection
```python
# Import the color module
from skimage import color

# Import the filters module and sobel function
from skimage.filters import sobel

# Make the image grayscale
soaps_image_gray = color.rgb2gray(soaps_image)

# Apply edge detection filter
edge_sobel = sobel(soaps_image_gray)

# Show original and resulting image to compare
show_image(soaps_image, "Original")
show_image(edge_sobel, "Edges with Sobel")
```

## Blurring to reduce noise
```python
# Import Gaussian filter 
from skimage.filters import gaussian

# Apply filter
gaussian_image = gaussian(building_image, multichannel=True)

# Show original and resulting image to compare
show_image(building_image, "Original")
show_image(gaussian_image, "Reduced sharpness Gaussian")
```

## What's the contrast of this image?
```python
np.max(clock_image) - np.min(clock_image)
```

## Medical images
```python
# Import the required module
from skimage import exposure

# Show original x-ray image and its histogram
show_image(chest_xray_image, 'Original x-ray')

plt.title('Histogram of image')
plt.hist(chest_xray_image.ravel(), bins=256)
plt.show()

# Use histogram equalization to improve the contrast
xray_image_eq =  exposure.equalize_hist(chest_xray_image)

# Show the resulting image
show_image(xray_image_eq, 'Resulting image')
```

## Aerial image
```python
# Import the required module
from skimage import exposure

# Use histogram equalization to improve the contrast
image_eq =  exposure.equalize_hist(image_aerial)

# Show the original and resulting image
show_image(image_aerial, 'Original')
show_image(image_eq, 'Resulting image')
```

## Let's add some impact and contrast
```python
# Import the necessary modules
from skimage import data, exposure

# Load the image
original_image = data.coffee()

# Apply the adaptive equalization on the original image
adapthist_eq_image = exposure.equalize_adapthist(original_image, clip_limit=0.03)

# Compare the original image to the equalized
show_image(original_image)
show_image(adapthist_eq_image, '#ImageProcessingDatacamp')
```

## Transformations
```python
# Import the module and the rotate and rescale functions
from skimage.transform import rotate, rescale

# Rotate the image 90 degrees clockwise 
rotated_cat_image = rotate(image_cat, -90)

# Rescale with anti aliasing
rescaled_with_aa = rescale(rotated_cat_image, 1/4, anti_aliasing=True, multichannel=True)

# Rescale without anti aliasing
rescaled_without_aa = rescale(rotated_cat_image, 1/4, anti_aliasing=False, multichannel=True)

# Show the resulting images
show_image(rescaled_with_aa, "Transformed with anti aliasing")
show_image(rescaled_without_aa, "Transformed without anti aliasing")
```

## Enlarging images
```python
# Import the module and function to enlarge images
from skimage.transform import rescale

# Import the data module
from skimage import data

# Load the image from data
rocket_image = data.rocket()

# Enlarge the image so it is 4 times bigger
enlarged_rocket_image = rescale(rocket_image, 4, anti_aliasing=True, multichannel=True)

# Show original and resulting image
show_image(rocket_image)
show_image(enlarged_rocket_image, "4 times enlarged image")
```

## Proportionally resizing
```python
# Import the module and function
from skimage.transform import resize

# Set proportional height and width so it is half its size
height = int(dogs_banner.shape[0] / 2.0)
width = int(dogs_banner.shape[1] / 2.0)

# Resize using the calculated proportional height and width
image_resized = resize(dogs_banner, (height, width),
                       anti_aliasing=True)

# Show the original and rotated image
show_image(dogs_banner, 'Original')
show_image(image_resized, 'Resized image')
```

## Handwritten letters
```python
# Import the morphology module
from skimage import morphology

# Obtain the eroded shape 
eroded_image_shape = morphology.binary_erosion(upper_r_image) 

# See results
show_image(upper_r_image, 'Original')
show_image(eroded_image_shape, 'Eroded image')
```

## Improving thresholded image
```python
# Import the module
from skimage import morphology

# Obtain the dilated image 
dilated_image = morphology.binary_dilation(world_image)

# See results
show_image(world_image, 'Original')
show_image(dilated_image, 'Dilated image')
```

# 3. Image restoration, Noise, Segmentation and Contours
## Image restoration
```python

```

## Let's restore a damaged image
```python

```

## Removing logos
```python

```

## Noise
```python

```

## Let's make some noise!
```python

```

## Reducing noise
```python

```

## Reducing noise while preserving edges
```python

```

## Superpixels & segmentation
```python

```

## Number of pixels
```python

```

## Superpixel segmentation
```python

```

## Finding contours
```python

```

## Contouring shapes
```python

```

## Find contours of an image that is not binary
```python

```

## Count the dots in a dice's image
```python

```

# 4. Advanced Operations, Detecting Faces and Features
## Finding the edges with Canny
```python

```

## Edges
```python

```

## Less edgy
```python

```

## Right around the corner
```python

```

## Perspective
```python

```

## Less corners
```python

```

## Face detection
```python

```

## Is someone there?
```python

```

## Multiple faces
```python

```

## Segmentation and face detection
```python

```

## Real-world applications
```python

```

## Privacy protection
```python

```

## Help Sally restore her graduation photo
```python

```

## Amazing work!
```python

```

