#**Finding Lane Lines on the Road** 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road

[//]: # (Image References)



---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps: 

1.) First, the images were converted to gray scale and a Gaussian smoothing function was applied on the image.

[image1]: ./examples/grayscale.jpg "Grayscale"

2.) After that the pipeline runs openCV's Canny function on the resulting images, which

shows which part of the image has high colour gradients like abrupt colour changes (e.g. lane marks).

3.) Now the image is ready to run the Hough Lines algorithm and detect the points in those lines, but before that

we mask the image to a region of interest which represents the area where the lane marks are generally positioned.

4.) Run OpenCV's Hough Lines algorithm to output points for every line segment detected.

5.) In order to draw a single line on the left and right lanes, I modified the draw_lines() function to sort

every detected line segment by slope and position and thus classifying them into potential candidates to fit the

left and right lane marks. Additional slope thresholds for unrealistic slope values were also applied.

Then to draw the lines the sorted points were fitted with a 1th degree polynomial (a line basically).

For the cases were no valid points were found a TRY and EXCEPT block was added. In the except block

a global variable is accessed which contains the lines stored in the previous iteration for the last video frame.



If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


###2. Identify potential shortcomings with your current pipeline


The solution will probably not generalize well to all imagery, since the slope thresholds and the region of interest
were chosen to fit the image properties (like image ratio) of the test cases.

More importantly the solution provided wont work for big turns, where the lane lines are not straight at all and

dont fit the region of interest.

The optional challenge shows that the pipeline has a hard time detecting the yellow line when the asphalt colour changes

to a brighter colour.

Shadows made the algorithm detect a lot of clutter which was also hard to deal with, so most probably the pipeline does not

work when the lighting is low (like at night).


###3. Suggest possible improvements to your pipeline

A possible improvement would be to average the detected lines over several video frames or dampening the jittering in some way.

Like for example keeping track of the jittering/change of the line slope and filtering out unrealistic big changes from one

video frame to the next.

Another potential improvement could be to find a more automatized way to find the region of interest which generalizes better 

and also handles better recognizing the lines in big turns.
