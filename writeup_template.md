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
[image9]: ./web/5.jpg "Traffic Sign 6"
[image10]: ./web/6.jpg "Traffic Sign 7"

---

###Data Set Summary & Exploration

####1. Dataset: [German Traffic Sign Dataset](http://benchmark.ini.rub.de/?section=gtsrb&subsection=dataset)

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is originally (32, 32, 3). (32, 32, 1) Gray.
* The number of unique classes/labels in the data set is 43

####2. Distribution of training data

![alt text][image1]

###Design and Test a Model Architecture

####1. Images are converted to grayscale. Because color does not help to differentiate the traffic sign.

![alt text][image20]
![alt text][image21]
After that operation pixel values are normalized ((X/255)-0.5) because.

#### Possible improvements: Generating artificial image and adding some noise.


####2. Final model architecture

My final model consisted of the following layers:

| Layer         		    |     Description	        					            |
|:---------------------:|:---------------------------------------------:|
| Input         		    | 32x32x1 Gray image   							            |
| Convolution 3x3     	| 1x1 stride, valid padding, outputs 30x30x8 	  |
| ELU					          |												                        |
| Max pooling	      	  | 2x2 stride,  outputs 15x15x8 					        |
| Convolution 1x1	      | 1x1 stride,  outputs 15x15x8 					        |
| Convolution 3x3     	| 1x1 stride, valid padding, outputs 13x13x16 	|
| ELU					          |												                        |
| Max pooling	      	  | 2x2 stride,  outputs 6x6x16 					        |
| Convolution 1x1	      | 1x1 stride,  outputs 6x6x16 				          |
| Fully connected		    | 6x6x16 = 576        							            |
| Fully connected		    | 120        									                  |
| Dropout				        | 0.6       									                  |
| Fully connected		    | 84        									                  |
| Dropout				        | 0.6       							                  		|
| Fully connected		    | 43        							                   		|
| Softmax				        |       								                     		|

To train the model, I used TensorFlow AdamOptimizer with learning rate 0.001, 20 Epoch , 128 batch size

It is bacisly LenNet architecture. I reduced filter sizes from 5x5 to 3x3 and I added two 1x1 convolution layers and dropouts.

Basic LeNet-5 results are good for classify traffic signs: (learning rate 0.001, 20 Epoch , 128 batch size)
* training set accuracy of %99.6
* validation set accuracy of %93.0
* test set accuracy of %92.2

My final model results were:
* training set accuracy of %99.8
* validation set accuracy of %94.5
* test set accuracy of %92.4
Changes have allowed us to get better results.

I also designed a inseption module you can find it in the code but, I could not test it.

###Test a Model on New Images

####1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6]
![alt text][image7] ![alt text][image8] ![alt text][image9]
![alt text][image10]

####2.

Here are the results of the prediction:

| Image			            |     Prediction	        					            |
|:---------------------:|:---------------------------------------------:|
| Bumpy road     		    | Bumpy road  									                |
| Stop     				      | Stop											                    |
| No entry				      | No entry										                  |
| No passing	      	  | No passing					 				                  |
| Priority road			    | Priority road     							              |
| Ice/snow	      	    | End of no passing by vehicles over 3.5 metric tons|
| Children crossing		  | Right-of-way at the next intersection    			|


####3. The top 5 softmax probabilities for each image along with the sign type of each probability.


| Probability         	|     Prediction	        					            |
|:---------------------:|:---------------------------------------------:|
| %99        			      | Bumpy road     								                |
| %99     				      | Stop 											                    |
| %100				          | No entry										                  |
| %100      			      | No passing					 				                  |
| %100			            | Priority road	      							            |
| %82        			      | End of no passing by vehicles over 3.5 metric tons|
| %88   		            | Right-of-way at the next intersection    			|

#### When we want to classify clearly visible traffic signs, the outcome is very likely to predict correctly. But weather conditions such as snow and fog reduce the success rate and cause misclassification.
