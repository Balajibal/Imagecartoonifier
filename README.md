## Aim:
To cartoonify an input image
## Steps:
1)Importing the required packages
2)Getting image as input
3)Transforming an image to grayscale
4)Smoothening the grayscale image
5)Preparing a Mask Image
6)Giving a Cartoon Effect

## Program
```python
import cv2
import matplotlib.pyplot as plt
image = cv2.imread("grouup.jpg")
grayScaleImage = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
ReSized1 = cv2.resize(grayScaleImage, (960, 540))
plt.imshow(ReSized1, cmap='gray')
ReSized2 = cv2.resize(grayScaleImage, (960, 540))
smoothGrayScale = cv2.medianBlur(grayScaleImage, 5)
ReSized3 = cv2.resize(smoothGrayScale, (960, 540))
getEdge = cv2.adaptiveThreshold(smoothGrayScale, 255,cv2.ADAPTIVE_THRESH_MEAN_C,cv2.THRESH_BINARY, 9, 9)
ReSized4 = cv2.resize(getEdge, (960, 540))
colorImage = cv2.bilateralFilter(image, 9, 300, 300)
ReSized5 = cv2.resize(colorImage, (960, 540))
cartoonImage = cv2.bitwise_and(colorImage, colorImage, mask=getEdge)
ReSized6 = cv2.resize(cartoonImage, (960, 540))
images=[ReSized1, ReSized2, ReSized3, ReSized4, ReSized5, ReSized6]
fig, axes = plt.subplots(3,2, figsize=(8,8), subplot_kw={'xticks':[], 'yticks':[]}, gridspec_kw=dict(hspace=0.1, wspace=0.1))
for i, ax in enumerate(axes.flat):
    ax.imshow(images[i], cmap='gray')
plt.show()
```
## Output:

![Screenshot (246)](https://user-images.githubusercontent.com/75234946/176443536-9ec01a9d-dadd-48df-8e50-5ddff2b27e28.png)
