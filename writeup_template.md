# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals of this project are the following:  
*Make a pipeline that finds lane lines on the road  
*Reflect on your work in a written report




---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 


1. Converted the images to grayscale.  
2. Apply Canny Edge (with Gaussian smoothing) to the image, which low_threshold = 90, high_threshold = 130. 
3. Define Region of Insterest and apply to the image. 
4. Using the Hough Transform to find the lines. 
5. Draw the lines on the raw image.

In order to draw a single line on the left and right lanes, I add the drawing separate_lines function to separate lines into left and right by slope value, if > 0.5 is left lane, < -0.5 is right lane.   

Also, to merge lines into a single line(for line extention in next step), I add merge_lines(lines) function.This fuction is simply caculate the average for each lines.  

To extend the lines, I add some code in draw_lines function. It make a line model by caculate line slope and offset.  

Additional, to reduce the line 'shaking' and to avoid some interference, I add an adjustment function(like learning) by adding global varivables for slopes to record the them continuously, it is the average of all slopes from the beginning, large deviation data will also be cut off.

Test on picture before adding average and extrapolate the line:   
![alt text](C:\Users\Instrumentation\Documents\GitHub\CarND-LaneLines-P1\test_videos_output\1.png)  
Test on video after adding average and extrapolate the line:  
![图片描述](C:\Users\Instrumentation\Documents\GitHub\CarND-LaneLines-P1\test_videos_output\2.png)  

As for the challenge, I didn't pass it as the left line disappeared when light change rapidly, I attach the video only for reference.

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the lane change rapidly, global slopes maybe cut it off, the threshold shall be selected very carefully.  
Another shortcoming is it still cannot pass the all challenge part, when light change rapidly, the line disappeared. I think it could only be handled by enhance Canny and Hough Transform part.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to make it more robust by enhance Canny and Hough Transform part and adding a more smart learning function.
