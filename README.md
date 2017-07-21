**Traffic Sign Recognition** 

---

[//]: # (Image References)

[image1]: ./report/train-dist.png "distribution of training images"
[image20]: ./report/color.png "Color"
[image21]: ./report/gray.png "Gray"
[image4]: ./web/0.jpg "Traffic Sign 1"
[image5]: ./web/1.jpg "Traffic Sign 2"
[image6]: ./web/2.jpg "Traffic Sign 3"
[image7]: ./web/3.jpg "Traffic Sign 4"
[image8]: ./web/4.jpg "Traffic Sign 5"

---

###Data Set Summary & Exploration

####1. Dataset: [German Traffic Sign Dataset](http://benchmark.ini.rub.de/?section=gtsrb&subsection=dataset)

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is originally (32, 32, 3). (32, 32, 1) Grayscaled.
* The number of unique classes/labels in the data set is 43

####2. Distribution of training data

![alt text][image1]

###Design and Test a Model Architecture

####1. Images are convered to grayscale. Because color does not help to differentiate the traffic sign.

![alt text][image20]
![alt text][image21]

#### Possible improvements: normalize the image, generate additional.


####2. Final model architecture

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Gray image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 					|
| Convolution 1x1	    | 1x1 stride,  outputs 14x14x6 					|
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 10x10x16 	|
| Convolution 1x1	    | 1x1 stride,  outputs 10x10x16 				|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x16 					|
| Fully connected		| 5x5x16 = 400        							|
| Fully connected		| 120        									|
| Dropout				| 0.6       									|
| Fully connected		| 84        									|
| Dropout				| 0.6       									|
| Fully connected		| 43        									|
| Softmax				|       										|

To train the model, I used TensorFlow AdamOptimizer with learning rate 0.001, 20 Epoch , 128 batch size

It is bacisly LenNet architecture. This model has..... I added two 1x1 convolution layers and dropouts.

My final model results were:
* training set accuracy of %99.7
* validation set accuracy of %95.8
* test set accuracy of %93.8

I also designed a inseption module you can find it in the code but, I could not test it.

###Test a Model on New Images

####1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]

####2.

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Bumpy road     		| Bumpy road  									| 
| Stop     				| Stop											|
| No entry				| No entry										|
| No passing	      	| No passing					 				|
| Priority road			| Priority road     							|


####3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a stop sign (probability of 0.6), and the image does contain a stop sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .52         			| Bumpy road     								| 
| .16     				| Stop 											|
| .68					| No entry										|
| .53	      			| No passing					 				|
| .55				    | Priority road	      							|

