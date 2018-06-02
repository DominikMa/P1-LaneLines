# **Finding Lane Lines on the Road**

This repository contains my solution for the project "Finding Lane Lines" of the Udacity Self-Driving Car Engineer Nanodegree Program. The python code could be found in the jupyter notebook [P1](P1.ipynb), the generated images in the folder [test_images_output](test_images_output/) and the videos in the folder [test_videos_output](test_videos_output/).

The following part of the README conatains a writeup which describes how the lane finding is achieved.


## Writeup

### Goals

Given images or videos the goal of this project is to detect the lanes in these and draw them on the images.

[//]: # (Image References)

[step0]: ./writeup_images/solidYellowCurve.jpg_step0.png "Original Image"
[step1]: ./writeup_images/solidYellowCurve.jpg_step1_masked_image.png "Masked Image"
[step2]: ./writeup_images/solidYellowCurve.jpg_step2_blur_gray_image.png "Blured Gray Image"
[step3]: ./writeup_images/solidYellowCurve.jpg_step3_edges_image.png "Edges found with CannyEdge Detector"
[step4]: ./writeup_images/solidYellowCurve.jpg_step4_masked_edges_image.png "Edges in Region of Interesst"
[step5]: ./writeup_images/solidYellowCurve.jpg_step5_hough_lines_image_image.png "Lines found with Hough transform"
[step6]: ./writeup_images/solidYellowCurve.jpg_step6_drawn_lines_image.png "Drawn Lanes"
[step7]: ./writeup_images/solidYellowCurve.jpg_step7_weighted_imgage_image_image.png "Output Image"

---

### Reflection

The used pipeline consisted of following 5 steps:

1. #### Filter for white and yellow colors

   Because it is known that the lanes are only yellow or white the image is filterd for these colors.
   Therefor the image ist converted to the HSV color model, colors which are not yellow or white are masked out and the mask is applied to the original image. Using this image as input
   ![alt text][step0]
   we get the following output after the first step:
   ![alt text][step1]

2. #### Grayscale and Blur

   For detecting the lanes their color is irrelevant, so that in the second step the image is converted to grayscale and after that a blur filter is applied.
   Now we get this image
   ![alt text][step2]

3. #### Canny edge detector

   To find all points which are part of edges we use the canny edge detector on the grayscale image.
   The following edges are found in the previous image
   ![alt text][step3]

4. #### Region of interest

   Because we know which region of the image contains the lanes other parts of the image can be masked out.
   Now we get this image
   ![alt text][step4]

5. #### Hough line detector

   To find the lines in the image of edges the Hough line detector is used.
   These lines are found
   ![alt text][step5]

6. #### Drawing the lanes

   To extend te lines to lanes and draw the left and right lane first all lines are sorted into lines for the left or right lane. This is done by the gradient of the lines. Additionally all lines which have a gradient above or below a threshold are filterd out because they can't be part of a lane.

   After that the numpy function `polyfit` is used to find a single line which fits best through all points of the left lines and another one which fits for the right lines. These two lines should be the searched lanes.
   The found lanes are shown in this image
   ![alt text][step6]

After the found lanes are combined with the original image we get the following final output
![alt text][step7]



### 2. Identify potential shortcomings


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Possible improvements

A possible improvement would be to ...

Another potential improvement could be to ...
