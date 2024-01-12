[[Difference between the three]]

Firstly, we should understand, that this models solve detection task in CV.
Generally, Detection task is
![[Pasted image 20240110003527.png]]
So, here we get image as an input and give an output of form [class label, confidence, BoundingBox]

There are two object Detection Challenges:
![[Pasted image 20240110004105.png]]

Let's try to create detection model from scratch:
Firstly, let's assume, that we have just one object in the image to detect. What can we do?

We can create simple CNN Network, which will be predict labels and Bounding Boxes for object. And then we can combine this losses (Softmax Loss and L2) to optimize weights of our model.

![[Pasted image 20240110012247.png]]

Ok. But what, if we will have more than one object in our image?
Here, we can create windows to slice through the image. And for every window we can use the model, which we consider above to predict labels and bboxes.

![[Pasted image 20240110012632.png]]

Here is another problem - we have different objects with different sizes. How to choose correct windows, because we can't choose all possible ones, as they are infinite. How to choose those windows?

![[Pasted image 20240110012843.png]]

![[Pasted image 20240110012853.png]]

There are many different approaches, how to choose windows for detection

![[Pasted image 20240110013057.png]]

But the most popular one is Selective Search. We will not go into details about this approach, let's just think, that we can somehow choose optimal windows

#### R-CNN

![[Pasted image 20240110131646.png]]

But there is some question: how to solve bbox regression? There is a problem, because predifined bbox can be not similiar to the ground true bbox.

We can predict not  coordinates of bboxes, but transformation.
(tx, ty, tn, tw)

![[Pasted image 20240110133726.png]]

Some additional info
	Here's a [[step-by-step explanation of how R-CNN]] works:
	1. **Region Proposals**: The first step in R-CNN is to generate region proposals. This is done using a technique known as [[Selective search]], which divides the image into small regions and proposes regions that likely contain an object. Approximately 2000 region proposals are generated [1](https://www.geeksforgeeks.org/r-cnn-region-based-cnns/amp/).
	2. **Feature Extraction**: Next, these region proposals are fed into a CNN to extract features. The CNN consists of several convolutional layers followed by pooling layers. The purpose of this step is to convert the raw pixel values of the image into a set of high-level features that capture the important characteristics of the objects in the image [2](https://blog.roboflow.com/what-is-r-cnn/amp/).
	3. **Classification**: Once the features have been extracted, they are passed to a linear [[Support Vector Machine (SVM)]] to classify whether each region proposal contains an object and what class of object it is [1](https://www.geeksforgeeks.org/r-cnn-region-based-cnns/amp/).
	4. **Bounding Box Regression**: Finally, a separate regression model is trained to predict the exact location of the object within the region proposal. This is done by predicting the coordinates of the bounding box around the object [1](https://www.geeksforgeeks.org/r-cnn-region-based-cnns/amp/).
	Despite its effectiveness, R-CNN has some limitations. Because it uses selective search to generate region proposals, the quality of these proposals can vary, leading to poor object detection. Additionally, R-CNN is computationally expensive due to the large number of region proposals and the need to run the entire CNN on each one. These drawbacks led to the development of faster and more efficient versions of R-CNN, such as Fast R-CNN and Faster R-CNN [1](https://www.geeksforgeeks.org/r-cnn-region-based-cnns/amp/), [2](https://blog.roboflow.com/what-is-r-cnn/amp/).
	![[Pasted image 20240112145045.png]]

Let's see steps of training R-CNN models

![[Pasted image 20240110135047.png]]

![[Pasted image 20240110135217.png]]

![[Pasted image 20240110135427.png]]

![[Pasted image 20240110135455.png]]

![[Pasted image 20240110135529.png]]

Let's see the results of R-CNN

![[Pasted image 20240110135909.png]]

But this model has problems

![[Pasted image 20240110135957.png]]

You can see that it has bad performance, it's very slow model, because of the first point above

## Fast R-CNN
![[Pasted image 20240110140403.png]]
Our feature map contains the special structure, so we don't loose information about location of our features and objects.

![[Pasted image 20240110142230.png]]

![[Pasted image 20240110170410.png]]

![[Pasted image 20240110170424.png]]

![[Pasted image 20240110170459.png]]

![[Pasted image 20240110170522.png]]

![[Pasted image 20240110170536.png]]

And as a result, this approach perform much better than R-CNN

![[Pasted image 20240110170629.png]]

The one thing that is not differentiable in Fast R-CNN is region proposal method. And it takes many time. It will be changed in the next model

## Faster R-CNN

![[Pasted image 20240110180458.png]]

![[Pasted image 20240111040115.png]]

![[Pasted image 20240111045714.png]]

![[Pasted image 20240111045732.png]]

