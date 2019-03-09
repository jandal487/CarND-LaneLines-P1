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

My pipeline consisted of these steps:

1. grayscale(): convert images to grayscale
2. gaussian_blur(): Blur the image using Gaussian smoothing
3. canny(): Apply Canny Edge Detection algorithm on blured images
4. I did some hyper parameter estimated to comes up with right VERTICES of polygon to crop in next step
5. region_of_interest(): Used previous calculated VERTICES paramter and extracted region of interest
6. hough_lines(): Executed Hough Transform to find lines in image
7. weighted_line(): Applied this function to reconstruct image initial image with the image after Hough Transform

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
1. Collected coordinates for each line segment into left and right line as lists
2. For each small line, stored respective slopes and intercepts & then calculated average of slope & intercept
3. Calculated y_min, y_max
4. Now considering the positivity or negativity of the slope, calculated x_min and x_max using intercept & slope
5. Draw a line using (x_min, y_min) and (x_max, y_max)

If you'd like to include images to show how the pipeline works, here is how to include an image: 

#### Result: Video solidWhiteRight
![Video solidWhiteRight](/test_videos_output/solidWhiteRight.gif)


### 2. Identify potential shortcomings with your current pipeline


I think there are still allot of shortcomings when we are looking for a general solution. The reason is that this is a heuristic solution to detec and draw lines on the road lanes and it is certainly not a general solution. The hyperparamters are found considering only these images and if given completely new (or different) stream of images then this parameter setting won't detect lanes correctly.


### 3. Suggest possible improvements to your pipeline

There can be allot of improvements done to this pipeline to get a better heuristic bases solution. Some of them are as following:
1. There is not allot of smoothness in displaying lines while playing a video stream. This should be fixed by fine tuning the implementation.
2. I reckon advance computer vision techniques can be applied to pre-process images more finer and then apply algorithms for edge detection, draw lines etc. Currently, I am simply applying gaussian smoothing, pixel threshold values, & cropping out region of interest manually.





