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


[//]: # (Image References)

[image1]: ./examples/hist.png "Augmented Image"
[image3]: ./examples/augmentation.jpg "Augmented Image"
[image4]: ./test_images/test4.jpg "Traffic Sign 1"
[image5]: ./test_images/test11.jpg "Traffic Sign 2"
[image6]: ./test_images/test8.jpg "Traffic Sign 3"
[image7]: ./test_images/test10.jpg "Traffic Sign 4"
[image8]: ./test_images/test5.jpg "Traffic Sign 5"

## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
###Writeup / README

####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/root221/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

###Data Set Summary & Exploration

####1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799.
* The size of the validation set is 4410.
* The size of test set is 12630.
* The shape of a traffic sign image is (32, 32, 3).
* The number of unique classes/labels in the data set is 43.

####2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing the distribution of classes in the test set.

![alt text][image1]

###Design and Test a Model Architecture

####1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

I didn't convert the images to grayscale because I thought that color would be a important for classifying traffic sign.

I didn't normalized the image data because the performance was bad when I normalized.(why?)

I decided to generate additional data because it made the classifier more robust for new images from the Internet.

To add more data to the the data set, I used keras data augmentation. Also, every class has the same amount of data.

Here is an example of an original image and an augmented image:

![alt text][image3]




####2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x30 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, outputs 14x14x30 				    |
| Convolution 5x5	    | 1x1 stride, valid padding, outputs 10x10x60   |
| RELU           		|        									    |
| Max pooling			| 2x2 stride, outputs 5x5x60					|
| Fully connected		| inputs 1500, outputs 240						|
| RELU           		|        									    |
| Fully connected		| inputs 240, outputs 84						|
| RELU           		|        									    |
| Fully connected       | inputs 84, outputs 10       				    |



####3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an AdamOptimizer, and the batch size is 128, the number of epochs is 220, the learning rate is 0.0005. 

####4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.998.
* validation set accuracy of 0.958. 
* test set accuracy of 0.951.

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?

    The first architecture was Lenet since it worked pretty well on mnist dataset.

* What were some problems with the initial architecture?

    The performance was not good enough.

* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.

    Made the convolution layer more deeper,the first cnn layer depth was 30, and the second cnn layer depth was 60.

* Which parameters were tuned? How were they adjusted and why? 

    I modified the sigma to 0.05, but I didn't know why. The performance just became better.

* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?

    I used convolution layer since cnn work pretty well with images. 

###Test a Model on New Images

####1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]

The fifth image might be difficult to classify because the frame was a red triangle and the frame of the "Road work" sign was also red triangle. The sign with red triangle frame seems to be easily wrong classified.

####2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Road work      		| Road work   									| 
| Yield     			| Yield 										|
| Ahead only			| Ahead only									|
| Priority road	      	| Priority road					 				|
| Road narrows on the right	 | Road work     							|


The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%. The accuracy was not very good compared with the test set.

####3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)


For the first image, the model is relatively sure that this is a Road work sign (probability of 1), and the image does contain a Road work sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
|  1          			| Road work   									| 
|  0     				| Speed limit (20km/h)   					    |
|  0					| Speed limit (30km/h)						    |
|  0	      			| Speed limit (50km/h)				 			|
|  0				    | Speed limit (60km/h)    						|


For the second image, the model is relatively sure that this is a Yield sign (probability of 1), and the image does contain a Yield sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
|  1          			| Yield   									    | 
|  0     				| Speed limit (20km/h)   					    |
|  0					| Speed limit (30km/h)						    |
|  0	      			| Speed limit (50km/h)				 			|
|  0				    | Speed limit (60km/h)    						|


For the third image, the model is relatively sure that this is a Ahead only sign (probability of 1), and the image does contain a Ahead only sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
|  1          			| Ahead only   									| 
|  0     				| Speed limit (20km/h)   					    |
|  0					| Speed limit (30km/h)						    |
|  0	      			| Speed limit (50km/h)				 			|
|  0				    | Speed limit (60km/h)    						|


For the fourth image, the model is relatively sure that this is a Priority road sign (probability of 1), and the image does contain a Priority road sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
|  1          			| Priority road   							    | 
|  0     				| Speed limit (20km/h)   					    |
|  0					| Speed limit (30km/h)						    |
|  0	      			| Speed limit (50km/h)				 			|
|  0				    | Speed limit (60km/h)    						|


For the fifth image, the model is relatively sure that this is a Road work sign (probability of 1), however, the image contain a  Road narrows on the right sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
|  1          			| Road work   									| 
|  3.00268488e-29     	| Double curve   					            |
|  0				    | Speed limit (20km/h)    						|
|  0					| Speed limit (30km/h)						    |
|  0	      			| Speed limit (50km/h)				 			|




### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
####1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?


