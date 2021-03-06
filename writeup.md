#**Traffic Sign Recognition** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # "Image References"

[image1]: ./examples/classCount.png "Count of Each Sign"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./examples/00000.png "Traffic Sign 1"
[image5]: ./examples/00001.png "Traffic Sign 2"
[image6]: ./examples/00002.png "Traffic Sign 3"
[image7]: ./examples/00003.png "Traffic Sign 4"
[image8]: ./examples/00004.png "Traffic Sign 5"

## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
###Writeup / README

####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/karabC/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

###Data Set Summary & Exploration

####1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32 x 32 x 3 (RGB)
* The number of unique classes/labels in the data set(Training Set) is 43

####2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. First, I listed out the Classes and the Sign Name. Then I randomly print some image to get some knowledge about the Class name and the Image data. Also, for each classes, I printed out a small set of image to have a look.

To understand the distribution of class better, I have done a aggregated count by the Class with the Sign Name with the help of panda. 

![alt text][image1]


###Design and Test a Model Architecture

####1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

To preprocessed the image data, I have applied the normalization to the data. I have also applied grayscale yet the accuracy is no better than the non-grayscale one.


####2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

|      Layer      |               Description                |
| :-------------: | :--------------------------------------: |
|      Input      |            32x32x3 RGB image             |
| Convolution 5x5 | 5x5 stride, valid padding, outputs 32x32x43 |
|   Max pooling   |       2x2 stride, outputs 14x14x43       |
|      RELU       |                                          |
| Convolution 5x5 | 5x5 stride, valid padding, outputs 10x10x83 |
|   Max pooling   |        2x2 stride, outputs 5x5x83        |
|      RELU       |                                          |
| Fully connected |          Input:2075, Output:400          |
|      RELU       |                                          |
|     Dropout     |           80% keep probablity            |
| Fully connected |          Input:400, Output:200           |
|      RELU       |                                          |
|     Dropout     |           80% keep probablity            |
| Fully connected |           Input:200, Output:43           |
|     Softmax     |                                          |
|                 |                                          |
|                 |                                          |



####3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used the Adam Optimizer, with Epochs 15 and Batch Size 128. The learning rate is 0.01 and the probablity of keeping in dropout is 0.8.

####4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 99.4%
* validation set accuracy of 94.4% 
* test set accuracy of 92.9%



If an iterative approach was chosen:

* What was the first architecture that was tried and why was it chosen?

  My first architecture is based on the LeNet, with increased convolution layer's depth. As it worked nice in the MNIST problem, which is also turning the image data to the symbolic classes.

* What were some problems with the initial architecture?

  The training accuracy is low and underfitting. Increased convolution layer to boost up the accuracy.

* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.

  However, after the increase of the depth. The model is highly overfit. I have further applied Max Pooling and Drop out to prevent overfitting

* Which parameters were tuned? How were they adjusted and why?

  I have tunned the Dropout probablity for finding a suitable probability. As the model is trained with decreased training error but increasing validation error, it looks like overfitting occured.

* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?

One of the important design is CNN, which allow the image pixels to be consider in group. Another technique is the dropout, which boosts the model's robutness and help in solving overfitting problem
  ​

###Test a Model on New Images

####1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]


####2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

|                  Image                   |  Prediction   |
| :--------------------------------------: | :-----------: |
| Vehicles over 3.5 metric tons prohibited |   Vehicles over 3.5 metric tons prohibited   |
|                  Speed limit (30km/h)                |    Speed limit (30km/h)     |
|                  Keep right                   |     Keep right     |
|                 Turn right ahead             |  Turn right ahead   |
|              Right-of-way at the next intersection               | Right-of-way at the next intersection |


The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%.

####3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 18 - 22 cell of the Ipython notebook.
For all five images, the prediction are pretty sure of their oringinal classes.


| Probability |  Prediction   |
| :---------: | :-----------: |
|     1.00000000e+00     |   Stop sign   |
|     6.69590662e-16     |    End of no passing by vehicles over 3.5 metric ...     |
|     8.84415614e-21     |     Speed limit (100km/h)     |
|     1.60674987e-21     |  Speed limit (80km/h)  |
|     5.76508486e-22     | End of no passing |

For the second image, 

| Probability |  Prediction   |
| :---------: | :-----------: |
| 1.00000000e+00 | Speed limit (30km/h) |
| 6.66715438e-09 | Ahead only |
| 1.18389187e-09 | Stop |
| 9.33583877e-10 | Speed limit (80km/h) |
| 2.19198146e-10 | Road narrows on the right |

For the third image, 

| Probability |  Prediction   |
| :---------: | :-----------: |
| 1.00000000e+00 | Keep right |
| 0 | Speed limit (20km/h) |
| 0 | Speed limit (50km/h) |
| 0	| Speed limit (60km/h) |
| 0	| Speed limit (70km/h) |


For the forth image, 

| Probability |  Prediction   |
| :---------: | :-----------: |
| 1.00000000e+00 | Turn right ahead |
| 1.86530682e-13 | Turn left ahead |
| 4.91353556e-18 | Keep left |
| 5.96932769e-19 | Ahead only |
| 2.86005193e-20 | Go straight or left |


For the fifth image, 

| Probability |  Prediction   |
| :---------: | :-----------: |
| 1.00000000e+00 | Right-of-way at the next intersection | 
| 1.12722809e-09 | Pedestrians | 
| 1.93478955e-10 | Double curve | 
| 4.47416660e-14 | Beware of ice/snow | 
| 5.16073458e-15 | Dangerous curve to the right | 


