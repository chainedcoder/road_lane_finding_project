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

My pipeline consisted of 5 steps. 
1. I converted the images to grayscale
2. I applied the Gaussian blur with kernel size 5.
![alt text][https://www.dropbox.com/s/92yq12hoanpg69n/Screen%20Shot%202021-03-17%20at%209.26.54%20AM.png?dl=0]
3. Edge detection using canny edge the low and high threshold of 200 and 300
![alt text][https://www.dropbox.com/s/3snv55huncmeddk/Screen%20Shot%202021-03-17%20at%209.37.09%20AM.png?dl=0]
4. I selected the region of interest
![alt text][https://www.dropbox.com/s/7k0r4rnvo9axizx/Screen%20Shot%202021-03-17%20at%209.40.09%20AM.png?dl=0]
5. Applied the houghline function

Finally, in order to draw a single line on the left and right lanes, I modified the draw_lines() function by
i). Calculated the slope and intercept of each line
ii). Using slope seperate left and right lines (left lines have positive slope). Calculate length of lines
iii). Average the slopes and intercept with length as weight
iv) Calculate the x,y coordinates of lines
![alt text][https://www.dropbox.com/s/a7myopb2de7ibp9/Screen%20Shot%202021-03-17%20at%209.42.24%20AM.png?dl=0]



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming is that when the lighting on the road is too bright and too inconstistent, the lane marks can't be correctly computed and drawn.
Another shortcoming is that when there are many white or yellow marks on the road, this leads to incorrect edges and incorrect lanes. On the challenge video, the far left edge of the highway was too bright than the actual left lane marks - and since I'm using average of left lines with length as weight to compute the lane, and also becuase the region fell inside the region of interest, this causes the lane to be drawn away from the correct lane mark.


### 3. Suggest possible improvements to your pipeline

If it would possible to dynamically and more efficiently compute the region of interest, the markings on the challenge video might be more accurate.