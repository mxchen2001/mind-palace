# Gaussian and Laplacian Pyramids

Image you need to change the resolution of a 1024x1024 image to a 128x128 image. How would you go about doing this?

Some naive solutions include, removing some pixels from the image — perhaps every other pixel — until the desired resolution is reached.
This will cause **Aliasing** in the spatial domains because as we downsample the image, high frequency components such as edges and corners will be lost, or aliased such that the image is no longer **smooth**.

We can alternatively apply an averaging filter to the image. This will mitigate the aliasing because an averaging filter is a LPF (this can remove higher frequencies). However, the issue with the averaging filter is that it will cause spectral leakage due to the nature of a squaring block (infinite frequency response).

The best solution to this problem is to use a **Gaussian Pyramid**.

Notice the special relationship between the time and frequency representation of a gaussian filter — it's the same.

The algorithm for building a Gaussian Pyramid is:

```py
def gaussianPyramid(img):
    pyramid = [img] # starting with the original image
    while img.width > 128 or img.height > 128:
        # filter
        img = gaussianFilter(img) # you can use cv2.pyrDown(img)

        # downsample by 2
        img = img.resize((img.width // 2, img.height // 2))

        # add to the pyramid
        pyramid.append(img) 
    return pyramid
```

Note that the gaussian filter should be odd and have a variance, $\sigma = \sqrt{\frac{\text{sampling rate}}{2}}$

Now the question becomes: "Can we reconstruct the original image from a higher level of the gaussian pyramid?"
Short answer: No, because we are deliberately removing information.

The solution to this is to use a **Laplacian Pyramid**.

You want to follow the same steps as the Gaussian pyramid, but before subsampling, you will take the difference between the original image and filtered image and store the residuals. Lastly, when you've reached the desired resolution, you will save the gaussian filtered image.

Having the residuals and the final gaussian filtered image, you can reconstruct any level of the pyramid.

```py
def laplacianPyramid(img):
    final = None
    pyramid = [] # starting with the original image
    while img.width > 128 or img.height > 128:
        # filter
        filtered_img = gaussianFilter(img) # you can use cv2.pyrDown(img)

        # find residuals
        residual = img - filtered_img
        # add to the pyramid
        pyramid.append(residual) 

        # downsample by 2
        img = img.resize((img.width // 2, img.height // 2))

    # store final gaussian filtered image
    final = img

    return pyramid, final
```
