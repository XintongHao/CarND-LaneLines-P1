# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images/solidYellowCurve.jpg "Grayscale"
[image2]: ./test_videos_output/solidYellowCurve.jpg 
[image3]: ./test_videos_output/improved_solidYellowCurve.jpg 
[image4]: ./test_videos_output/challenge_image.png
[image5]: ./test_videos_output/incorrect_line.png
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline has 6 steps:

1) Convert the image to grayscale image.

2) Apply Gaussian smoothing to the image with kernei_size = 7 which implies averaging, or smoothing, over a larger area.

3) Define parameters for Canny function (low_threshold = 50, high_threshold = 125) and apply to the image to detect the edges.

4) Define a four sided polygon to mask edges using cv2.fillPoly.

5) Define the Hough transform parameters and run it on edge detected image, output an image with hough lines drawn.

6) Draw the lines on the original image.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 

1) Storing all the left (x, y) points (of left lines) and right (x, y) points (of right lines) in the arrays separately.

2) Raise exception when there is no lines in the array.

3) Find the slope `m` and intercept `b` between those left and right points.

4) Get the first point from the bottom of the image where `y1 = maxY` and calculate its x1 using the given `m` and `b` parameters.

5) Get the second point from the middle upper of the image where `y2 = int((maxY/2)) + 60` and caculate its x1 using `m` and `b` parameters.

6) Draw the line on the image using cv2.
 
Original image example: 

![alt text][image1]

Before improvement, the lines are segments: 

![alt text][image2]

After improvement: 

![alt text][image3]

### 2. Identify potential shortcomings with your current pipeline


1) I didn't overcome the challenge problem where there is a 90 degree curve on the road.

![alt text][image4]

2) In some frams of the video, there are incorrect lines (in the 11 second in the solidYellowLeft.mp4) 

![alt text][image5]


### 3. Suggest possible improvements to your pipeline

1) One possible improvement is to detect curve and make segmentation lines on the curve lane line.

2) A better method is to use other line function to draw the curve like circular orbits. (especially for 90 degree curve)  

3) For the second shortcoming, I can try to figure out what happened when drawing the line, and raise some exception to solve this kind of problem.
