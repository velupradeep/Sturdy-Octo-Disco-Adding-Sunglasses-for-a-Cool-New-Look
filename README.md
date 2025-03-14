# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

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

## Program:
### Name:PRADEEP V
### Reg.no:212223240119

import cv2 
import numpy as np
import matplotlib.pyplot as plt
myimage = cv2.imread('WhatsApp Image 2024-01-09 at 21.26.03_7aea8f7c.jpg')
plt.imshow(myimage[:,:,::-1]);plt.title("Face")
myimage.shape
glassPNG = cv2.imread('sunglass-png-aviator-sunglass-png-clipart-3381.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(430,110))
print("image Dimension ={}".format(glassPNG.shape))
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:2]
glassMask1 = glassPNG[:,:,2]
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
faceWithGlassesNaive = myimage.copy()

# Correct assignment
faceWithGlassesNaive[400:510, 310:740] = glassBGR

plt.imshow(faceWithGlassesNaive[..., ::-1])
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = myimage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[400:510, 310:740]

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
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[400:510, 310:740]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(myimage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
## Output:
### 1.Original image:
![image](https://github.com/user-attachments/assets/399dec1b-df84-40f3-bcae-375ac2639669)



### 2.Glass:
![image](https://github.com/user-attachments/assets/6766ac36-73c1-42b9-99e4-6ca591a49f6c)



### 3.Glass color channel:
![image](https://github.com/user-attachments/assets/794f7886-425d-447f-8119-9e1ca06decfc)




### 4.Face With Glass:
![image](https://github.com/user-attachments/assets/8ac9b126-07dc-422d-9615-0a43458045d9)



### 5.Eye and glass region:
![image](https://github.com/user-attachments/assets/b7455935-3fea-4a56-a051-3bcc8f98accf)






### 6.Final image with glass:
![image](https://github.com/user-attachments/assets/14170bf1-44f9-4297-a742-6e7d1d5128a3)




## Result:
Thus, the creative project designed to overlay sunglasses on individual passport size photo has been successfully executed.
