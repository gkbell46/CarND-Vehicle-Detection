# Vehicle Detection
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)


In this project, your goal is to write a software pipeline to detect vehicles in a video (start with the test_video.mp4 and later implement on full project_video.mp4), but the main output or product we want you to create is a detailed writeup of the project.  Check out the [writeup template](https://github.com/udacity/CarND-Vehicle-Detection/blob/master/writeup_template.md) for this project and use it as a starting point for creating your own writeup.  

Creating a great writeup:
---
A great writeup should include the rubric points as well as your description of how you addressed each point.  You should include a detailed description of the code used in each step (with line-number references and code snippets where necessary), and links to other supporting documents or external references.  You should include images in your writeup to demonstrate how your code works with examples.  

All that said, please be concise!  We're not looking for you to write a book here, just a brief description of how you passed each rubric point, and references to the relevant code :). 

You can submit your writeup in markdown or use another method and submit a pdf instead.

The Project
---

The goals / steps of this project are the following:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Optionally, you can also apply a color transform and append binned color features, as well as histograms of color, to your HOG feature vector. 
* Note: for those first two steps don't forget to normalize your features and randomize a selection for training and testing.
* Implement a sliding-window technique and use your trained classifier to search for vehicles in images.
* Run your pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.

[//]: # (Image References)

[image1]: ./test_images/test1.jpg "Test Image1"
[image2]: ./test_images/test2.jpg "Test Image2"
[image3]: ./test_images/test3.jpg "Test Image3"
[image4]: ./test_images/test4.jpg "Test Image4"
[image5]: ./test_images/test5.jpg "Test Image5"
[image6]: ./test_images/test6.jpg "Test Image6"

[image7]: ./output_images/Set2/car_HOG_image.png "Car Hog Image"
![alt text][image8]: ./output_images/Set2/car_image.png "Car Image"
![alt text][image9]: ./output_images/Set2/notcar_HOG_image.png "Not Car Image"
![alt text][image10]: ./output_images/Set2/notcar_image.png "Not Car Hog Image"

[image10]: ./output_images/Set2/notcar_image.png "Car Hog Image"
[image10]: ./output_images/Set2/notcar_image.png "Car Hog Image"
[image10]: ./output_images/Set2/notcar_image.png "Car Hog Image"
[image10]: ./output_images/Set2/notcar_image.png "Car Hog Image"
[image10]: ./output_images/Set2/notcar_image.png "Car Hog Image"
[image10]: ./output_images/Set2/notcar_image.png "Car Hog Image"
[image10]: ./output_images/Set2/notcar_image.png "Car Hog Image"




[video10]: ./project_output_final.mp4 "Video"

Here are links to the labeled data for [vehicle](https://s3.amazonaws.com/udacity-sdc/Vehicle_Tracking/vehicles.zip) and [non-vehicle](https://s3.amazonaws.com/udacity-sdc/Vehicle_Tracking/non-vehicles.zip) examples to train your classifier.  These example images come from a combination of the [GTI vehicle image database](http://www.gti.ssr.upm.es/data/Vehicle_database.html), the [KITTI vision benchmark suite](http://www.cvlibs.net/datasets/kitti/), and examples extracted from the project video itself.   You are welcome and encouraged to take advantage of the recently released [Udacity labeled dataset](https://github.com/udacity/self-driving-car/tree/master/annotations) to augment your training data.  

Some example images for testing your pipeline on single frames are located in the `test_images` folder.  To help the reviewer examine your work, please save examples of the output from each stage of your pipeline in the folder called `ouput_images`, and include them in your writeup for the project by describing what each image shows.    The video called `project_video.mp4` is the video your pipeline should work well on.  

**As an optional challenge** Once you have a working pipeline for vehicle detection, add in your lane-finding algorithm from the last project to do simultaneous lane-finding and vehicle detection!

**If you're feeling ambitious** (also totally optional though), don't stop there!  We encourage you to go out and take video of your own, and show us how you would implement this project on a new video!
