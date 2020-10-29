# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The objective of this project is to make a pipeline which identifies lane lines on the road. The efforts have been reflected in the below Summary.

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The task here is to identify lanes in a video by drawing lines on the left and right edge of the lane where our car is driving.
For this I have gone though a pipeline which can be described as below:
The pipeline is first created for an image which is later applied to a video, which a series of frames(images).

The pipeline is: First, I have converted image to grayscale. 
![grayscale] [./test_image_output/gray.png]

Then I have applied a Guassian blur function of kernel size=13 for further smoothening of image.
![guassian_blur] [./test_image_output/gaussian_blur1.png]

On this smoothened image, I have applied Canny edge detection to detect all the edges in it.
![edges] [./test_image_output/edges1.png]

From this image I have masked a ragion of interest where our lane line probably exist.
![masked_image] [./test_image_output/masked_image1.png]

Then I have used Hough transform to draw red coloured lines on the lane edges detected in region of interest. 
![lines_image] [./test_image_output/hough1.png]

Finally I have combined these lane lines with the original image to show exact plotting of lane lines on original image. 
![lines_edges] [./test_image_output/final1.png]

As part of modifying the draw_lines() function, Firstly, I have tuned rho, theta, threshold, min_line_len and max_line_gap parameters of Hough trasform to get draw line segments over lane segments detected as much as possible. Secondly, I have taken slope of line segments detected and extrapolated them into left and right lines segments and averaged them to get left and right lane lines to draw on the original image.


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming is that these lane lines may not work appropristely on curved lanes.

The shortcoming of the curved lane could be solved by using a quadratic fit, instead of a linear fit, where we’d have more coefficients and we could create the curved lane accordingly. The problem of ending one lane could be solved by creating a temporary parallel lane for the vanished lane allowing the car to change lanes until it finds well defined lanes. The problem of cracks on the roads leading to edges in the region of interest could be solved by creating a regions of interest which is a combination of offsetted trapezium, with parallel edges, one sitting inside and one outside. This would only keep the lanes in the region and as long as a lanes are defined, we’ll have our lines.

### 3. Suggest possible improvements to your pipeline

One improvement can be using a different color space. HSL will be much more efficient in finding the yellow lane line and in case of shadows.The HSL color mask in this sceneario performs better than the RGB because it is able to consistently filters smooth yellow pixels than RGB color mask, despite it sometimes picks up unwanted noises such as yellow road sign and the lawn on the right. However, these minor imperfections of HLS mask should not be a problem, as later we can apply region of interest to specifically crop the non-road regions.


