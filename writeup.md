#**Finding Lane Lines on the Road** 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)


[image5]:./processed_images/gray_canny_region_hough_combinedsolidWhiteCurve.jpg
[image4]:/processed_images/gray_canny_region_houghsolidWhiteCurve.jpg
[image3]:/processed_images/gray_canny_region_solidWhiteCurve.jpg
[image2]:/processed_images/gray_canny_solidWhiteCurve.jpg
[image1]:/processed_images/gray_solidWhiteCurve.jpg


---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. 

1. Convert the image from 3 channel color(0-255,0-255,0-255)  to 1 channel gray color(0-255)
2. Do Gusssian blur on the image to avoid some weird artifact in final image in next process
3. Do the Canny edge detection, if skip this phase, it will has big area of line selected, we need it remove out most filled area, leave only edge there for next step
4. Do region selection on the part need included, this parameter is kind of very subjective, but it do help to remove a lot of non-road line edge, especially those road edge long line    
5. Do hough transformation to find the longest line in the selected area


In order to draw a single line on the left and right lanes, I modified the draw_lines() function which take solid parameter to add branch to do the solid line drawing, here is how it implement:

1. divide the line into left side or right side by its slop
2. iterate to get the Xmax or Xmin  when each line extend Y to bottom on left and right side of road
3. iterate the point to  get Ymin  on both side
3. sum up the slop value on both side, and average them out
4. draw solid line from ((Xmax+Xmin)/2,Ybottom),  thickness: Xmax-Xmin, average slop, to reach Ymin


If you'd like to include images to show how the pipeline works, here is how to include an image: 

A little bit compare with gray file with original one , it look like it increase the size dramatically, Alpha channel is Yes now, don't know why?


![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]


###2. Identify potential shortcomings with your current pipeline

The red line flick, and sometime it disappear, a cross over show up.
The draw solid line method is error-prone, I add too much adjustment to make sure it doesn't over limit, but it turn out add a lot of noise.


###3. Suggest possible improvements to your pipeline

Make the draw solid line more efficiency.