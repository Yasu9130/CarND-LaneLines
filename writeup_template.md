# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 9 steps. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by least square method.

1. Convert images to HLS

    The lines are more recognizable in HLS than RGB.

2. Blur images by Gaussian Filter

    To decrease noises, the images are blurred.
    At this step, this app prepares 2 blurred images for next step.

3. Extract each color, yellow and white, by inRange()

    Yellow and white color have different theshhold values respectively.
    Therefore, this app prepares 2 extercted images respectively.

4. Create a mask image and get AND of the original image

    This app combines each extracted images by bitwise_or() to create a mask image.
    Then, this app applys the mask image to the original image by bitwise_and().

5. Detect edges by using Canny method

    Before applying Canny method, the images are converted to Grayscale.

6. Define region of interest

    To detect lines easily and decrease noises, this app defines region of interest.
    The area is deifned by 4 vertices.

7. Detect lines by using Hough Transform

    At this step, many lines are detected no matter how you tune parameters.
    2 Lane lines are determined by next step.

8. Estimate each lane by least square method

    To estimate the best line from detected lines, this app uses least square method.
    This method is useful to exclude outliers.

9. Draw the estimated lines

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when true lanes are out of roi.

Another shortcoming could be parameters to use OpenCV func. 
If Test videos are changed, this app does not detect lane lines.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to define roi dynamically.

Another potential improvement could be to define parameters dynamically.
(Especially, Canny() and HoughLinesP() )
