# **Finding Lane Lines on the Road** 
## Writeup


### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
The pipeline I have created takes as the image or a frame from a video input and processes it.

The steps I used to create the pipeline had the 6 following steps:

1.I converted the images to grayscale using the open cv using:
  cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

  Now, the grayscale image was smoothened using a Gaussian filter. For this the following line of code was used:
  return cv2.GaussianBlur(img, (kernel_size, kernel_size), 0)

2.Then I used the canny edge operator to detect edges in the smoothened image using :
  cv2.Canny(img, low_threshold, high_threshold)

3.Now I've masked an ROI in the shape of a trapezium arround the lane line pixels.
  The code for this is written in the function **region_of_interest()** of cell no 3 of the iPython Notebook **P1**.

4.Now all the lines in the ROI are stored in an array using the open cv method :
  cv2.HoughLinesP(img, rho, theta, threshold, np.array([]), minLineLength=min_line_len, maxLineGap=max_line_gap)

5.All the lines that are stored are now filtered using the slope filter technique in which horizontal lines and 
  lines with slopes more than half are declared as outliers and eliminated. 

6. Now I've taken the mean of the accepted slopes and the lane lines are drawn on the original image. 
   This functionality can be found in the function **draw_lines()** of cell no 3 of the iPython Notebook **P1**.

I've uploaded the videos on Youtube and they can be found here:
For the solid white right input video [here](https://www.youtube.com/watch?v=m213hS8g74I&feature=youtu.be)
For the solid yellow left input video [here](https://www.youtube.com/watch?v=TsDMq_RS8d4&feature=youtu.be)


### 2. Identify potential shortcomings with your current pipeline

One drawback of using this method, I believe, would be what happens if the lighting conditions on the road are not up to the requirements for this code to function correctly.
The algorithm will not be able to identify the lane line pixels under poor lighting conditions.

Also if we consider different weather conditions like snow , this algorithm will not be able to differentiate between lane lines and the snow particles.


### 3. Suggest possible improvements to your pipeline

As I've read the following course, I realised that a possible improvement to this pipeline would be using other color formats like HSV and HLS instead of RGB. 
Thresholding these different channels might just help in detecting lane pixels in different light conditions.

Also, I think averaging the final slopes from previous frames in the video and then using that to plot lines in the next frame would help in avoiding the fluttery motion of the drawn lane lines.

