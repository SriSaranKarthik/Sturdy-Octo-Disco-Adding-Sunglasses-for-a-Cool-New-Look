# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look
### NAME: K.SRISARAN KARTHIK
### REGISTER NO: 212224230275

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

Feel free to fork, contribute, or customize this project for your creative needs!

## Code
```

import cv2
import numpy as np
import matplotlib.pyplot as plt

faceImage = cv2.imread('/content/How To Robert Downey Jr Hairstyle at Ryandreher.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="694" height="544" alt="image" src="https://github.com/user-attachments/assets/241099f2-5166-4150-9e5e-6f047925d0d2" />

```
faceImage.shape
```
<img width="167" height="42" alt="image" src="https://github.com/user-attachments/assets/a51d1cbf-f98a-42c1-9340-b4a82ea7a4ba" />

```
glassPNG = cv2.imread('/content/584999937b7d4d76317f5ffd (1).png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
<img width="781" height="398" alt="image" src="https://github.com/user-attachments/assets/65275df6-4623-496b-81ab-a5100d2848b1" />
```
glassPNG = cv2.resize(glassPNG,(240,150))
print("image Dimension ={}".format(glassPNG.shape))
```
<img width="312" height="33" alt="image" src="https://github.com/user-attachments/assets/122c4e3f-a969-44e7-9eea-e0ef756e1b72" />

```
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

plt.figure(figsize=[16,16])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img width="1143" height="208" alt="image" src="https://github.com/user-attachments/assets/1e4cc2a9-6b2c-4543-aa66-7e056cb309a6" />

```
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[205:355,105:345]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```
<img width="541" height="371" alt="image" src="https://github.com/user-attachments/assets/862461a8-8764-4cc1-ac6a-058dac215f1a" />

```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[205:355,105:345]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
<img width="1383" height="160" alt="image" src="https://github.com/user-attachments/assets/7a810c8a-dd74-44eb-b260-7fc7f410fe5a" />

```
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[205:355,100:340]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
<img width="1102" height="426" alt="image" src="https://github.com/user-attachments/assets/6fc4013f-2796-48ef-b06c-f61ee69eb751" />

## Result
Program for adding Sunglasses to a Passport Photo Using OpenCV, Successfully executed
