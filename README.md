# Project: Build a Traffic Sign Recognition Program
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

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

[random_traffic_signs]: ./traffic-signs-data/random_images_with_labels.png "Random images"
[distribution_of_traffic_sign_types]: ./traffic-signs-data/distribution_of_labels.png "Distribution of labels"
[distribution_of_traffic_sign_types_augmented]: ./traffic-signs-data/distribution_of_traffic_sign_types_augmented.png "Distribution of labels augmented"
[grayscale]: ./traffic-signs-data/grayscale.png "Grayscale"
[web_images]: ./traffic-signs-data/web_images.png "Web Traffic Signs"
[softmax]: ./traffic-signs-data/softmax.png "Softmax of Web traffic signs"
[conv_1]: ./traffic-signs-data/conv_1.png "Feature maps of the first convolutional layer"

## Project Rubric
Link to the project rubic: [rubric points](https://review.udacity.com/#!/rubrics/481/view).

---

### Data Set Summary & Exploration

#### 1. Basic summary of the data set

I used the numpy library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32x32x3 pixels
* The number of unique classes/labels in the data set is 43

#### 2. Exploratory visualization of the dataset

Here is an exploratory visualization of the data set. The first image includes 8 random traffic signs from the training set along with their respective labels and the sign name. The second image shows the distribution of the 43 traffic sign types for both the training and validation set.

![random_traffic_signs][random_traffic_signs]

![distribution_of_traffic_sign_types][distribution_of_traffic_sign_types]

### Design and Test a Model Architecture

#### 1. Image data preprocessing

Since the dataset was not uniformly distributed, I chose to augment it with synthetic data created from the least 20 frequent labels. For each of these labels, I took a random image as a base image and added random noise (+-2 pixels), 600 times. Therefore, I came up with a synthetic dataset of 12000 images. The following image, shows the resulting distribution after applying this step:

![distribution_of_traffic_sign_types_augmented][distribution_of_traffic_sign_types_augmented]

Then, I decided to convert the images to grayscale as it gave better results than using the rgb channels. Exploring other channels transformations (e.g., HSV) might be an alternative for future work. Here is an example of 8 random traffic sign images after grayscaling.

![grayscale][grayscale]

As the last step, I centred the data around zero to achieve better performance. To do so, I standardised the image data by subtracting the mean and dividing by the standard deviation.


#### 2. Final model architecture

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Grayscale image   					| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, same padding,  outputs 14x14x6	|
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 10x10x16 	|
| RELU					|												|
| Max pooling			| 2x2 stride, same padding,   outputs 5x5x16	|
| Flattening			| Output 400									|
| Fully connected 1		| Output 120									|
| RELU					|												|
| Fully connected 2		| Output 84										|
| RELU					|												|
| Dropout				|												|
| Fully connected 3		| Output 43										|
|						|												|
 


#### 3. Training the model

To train the model, I used the following parameters:
- Batch size: 128
- Number of epochs: 15
- Learning rate: 0.001
- Dropout keep probability: 0.75
- Optimizer: Adam

#### 4. Finding a solution and getting the validation set accuracy to be at least 0.93

The LeNet architecture has been taken as a base architecture for its well-recognized performance on image classification tasks. Then, a dropout layer has been added to avoid overfitting.  

My final model results, which can be observed in the "Train, Validate and Test the Model" section, were:
* training set accuracy of 0.998
* validation set accuracy of 0.943


### Test a Model on New Images
#### 1. Choose five German traffic signs found on the web and provide them in the report.

Here are five German traffic signs that I found on the web:

![web_images][web_images]

The second and fourth images might be more challenging to classify because of their respective darkness.

#### 2. Model's predictions on these new traffic signs

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Speed limit (30km/h)	| Stop sign   									| 
| End of speed limit (80km/h)| U-turn 										|
| Vehicles over 3.5 metric tons prohibited			| Vehicles over 3.5 metric tons prohibited											|
| Righ-of-way at the next intersection		| Righ-of-way at the next intersection					 				|
| Double curve			| Double curve							|


The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100% on this small test set.

#### 3. Top 5 softmax probabilities for each image along with the sign type of each probability.

The code for making predictions on my final model can be found in the "Output Top 5 Softmax Probabilities For Each Image Found on the Web" section of the Ipython notebook.

As it can be seen in the image below, the model is at least 99.9% certain to select the right label on all of these predictions.

![softmax][softmax]

### Visualizing the Neural Network
The following image shows the resulting feature maps of the first convolutional layer. It can be observed that for this layer, the network used the image's edge and shape to make classifications.

![conv_1][conv_1]