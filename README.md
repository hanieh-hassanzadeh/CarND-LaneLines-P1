
Author: Hanieh Hassanzadeh

e-mail: hassanzadeh.hanieh@gmail.com

# **Finding Lane Lines on the Road**

The aim of this project is to detect the lane lines on the road, used by self driving cars. It is the first project of Udacity's Self-Driving Car Engineer Nanodegree Program.


## Overview

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle (Udacity).


## 1. Required Python packages

- numpy
- openCV
- IPython
- os
- math
- moviepy


## 2. Pipeline
My pipeline consistes of 9 steps: 

a. Converting to gray scale to be able to feed it into canny.

b. Applying gaussian blur to reduce the noises.

c. Detect the edges, using Canny method.

d. Defining a region of interest (ROI) in which is most likely the desired lines fall through.

e. Selecting only the edges which are within the ROI.

f. Ignoring the edges with less than pi/8 or more than -pi/8 angle (as they are less likely to be part of lane-lines).

g. Splitting the remaining edges into left- and right-aligned lines (by `tan` of their angles).

h. Defining one single line from averaging the slopes and intercepts of the lines for each group defined in step `g`.

i. Merging the original picture and the two final lines.


I replaced the draw_lines() function by unifyLines() function, entirely. I did so because there were more steps required for video processing than image processing. Namely, for video processing, I implemented a possibility to use the line properties from the previous frame when no edge could be detected in either right or left side. This is a reasonable assumption, as the lines do not change drastically between consequent frames. 

unifyLines() inputs the averaged slope and intercept of each line groups defined in step `g`, and its output is the two points, the final line is passing through.


## 3. Shortcomings

a. What if due to construction (or any other reason), some part of the road has no or very light-colored lines?

b. What if the ROI includes less or too much of the area suitable for the method implemented in this code?

c. I would guess night-time needs more steps to detect the lane-lines.

d. There should be more considerations where either of the lines intersect with other lines on he road, e. g., near the 'Exits' and entering the 'Ramps'.

e. Other type of lines/signs/objects on the roads should be catagorized separately' e. g., cross lines.

f. I implemented the possibility for a videoframe to use the previous frame's line properties if no edge could be detected in either sides. However, no strategy is considered for the case of no line detected for the very first frame.

g. The lines on the video are not stable, and they shake a lot (I am not sure if this is really a shortcoming, though).


## 4. Suggestion for possible improvements

Bellow are the possible improvements addressing each point of shortcomings, respectively.

a, b. Deep learning should be used for a better line estimation.

c. The color range to detect the lines should be adjusted.

d, e. The lines with very different angles (can we call them outliers) should be ignored.

f. The code could ignore the first image frames with no edge detected untill it detects both the lines. 

g. If the line properties from several previous images were saved, one could averaged the line slopes and intercepts from more than one frame to achive a more stable lines.




