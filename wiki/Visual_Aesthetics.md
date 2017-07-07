---
title: Visual Aesthetics
permalink: wiki/Visual_Aesthetics/
layout: wiki
---

Visual feature extraction tool
------------------------------

A command line utility that can be used to generate metadata for visual
quality assessment, it relies on opencv 3.2 library of algorithms to
compute features that describe images and videos in respect to visual
properties carefully selected from state-of-the-art literature. An
extensive review and testing was made to find a group of visual features
good for the task of visual discrimination. A top-down aproach for
extraction results in a very compact feature vector. A graphical
interface (demo available
[here](https://drive.google.com/file/d/0Bzelhrdw43rCc0JkOGdSNnYtclE/view?usp=sharing))
was used to check overall usability and performance of the features. A
subset was used to train classifiers for aesthetic and interestingness
and some of the features were also indexed and used to compute a
similarity metric.

### Usage

The utility accepts images or videos as input. The files can be loaded
from a text file list or by providing a folder path. The output feature
vector is saved in CSV format.

example 1: Extract features from image files in bin/data/images folder
to the CSV file images\_output.csv

The resulting output file can be found
[here](https://drive.google.com/file/d/0Bzelhrdw43rCWWc5QWQtQmp6Y0E/view?usp=sharing).

example 2: Extract features from video files in videos.txt to the CSV
file video\_output.csv

[Here](https://drive.google.com/file/d/0Bzelhrdw43rCQURPaHYwaUoyMFk/view?usp=sharing)
is the resulting feature vector in CSV format.

### Feature description

In this section we made a list of features,for each one we explain its
relevancy and show the range of acceptable values

-   file\_path - path to media file

The path of folder, text file or url to the media. note: -d argument
should be set acordingly.

-   width - \[1-1920\]

Width of the image or video.

-   height - \[1-1080\]

Height of image or video.

#### Focus

-   focus - \[0.0-1.0\]

Based on a survey implementation of many focus measurement algorithms in
["Analysis of focus measure operators for shape from
focus"](https://drive.google.com/file/d/0B6UHr3GQEkQwYnlDY2dKNTdudjg/view)

We selected the OpenCV port of 'LAPV' Variance of Laplacian algorithm
([Pech2000](http://decsai.ugr.es/vip/files/conferences/Autofocusing2000.pdf)).

This kind of algorithms are used in camera auto-focus, and rely on edge
detection since we can detect more edges in a focused image then in a
blurred version of it. Returns the maximum sharpness detected, which is
a pretty good indicator of if a camera is in focus or not. Not
surprisingly, normal values are scene dependent but much less so than
other methods like FFT which has too high of a false positive rate to be
as useful. This is not an easy measure to normalize since we are not
trying to get perfect focus on one same media(camera), but instead we
want to apply it to very different inputs.

#### Color moments

The basis of color moments lays in the assumption that the distribution
of color in an image can be interpreted as a probability distribution.
Probability distributions are characterized by a number of unique
moments (e.g. Normal distributions are differentiated by their mean and
variance). It therefore follows that if the color in an image follows a
certain probability distribution, the moments of that distribution can
then be used as features to identify that image based on color. Color
moments are scaling and rotation invariant, they are also a good feature
to use under changing lighting conditions. We use the first two central
moments of color distribution. They are the Mean and Standard deviation
computed as explained in: ["M. Stricker and M. Orengo Similarity of
color
images."](http://spie.org/Publications/Proceedings/Paper/10.1117/12.205308)

We compute moments for each RGB channel.

Mean - The first color moment can be interpreted as the average color in
the image.

-   red\_moment\_1 - \[0-255\]
-   green\_moment\_1 - \[0-255\]
-   blue\_moment\_1 - \[0-255\]

Standard deviation - The second color moment which is obtained by taking
the square root of the variance of the color distribution.

-   red\_moment\_2 - \[0-255\]
-   green\_moment\_2 - \[0-255\]
-   blue\_moment\_2 - \[0-255\]

#### Color ratio

Color moments are great as a measure to judge similarity between images
or videos, but it's a concept hard to be directly interpreted by a human
user, instead we devised a better feature based on the color average
given by the first moment, the color ratio. For a human is much easier
to understand and use this concept.

-   red\_ratio - \[0.0-1.0\]
-   blue\_ratio - \[0.0-1.0\]
-   green\_ratio - \[0.0-1.0\]

#### Luminance

Luminance is
[arguable](http://therefractedlight.blogspot.pt/2010/06/luminance-is-more-important-than-color.html)the
most important component of color, humans are so much more sensitive to
light than color information. we compute the average luminance of the
media (first luminance moment).

-   luminance - \[0.0-1.0\]

#### edges

Edges may indicate the boundaries of objects in the scene. Detecting
sharp changes in brigthness between each pixel and its surroundings
allow us to detect edges.We start by first applying Gaussian Blur (3x3)
to add some robustness to eventual presence of noise. Afterwards we
apply Prewitt or Sobel kernel convolution to differentiate edge pixels
and give some perspective about the general orientation of edges found
in the scene (horizontal, vertical or diagonal predominance). note: we
tested Prewitt and sobel methods, we intend to experiment also with
canny edge.

-   v\_edges - \[0.0-1.0\].
-   h\_edges - \[0.0-1.0\].
-   d\_edges - \[0.0-1.0\].
-   orientation - \[Horz-0, Vert-1, Diag-2\].

note: This features are being replaced by the edge histogram algorithm +
grid support tool

#### Color diversity

We count groups of different hues present on the H channel of HSV. Edge
composition - it's a measure of edges detected on the image. We compute
the harmonic mean of this two factors.

-   dif\_hues - \[0-360\].

Color diversity is a property related to visual aesthetics. We count
different groups of hues. On the hue histogram (computed from the H
channel of HSV) we count any variation of hue bigger than a certain
threshold.

using the argument -t=1 we turn on a visualization were we can see the
hue histograms computed for each image or frame.

-   simplicity - \[0.0-1.0\]

At the moment this feature relies only on two factors:

#### Object detection

We apply object Detection using Haar feature-based cascade classifiers,
this method was originally proposed by Paul Viola and Michael J. Jones.
in the International Journal of Computer Vision, 57(2):137–154, 2004. We
instantiate two cascade classifiers loading data from existing .xml
classifier files, the first one is used for face detection, and the
second can be used to load any of the other existing classifiers, there
are around 30 different human features classifiers in the folder
(/bin/data/haar), we can find features like eyes, mouth, nose and smile
among others.

Using the argument -t=6 everytime a feature is detected we have acess in
a window to its visualization.

-   faces - images\[0,1\] , videos\[0.0-1.0\]

Faces capture attention, to the detriment of other visual stimuli, in a
visual cueing paradigm, observers responded faster to a target probe
appearing in the location of a face cue than of a competing object cue,
[see](http://jov.arvojournals.org/article.aspx?articleid=2192946). This
measure have a boolean value for images or a double value for videos, in
the first case it signs if it was found or not faces in the image, in
the second it represents the average number of video frames where faces
were detected.

-   faces\_area - \[0.0-1.0\]

Ratio of face area(face bounding box) to full image area. If faces are
found we measure their areas, we consider that preponderancy of
attention faces can arouse is directly related to their visible area.

-   smiles - images\[0,1\] , videos\[0.0-1.0\]

We do smile detection with cascade classifier to compute a smile
measure.It represents average frames where smiles were found, for
videos, and smiles found for images. Depending on the boolean parameter
"insideFace" smiles are detected inside or outside faces.

-   rule\_of\_thirds - \[0.0-1.0\]

The rule of thirds is one of the usual guidelines used to assess quality
of visual image composition, The image is divided in nine equal parts by
four equal spaced lines(the power lines), two oriented horizontally and
the other two vertically, important compositional elements should be
placed along these lines or their intersections. Like in “Evaluating
Visual Aesthetics in Photographic Portraiture,” in Computational
Aesthetics in Graphics, Visualization and Imaging , Annecy, 2012, by D.
V. Shehroz and S. Khan we use a Spatial composition template to score
images according to a variation of the rule of thirds where more power
points were added, the template is in grayscale format, afterwards we
compare face centroids from the previous step of the pipeline with this
template and assign a score ranging from 0-255, this value is afterward
normalized to the \[0.1-1.0\] range.

#### Saliency

Topics related to saliency were adapted from the opencv
[documentation](http://docs.opencv.org/3.0-beta/modules/saliency/doc/saliency.html).

Many computer vision applications may benefit from understanding where
humans focus given a scene. Other than cognitively understanding the way
human perceive images and scenes, finding salient regions and objects in
the images helps various tasks such as speeding up object detection,
object recognition, object tracking and content-aware image editing.

-   static\_saliency\[0.0-1.0\]

Algorithms belonging to this category, exploit different image features
that allow to detect salient objects in a non dynamic scenario. We
experiment with both approaches for static saliency offered by the new
opencv 3.2 Saliency API:

\[SpectralResidual\] - Starting from the principle of natural image
statistics, this method simulate the behavior of pre-attentive visual
search. The algorithm analyzes the log spectrum of each image and obtain
the spectral residual. Then transform the spectral residual to spatial
domain to obtain the saliency map, which suggests the positions of
proto-objects. based on \[Hou, Xiaodi, and Liqing Zhang. “Saliency
detection: A spectral residual approach.” Computer Vision and Pattern
Recognition, 2007. CVPR‘07. IEEE Conference on. IEEE, 2007.\]

\[FineGrained\] - This method calculates saliency based on
center-surround differences. High resolution saliency maps are generated
in real time by using integral images. Based on \[Sebastian Montabone
and Alvaro Soto. Human detection using a mobile platform and novel
features derived from a visual saliency mechanism. In Image and Vision
Computing, Vol. 28 Issue 3, pages 391–402. Elsevier, 2010.

After computing a saliency map with one of the above methods, we
calculate the mean pixel value of this saliency map to give a rough
measure of its strength, the value is normalized dividing it by 255.

Using the argument -t=2 we have acess in a window to the original image,
saliency map and binary map.

-   rank\_sum \[0.0-1.0\]

We experimented to combine some objective measures in a effort to
compute a general objective quality measure.

-   fps - \[1-60\]

Frames per second

#### Optical flow

Optical flow is the pattern of apparent motion of image objects between
two consecutive frames caused by the movement of object or camera. It is
a 2D vector field where each vector is a displacement vector showing the
movement of points from first frame to second. Optical flow works on two
main assumptions: the pixel intensities of an object do not change
between consecutive frames and neighboring pixels have similar motion.
OpenCV provides a algorithm to find dense optical flow. It computes the
optical flow for all the points in the frame. It is based on Gunner
Farneback's algorithm which is explained in "Two-Frame Motion Estimation
Based on Polynomial Expansion" by Gunner Farneback in 2003. For the sake
of performance we compute motion vectors in a 5 by 5 grid, this way we
only have to deal with a fraction of around 1/25 of total pixels present
in the image. After we compute the absolute total flow and signed total
flow per frame used to compute the total video flow and average flow per
frame. We also measure optical flow only on a border of the frame so the
main subject movement dont interfere with our angle measures to increase
accuracy of shake detection.

Using the argument -t=3 we have acess in a window to the motion field
were we can see superimposed the average motion vector computed using
all motion vectors or only the ones inside a border.

-   shackiness \[0.0-1.0\]

We compare the angle between two subsequent motion vectors(computed from
three consecutive video frames), if the angle is above a certain
threshold(90º) we mark the transition between frames as "shaky", then
compute the ratio between this "shaky" transitions and the total frames
of the video.

-   motion\_mag \[0.0-1.0\]

Motion magnitude is the length of the average motion vector, we can use
it as a global measure of change introduced by motion between two frames
of video.

#### Background subtraction

Background subtraction or Foreground Detection is a technique where an
image's foreground is extracted for further processing. It is widely
used for detecting moving objects in videos or cameras. The rationale in
the approach is that of detecting the moving objects from the difference
between the current frame and a reference frame, often called
“background image”, or “background model”. Background subtraction is
generally based on a static background hypothesis which is often not
applicable in real environments. With indoor scenes, reflections or
animated images on screens lead to background changes. In a same way,
due to wind, rain or illumination changes brought by weather, static
backgrounds methods have difficulties with outdoor scenes.

From the video analysis
[section](http://docs.opencv.org/3.0-beta/modules/video/doc/video.html)
of OpenCV, we use the class BackgroundSubtractor, included in the Motion
Analysis and Object Tracking algorithms. The class is only used to
define the common interface for the whole family of
background/foreground segmentation algorithms from wich we use two
specific algorithms that take shadows in account, a shadow is detected
if a pixel is a darker version of the background. See \[Prati, Mikic,
Trivedi and Cucchiarra, Detecting Moving Shadows..., IEEE PAMI,2003\]

\[BackgroundSubtractorKNN\] - The class implements the K-nearest
neigbours background subtraction described in \[ Z.Zivkovic, F. van der
Heijden. “Efficient Adaptive Density Estimation per Image Pixel for the
Task of Background Subtraction”, Pattern Recognition Letters, vol. 27,
no. 7, pages 773-780, 2006\] . Very efficient if number of foreground
pixels is low. Link:
[1](http://www.zoranz.net/Publications/zivkovicPRL2006.pdf) -
[2](http://escholarship.org/uc/item/2kj2g2f7)

\[BackgroundSubtractorMOG2\] - The class implements the Gaussian mixture
model background subtraction described in \[Zivkovic. “Improved adaptive
Gausian mixture model for background subtraction”, International
Conference Pattern Recognition, UK, August, 2004\] -
[Link](http://www.zoranz.net/Publications/zivkovic2004ICPR.pdf), and
Z.Zivkovic, F. van der Heijden. “Efficient Adaptive Density Estimation
per Image Pixel for the Task of Background Subtraction”, Pattern
Recognition Letters, vol. 27, no. 7, pages 773-780, 2006.-
[Link](http://www.zoranz.net/Publications/zivkovicPRL2006.pdf)

Using the argument -t=5 we have acess in a window to the computed
foreground, background and shadows. Using the argument -b we can 0 -
turn background subtraction off, or choose algorithm 1-knn, 2-mog2.

-   fg\_area

Foreground area

-   shadow\_area

From
[3](http://www.hitl.washington.edu/research/knowledge_base/virtual-worlds/EVE/III.A.1.c.DepthCues.html)
When we know the location of a light source and see objects casting
shadows on other objects, we learn that the object shadowing the other
is closer to the light source. As most illumination comes downward we
tend to resolve ambiguities using this information.

-   bg\_area

background area

-   camera\_move

Percentage of frames where foreground area is bigger then 80% of total
area available, this indicates high probability of camera movement
occurance.

-   focus\_diff

Difference of focus between foreground and background. We try to detect
low depth of field, the region of interest should be in sharp focus and
the background blurred, this is a attribute that can boost aesthetic
perceived from media or attention arouse.

#### Texture

-   Gabor

<!-- -->

-   Edge histogram

#### Not implemented

-   Dynamic saliency

<!-- -->

-   Onjectness
