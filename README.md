**Vehicle Detection Project**
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)


[//]: # (Image References)

[image1]: ./test_images/test1.jpg "Test Image1"
[image2]: ./test_images/test2.jpg "Test Image2"
[image3]: ./test_images/test3.jpg "Test Image3"
[image4]: ./test_images/test4.jpg "Test Image4"
[image5]: ./test_images/test5.jpg "Test Image5"
[image6]: ./test_images/test6.jpg "Test Image6"

[image7]: ./output_images/Set2/car_HOG_image.png "Car Hog Image"
[image8]: ./output_images/Set2/car_image.png "Car Image"
[image9]: ./output_images/Set2/notcar_HOG_image.png "Not Car Image"
[image10]: ./output_images/Set2/notcar_image.png "Not Car Hog Image"

[image11]: ./output_images/0.png "sliding window vehicle detect 0"
[image12]: ./output_images/1.png "sliding window vehicle detect 1"
[image13]: ./output_images/2.png "sliding window vehicle detect 2"
[image14]: ./output_images/3.png "sliding window vehicle detect 3"
[image15]: ./output_images/4.png "sliding window vehicle detect 4"
[image16]: ./output_images/5.png "sliding window vehicle detect 5"

[image18]: ./output_images/heatmap1.png "Heat Map of vehicle detect 0"
[image19]: ./output_images/heatmap3.png "Heat Map of vehicle detect 1"
[image20]: ./output_images/heatmap5.png "Heat Map of vehicle detect 2"
[image21]: ./output_images/heatmap7.png "Heat Map of vehicle detect 3"
[image22]: ./output_images/heatmap9.png "Heat Map of vehicle detect 4"
[image23]: ./output_images/heatmap11.png "Heat Map of vehicle detect 5"


[ProjectOutput]: ./project_output_final.mp4 "Output Video final"
[video25]: ./test_Output.mp4 "Output Video test"


---

The goals / steps of this project are the following:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Optionally, you can also apply a color transform and append binned color features, as well as histograms of color, to your HOG feature vector. 
* Note: for those first two steps don't forget to normalize your features and randomize a selection for training and testing.
* Implement a sliding-window technique and use your trained classifier to search for vehicles in images.
* Run your pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.


## Histogram of Oriented Gradients (HOG)

HOG features are extracted using the `hog()` from skimage.feature import hog. The function is used in a wrapper function `get_hog_features()` in cell no 3 of `Vehicle_Detection.ipynb` notebook. 

The scikit-image `hog()` function takes in a single color channel or grayscaled image as input, as well as various parameters. These parameters include orientations, pixels_per_cell and cells_per_block.

The number of orientations is specified as an integer, and represents the number of orientation bins that the gradient information will be split up into in the histogram. Typical values are between 6 and 12 bins.

The pixels_per_cell parameter specifies the cell size over which each gradient histogram is computed. This paramater is passed as a 2-tuple so you could have different cell sizes in x and y, but cells are commonly chosen to be square.

The cells_per_block parameter is also passed as a 2-tuple, and specifies the local area over which the histogram counts in a given cell will be normalized. Block normalization is not necessarily required, but generally leads to a more robust feature set.

There is another optional power law or "gamma" normalization scheme set by the flag transform_sqrt. This type of normalization may help reduce the effects of shadows or other illumination variation, but will cause an error if your image contains negative values (because it's taking the square root of image values).

I started by reading in all the `vehicle` and `non-vehicle` images.  Here is an example of one of each of the `vehicle` and `non-vehicle` classes:

Car input image and the output after hog features extraction is as shown below.

![alt text][image8]
![alt text][image7]

Not Car input image and the output after hog feature extraction is as shown below.

![alt text][image10]
![alt text][image9]

After several round of trial and error, the following are the parameters chosen for HOG, Spatial Bins and Color Histograms:-

    # Define feature parameter
    color_space = 'YCrCb' # Can be RGB,HSV,LUV,HLS,YUV, YCrCb
    orient = 9
    pix_per_cell =8
    cell_per_block =2
    hog_channel = 'ALL' #can be 0,1,2, or "ALL"
    spatial_size = (32,32) # spatial binning dimenions
    hist_bins = 32 # number of histogram bins
    spatial_feat = True #spatial features on/off
    hist_feat = True # Histogram features on/off
    hog_feat = True # HOG features on/off
    
  The parameters can be found in **cell no 5 of Veicle_Detection.ipynb** 
 
 #### Training model to identify Car and not car for the images.
   The data set given by the udacity is used to train the model to identify car and not car. classifier was trained using **SVC** function **sklearn.svm**. LinearSVC gave an increased accuracy. Implementation is present in **cell no 5 of Vehicle_Detection.ipynb**
 The trained model gave an accuracy of **99.38%**
 
 ## Sliding window
 
 Sliding window function `slide_window()`and its supporting function `search_windows()` can be found in **cell no 5 of Vehicle_Detection.ipynb** The `slide_window()` slide over the entire region of interest and returns the list of windows. 
 
 The window list is passed to `search_window()` to identify if the car is present or not. Implementation can be seen in the piple in **cell no 6 of Vehicle_Detection.ipynb**.  Based on the trail and error following window parameters were slected.
 
      y_start_stop = [400,656]
      x_start_stop = [640,1280]
      xy_window = (96,96)
      overlap=(0.4,0.4)
      
  The output of the `search_windows()` are hot_windows. The windows are returned hot if vehicle is predected by the SVC classifier. This demo imprementation can see in **cell no 8 pf Vehicel_Detection.ipynb** 
  The detected cars by sliding window technique and the heatmap added is as shown below.

![alt text][image18]

![alt text][image19]

The below line in the **cell no 5 of Vehicle_Detection.ipynb** is used to generate heatmap based on the vehicle detectio from sliding window and search window techniques explained earlier.

    heatmap[ytop_draw+ystart:ytop_draw+win_draw+ystart,xbox_left:xbox_left+win_draw] += 1
    
Blue Boundaries around the heatmap is added using `draw_labeled_bboxes()` this function can be found in **cell no 10 of Vehicle_Detection.ipynb**

![alt text][image11]

![alt text][image12]

False positives from the image are removed by defining min and max co-oridinates region of interest in x and y. All the boxes ioutseide the region of interest are filtered out. Also the number of windows in sliding window is removed by the defined ROI.

## Video Implementaion

The output video post processing using the pipline is as in the below link: 

[ProjectOutput]

Youtube link :  [Video_Link][https://youtu.be/0HRjKKaxxJQ]

As explained earlier, False positives were removed using defined ROI over which sliding window technique was restricted to. The observed false positives were the vehicles coming from the opposite side. so X min and max were defined to view only vehicles from the right hand side and not left hand side. Implementation can be seen in `draw_labeled_boxes()` on **cell no 10 of Vehicle_Detection.ipynb**. Heatmaps obtained from previous frame is given weightage of **0.4** and heatmaps from current frame are given weightage of **0.6**. This is the way in which we decide the heatmap for current frame. These two values were obtained experimentally. 

I could not get the generalized approch of removing false positives. Had to customize for the current project video. The pipeline will fail if vehicles apprear on both the side of the view. Need to use lane detection method to identify the position of the own vehicle and also other vehicles from the lane. Need intelligence to identify if vehicle is moving away or towards the vehicle. 
Use of infomation from previous frames will be very helpful.

