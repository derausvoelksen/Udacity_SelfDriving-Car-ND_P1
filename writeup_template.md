# **Finding Lane Lines on the Road** 

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

My pipeline consisted of 5 steps: grayscaling, applying gaussian blur, masking the region of interest, doing canny edge detection, getting hough lines.

Finally, I drew the hough lines (and the region of interest) in the orinigal image. The resulting images and videos can be identified by the _CS file ending.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function.
I needed to find a slopes and y-intercepts for both sides (left and right). I used the np.polyfit function on the hough lines (ignored steep and flat slopes) to do so, and then drew a line from the bottom of the image to the upper end of the region of interest using the resulting slopes and y-interecepts.
For the challenge Video, I modified the region of interest in such a way, that the lower part of the image (y coordinate > 9/10 of y_max) is not included in the region of interest in order to cut out the hood.



### 2. Identify potential shortcomings with your current pipeline

At the moment, the region of interest is static, and tuned by hand --> lane detection will be errorous on sharp corners or overrun of hills or bumps.



### 3. Suggest possible improvements to your pipeline

* lacking of smoothening the slopes (for example weighted average over 3 frames)
* lane is just a line, and will not follow curves. Polynomials of higher degree (3) could be used to fit in curves.