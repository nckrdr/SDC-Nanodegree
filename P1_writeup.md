# **Finding Lane Lines on the Road** 

## Writeup

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

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I passed it through a gaussian blur to filter out artifacts in the image such as leaves, divots in the road or tire marks that could cause problems later on. I then passed this image through a canny filter to detect all edges, emphasizing the pixels where lane lines exist. Next, I passed the canny image through a region filter that only outputs the canny edges inside a certain region representing the road lanes. Finally, this cropped canny image passes through a hough lines filter, which draws two single lines representing the left and right lanes of the road. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by taking the array of all lines from hough transform and separating them into positive and negative slope groups. Then, I go over each slope group and average the slopes. I then find a sample point for each group to represent where a lane exists, and find the intercept, so I have a line equation for each lane line. Next, I find my "lowest point" for each lane line. I use the line equation I found previously with the bottom point of the screen to solve for an X value. From there, I find my top point by plugging in the lowest Y value in the image and solve for an X. Then, I connect these two points with a line using the average slope.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there are tight curves in the road. This pipeline only draws straight lines and is optimized to work best on long, straight roads. 

Additionally, this pipeline will only work for roads with clear lane markings and few artifacts on the road. If a road is covered in leaves or snow, my pipeline will have issues. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to detect when a road is curving and draw non-straight lines over the lanes. 
