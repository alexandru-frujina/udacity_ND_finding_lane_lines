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

My pipeline consisted of 5 steps:
1. I converted the RGM image to grayscale
2. I applied a gaussian blur with a kernel of 5
3. Applied the Canny filter with a threshold between 60 and 180
4. Isolated the image to only the region if interest
5. Applied the Hough lines algorithm to extract the lane lines and overlay them as a an image on the original image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function to first divide between a left line list and a right line list based on the slope of each line.

There are two code files submitted:
./P1.ipynb -> for the mandatory project
Output can be found in the directories: ./test_images_output, ./test_videos_output

./P1-Just-Challenge.ipynb -> just for the challenge project
Output can be found in the file ./test_videos_output/Just-Challenge.mp4

The main idea of for the challenge project is to mask just the region of the lane lines by applying another inverted mask over the previos mask:
[image1]: ./JustChallengeIdea.png "Challenge Idea"


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming is when a line is classified wrongly in the left line lane while it is actually part of the right lane line list and vice-versa based on the calculated slope. If this happens the estimaged lane can be way off.

Another shortcoming is when a curved line is encountered. In this case a polynomial fit of a higher degree will produce better results but also the classification between left lane line and right lane line becomes more difficult as the slope values may not be sufficient to classify the lane lines.

The method outlined in
[image2]: ./JustChallengeIdea.png "Challenge Idea"
may sometimes not be able to detect lane departure for example.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to classify the lane lines on a curved road. A second order or higher polynomial can be used to fit the lane lines.

For both the mandatory and challenge projects the input parameters for the canny threshod, vertex region and hough transform cab be further tweaked.