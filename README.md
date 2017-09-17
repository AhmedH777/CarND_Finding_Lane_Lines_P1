# **Finding Lane Lines on the Road**

---

## Overview

The goal of this project is to build a pipeline to find lane lines on the road by using a combination of computer vision algorithms. The result of the project is the application of the build pipeline on a stream video input which generates a video output with the overlaid lane lines.

## Project Analysis

### Pipeline
---

My pipeline consisted of 5 steps which are:

#### 1. Convert Image to gray scale

![alt text][image1]

#### 2. Image Smoothing using Gaussian Blur filter

![alt text][image2]

#### 3. Edge Detection using canny edge detector

![alt text][image3]

#### 4. Region of Interest masking

![alt text][image4]

#### 5. Lines extraction using Hough Transform

![alt text][image5]

#### 6. Lines Processing

![alt text][image6]


The pipeline starts by getting the colored image from the video data stream, then the image is transformed to gray scale, after that and image smoothing step is applied using Gaussian blur filter in order to prepare the image for the canny edge detector which gets all the edges in the images by returning a Binary image of the detected edges.

The resulted edges binary images is then passed through a region of interest detection mask to only return the area which is more likely to find the lines in based on the camera mounting.Then, the resulted masked image is passed to the hough transform algorithm to return the detected lines in the image.

After that, a lines processing algorithm is applied to filter the lines returned from the Hough transform based on slope angle where the slope angle for each lines is checked against a pre configured mean slope angle within a certain standard deviation, if the line being checked is within the standard deviation of the mean value then it is considered as a lane line.

Finally, All filtered lines start and end points are fitted to one line then this line is extrapolated to overlay the lane lines.The output is then merged with the old lane lines using a complementary filter to allow a smooth change in the line states through the video stream.


### Potential shortcomings
---
One potential shortcoming would be what would happen when the lightning is changed which was clear in the challenge video that the algorithm fail due to the shades of the trees on the road which is a very tricky point to overcome.

Another shortcoming could be the intensity of colors which is highly affected by the reflected light which will differ in different periods of the day.

### Possible improvements
---
One possible improvement would be to track the line extension and slope to overcome the line disappearance.

Also another improvement would be to take the intensity of the color in consideration to apply a color segmentation step which would work in different lightning conditions.




























[//]: # (Image References)

[image1]: ./test_images/grayScale.png "Grayscale"
[image2]: ./test_images/smoothed.png "Smoothed"
[image3]: ./test_images/canny.png "Canny"
[image4]: ./test_images/masked.png "Masking"
[image5]: ./test_images/hough.png "Hough"
[image6]: ./test_images/lines.png "Lines"