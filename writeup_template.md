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

[image2]: ./test_images_output/blur_gray.jpg "Blur_gray"

[image3]: ./test_images_output/edges.jpg "Edges"

[image4]: ./test_images_output/lane_solidWhiteRight.jpg "Lane"

[image5]: ./test_images_output/solidlane_solidWhiteRight.jpg "SolidLane"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, we get a picture like following.

![alt text][image1]

Then I use the gaussian filter to remove the noise from image and blur the initial image.

![alt text][image2]

After that, use the canny edge algorithm to extract the edges from the picture, what we get is as shown below.

![alt text][image3]

The fourth step is to pick our interesting zone to draw lines.

The last step is to use Hough Line function to find the lines and draw them.

![alt text][image4]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by seperate lines according to the value of their slopes. If it's positive, we consider it as right line and ignore the line with obvious wrong value(setting range is between 0.5 and 1.5). Then record these data and get the mean value of them. Finally, fit the data to a line function and draw it in the image.

![alt text][image5]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when driving on the coners, the assumption of the straight line cannot work well in this case or the prediction of trace is myopic. Also, the further left and right lines are somehow parallel and cannot be seperated based on their slopes.

Another shortcoming could be that the program cannot distinguish the dashed line and the solid line which may affect the decision make during the driving.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to we could make use of the color features to distinguish left and right lines, and at the same time use a second order polynomial to fit those line points.

Another potential improvement could be to make use of lines' length and their distance to each other to tell dashed line from solid line to help the future decision make. This could also be a optional feature for left and right lines seperation.

By making use these extra information, I think we can make it better.
