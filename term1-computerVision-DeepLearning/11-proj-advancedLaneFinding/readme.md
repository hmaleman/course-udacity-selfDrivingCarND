# Project: Advanced Lane Finding

## 1. Goal
The goal of this project was to create a software pipeline to identify the lane boundaries in a video from a front-facing camera on a car. The camera calibration images, test road images, and project videos are available in the [project repository](https://github.com/udacity/CarND-Advanced-Lane-Lines).

## 2. Applied methodology
### 2.1. Camera Calibration
The provided project repository contained a set of chessboards like images from different positions in order to get the camera calibration parameters to be later used to undistort the image captured at the car.

For this project OpenCV was used and with the help from **cv2.findChessboardCorners()** was possible to get camera parameters with **cv2.calibrateCamera()**. With those parameters in hand, it was possible to undistort the images captured by the camera and also to warp them. 

The complete camera calibration pipeline is available at [01-proj-cameraCalibration.ipynb](01-proj-cameraCalibration.ipynb)

The following images present the complete transformation process for one sample image.

![Step1](./20-output-report/Step1.png)
![Step2](./20-output-report/Step2.png)
![Step3](./20-output-report/Step3.png)
![Step4](./20-output-report/Step4.png)
![Step5](./20-output-report/Step5.png)

### 2.2. Pipeline
Core part of this project was the pipeline which involved in summary the following steps:
- Undistort the input image based on the parameters stored from the Camera Calibration phase
- Filter the image to the zone of interest, in order to capture only the lane lines. Several filters, were used here, from cropping, Sobel gradient on X and Y axis, Sobel gradient direction, collor threshold for HSV color space (only used Saturation channel), collor threshold for HSV color space (only used Value channel). The final image was quite clear.
- Following the filtering, a convolution was applied to the image subsections in order to identify the lane marks
- Once the lanes zones were identified a 2nd degree polyfit was used to extrapolate the lane marks
- With the extrapolated lane lines, it was possible to calculate the lane radius and also the car displacement with regard to the lane center.

The pipeline is documented at the jupyter notebook [02-proj-advancedLaneFinding.ipynb](02-proj-advancedLaneFinding.ipynb). The following images present the pipeline applied to a single test image.

![Pipeline1](./20-output-report/Pipeline1.png)

![Pipeline2](./20-output-report/Pipeline2.png)
![Pipeline3](./20-output-report/Pipeline3.png)
![Pipeline4](./20-output-report/Pipeline4.png)
![Pipeline5](./20-output-report/Pipeline5.png)
![Pipeline6](./20-output-report/Pipeline6.png)
![Pipeline7](./20-output-report/Pipeline7.png)

## 3. Results
There were some really hard sections on the pipeline development, in special to tune the image filters to get mainly lane lines to forward to the convolution step. The final pipeline works perfectly at the reference video, it is however on good light conditions, and the pipeline is certainly still limited.  

The reference video used for this project processed by the pipeline is also available at **YouTube**, click to watch!

[![Advanced Lane Finding](https://img.youtube.com/vi/QwwvT9pDWGM/hqdefault.jpg)](https://youtu.be/QwwvT9pDWGM "Advanced Lane Finding - Click to Watch!")

## 4. Keywords:
Computer Vision, Image transformation, Camera Calibration, Bird-Eye view, Sobel gradient
