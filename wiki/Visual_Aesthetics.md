---
title: Visual Aesthetics
permalink: wiki/Visual_Aesthetics/
layout: wiki
---

Visual feature extraction tool
------------------------------

A command line utility that can be used to generate metadata for visual
quality assessment, it relies on OpenCV 3.2 library of algorithms to
compute features that describe images and videos in respect to visual
properties carefully selected from state-of-the-art literature. An
extensive review and testing was made to find a group of visual features
good for the task of visual discrimination. A top-down approach for
extraction results in a very compact feature vector. A graphical
interface (demo available
[here](https://drive.google.com/file/d/0Bzelhrdw43rCc0JkOGdSNnYtclE/view?usp=sharing))
was used to test overall usability of the features with good results. A
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
