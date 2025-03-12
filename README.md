Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## PROGRAM:
## NAME: SANTHIYA R
## REG NO : 212223230192

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
Image = cv2.imread('Photo.jpg')
plt.imshow(Image[:,:,::-1]);plt.title("Image")
Image_copy=Image.copy()
```
![Screenshot 2025-03-12 143627](https://github.com/user-attachments/assets/73e3b5c8-c111-45f3-9b9e-ae94d2442199)

```
glassPNG = cv2.imread('sunglass.png', cv2.IMREAD_UNCHANGED)
plt.imshow(glassPNG[:,:,::1]);plt.title("glass")
```
![Screenshot 2025-03-12 143718](https://github.com/user-attachments/assets/1cbfed3f-13e9-46af-a019-9eeaee1a0dd4)
```
glass_width = 200
glass_height = 50
glassPNG = cv2.resize(glassPNG, (glass_width, glass_height))
print("Image Dimension ={}".format(glassPNG.shape))
```
![Screenshot 2025-03-12 143814](https://github.com/user-attachments/assets/28607db7-feff-46fc-b11d-58097d174ea5)
```
glassBGR = glassPNG[:, :, :3]
glassalpha = glassPNG[:, :, 3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Colored Sunglass');
plt.subplot(122);plt.imshow(glassalpha, cmap='gray');plt.title('Alpha Sunglass');
```
![Screenshot 2025-03-12 143906](https://github.com/user-attachments/assets/a5f9dbd5-a869-4a4e-a951-65e97a1cd8be)
```
y1, y2 = 135, 135 + glass_height
x1, x2 = 110, 110 + glass_width
if x2 > Image_copy.shape[1]:
    x2 = Image_copy.shape[1]
if y2 > Image_copy.shape[0]:
    y2 =Image_copy.shape[0]
roi = Image_copy[y1:y2, x1:x2]
glassMask_inv = cv2.bitwise_not(glassalpha)
face_bg = cv2.bitwise_and(roi, roi, mask=glassMask_inv)
glass_fg = cv2.bitwise_and(glassBGR, glassBGR, mask=glassalpha)
eyeRoiFinal = cv2.add(face_bg, glass_fg)
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(face_bg[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(glass_fg[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
![Screenshot 2025-03-12 144018](https://github.com/user-attachments/assets/5bb6a266-16b1-471b-9a9d-ae4fce32cc28)
```
Image_copy[y1:y2, x1:x2] = eyeRoiFinal
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(Image[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(Image_copy[:,:,::-1]);plt.title("With Sunglasses");
plt.show()
```
![Screenshot 2025-03-12 144144](https://github.com/user-attachments/assets/95987fff-9783-47e3-9ac2-4256f5921227)

Feel free to fork, contribute, or customize this project for your creative needs!
