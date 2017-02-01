---
title: Image Annotation
permalink: wiki/Image_Annotation/
layout: wiki
---

Image Classification
--------------------

### ImageNET Concepts - Convolutional Neural Networks

A tool is available in the cluster to classify images with ImageNET
concepts (a total of 1000 concepts - List available
[here](http://image-net.org/challenges/LSVRC/2014/browse-synsets)). The
current version performs classification using the state-of-the-art
GoogleNet CNN, which won the ILSVRC 2014 competition with 6.65% Top-5
error.

Each image is classified within the 1000 concepts. For each concept, a
probability score is assigned thus, the tool outputs the top N concepts
(from the 1000) with highest probability. Namely, for each image it
outputs N pairs \<concept name, probability\>.

Features:

-   Performs classification in batch (all images on a given folder) or
    single-image only.
-   Supports .jpg and .png images.
-   Output can be stored in a nice JSON file.
-   The number of concepts N to output can be specified.

Support for other CNN networks will be added later. If you find any bug
or if you have any suggestion to improve the tool, please send an email
to: df.semedo\_\_at\_\_campus.fct.unl.pt

To run the tool:

`$ concepts_extraction --help`  
` usage: concepts_extractor.py [-h] [-n [NUM_CONCEPTS]] [-p [INPUT_PATH]]`  
`                      [-i [SINGLE_IMG_PATH]] [-j [OUT_JSON]]`  
` CNN ImageNet Concept extractor.`  
` - Current version only supports GoogleNet (Inception) network.`  
` - Supports JPG and PNG images (w/ 3 channels).`  
  
` Author: David Semedo (df.semedo__at__campus.fct.unl.pt )`  
  
` optional arguments:`  
`  -h, --help            show this help message and exit`  
`  -n [NUM_CONCEPTS], --num_concepts [NUM_CONCEPTS]`  
`                       Number of concepts to retrieve.`  
`  -p [INPUT_PATH], --input_path [INPUT_PATH]`  
`                       Path with target images.`  
`  -i [SINGLE_IMG_PATH], --image [SINGLE_IMG_PATH]`  
`                       Path of a single target image.`  
`  -j [OUT_JSON], --out_json [OUT_JSON]`  
`                       Store output in a JSON file.`

To extract 20 concepts per image, from a folder <folder> and store the
output in a JSON file \<out.json\>:

`$ concepts_extraction -n 20 -p `<folder>` -j <out.json>`
