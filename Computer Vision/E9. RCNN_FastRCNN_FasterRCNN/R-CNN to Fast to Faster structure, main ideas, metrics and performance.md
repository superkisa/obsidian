[[Difference between the three]]

[Artical about these three](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/)

Enter slides
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

Some additional info
	Here's a [[step-by-step explanation of how R-CNN]] works:
	1. **Region Proposals**: The first step in R-CNN is to generate region proposals. This is done using a technique known as [[Selective search]], which divides the image into small regions and proposes regions that likely contain an object. Approximately 2000 region proposals are generated [1](https://www.geeksforgeeks.org/r-cnn-region-based-cnns/amp/).
	2. **Feature Extraction**: Next, these region proposals are fed into a CNN to extract features. The CNN consists of several convolutional layers followed by pooling layers. The purpose of this step is to convert the raw pixel values of the image into a set of high-level features that capture the important characteristics of the objects in the image [2](https://blog.roboflow.com/what-is-r-cnn/amp/).
	3. **Classification**: Once the features have been extracted, they are passed to a linear [[Support Vector Machine (SVM)]] to classify whether each region proposal contains an object and what class of object it is [1](https://www.geeksforgeeks.org/r-cnn-region-based-cnns/amp/).
	4. **Bounding Box Regression**: Finally, a separate regression model is trained to predict the exact location of the object within the region proposal. This is done by predicting the coordinates of the bounding box around the object [1](https://www.geeksforgeeks.org/r-cnn-region-based-cnns/amp/).
	Despite its effectiveness, R-CNN has some limitations. Because it uses selective search to generate region proposals, the quality of these proposals can vary, leading to poor object detection. Additionally, R-CNN is computationally expensive due to the large number of region proposals and the need to run the entire CNN on each one. These drawbacks led to the development of faster and more efficient versions of R-CNN, such as Fast R-CNN and Faster R-CNN [1](https://www.geeksforgeeks.org/r-cnn-region-based-cnns/amp/), [2](https://blog.roboflow.com/what-is-r-cnn/amp/).
	![[Pasted image 20240112145045.png]]
	![[Pasted image 20240112152517.png]]

Presentation
	![[Pasted image 20240110131646.png]]
	But there is some question: how to solve bbox regression? There is a problem, because predifined bbox can be not similiar to the ground true bbox.
	We can predict not  coordinates of bboxes, but transformation.
	(tx, ty, tn, tw)
	
	![[Pasted image 20240110133726.png]]
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

Some additional info
	Fast R-CNN is an improvement over the original R-CNN model that addresses several of its limitations, including computational efficiency and the handling of multiple objects in an image. Here's how Fast R-CNN works:
	1. **Region Proposals**: Like R-CNN, Fast R-CNN starts with region proposals. These proposals are generated using a method like selective search, which segments the image into smaller regions and proposes regions that likely contain an object [2](https://paperswithcode.com/method/fast-r-cnn).
	2. **Shared Convolutional Layers**: Unlike R-CNN, which performs feature extraction for each region proposal independently, Fast R-CNN applies the convolutional layers to the entire image only once. This allows it to share computations across all region proposals, which significantly speeds up the process [3](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/).
	3. **ROI Pooling**: After the convolutional layers, Fast R-CNN introduces a new layer called Region of Interest (ROI) Pooling. This layer extracts fixed-size feature vectors from each region proposal. It splits each region proposal into a grid of cells, applies max pooling to each cell, and concatenates all values to form a feature vector for that region proposal [3](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/).
	4. **Classification and Bounding Box Regression**: The ROI Pooling layer feeds the pooled feature vectors into fully connected layers for classification and bounding box regression. The classification layer assigns each region proposal to a class, while the regression layer refines the bounding box coordinates of each region proposal [3](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/).
	One limitation of Fast R-CNN is that it still relies on the time-consuming Selective Search algorithm for generating region proposals. Another downside is that while Fast R-CNN shares computations across multiple proposals, it does not cache the extracted features, which could lead to increased memory usage [3](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/).
	![[Pasted image 20240112152418.png]]

Presentation
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

Some additional info
	Faster R-CNN is an extension of Fast R-CNN that further improves its speed and performance. It incorporates a Region Proposal Network (RPN) directly into the network architecture, eliminating the need for a separate region proposal stage. Here's a detailed explanation of how Faster R-CNN works:
	1. **Region Proposals**: Unlike R-CNN and Fast R-CNN, which rely on external methods like selective search to generate region proposals, Faster R-CNN includes a built-in [[RPN]] that generates region proposals directly within the network. The RPN uses anchor boxes to propose potential object locations in the image [1](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/amp/).
	2. **Shared Convolutional Layers**: Similar to Fast R-CNN, Faster R-CNN also shares the convolutional layers between the RPN and the rest of the network. This allows the network to share computations across all region proposals, significantly increasing efficiency [1](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/amp/).
	3. **ROI Pooling**: After the convolutional layers, Faster R-CNN introduces a new layer called Region of Interest (ROI) Pooling. This layer extracts fixed-size feature vectors from each proposed region. It splits each region proposal into a grid of cells, applies max pooling to each cell, and concatenates all values to form a feature vector for that region proposal [1](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/amp/).
	4. **Classification and Bounding Box Regression**: The ROI Pooling layer feeds the pooled feature vectors into fully connected layers for classification and bounding box regression. The classification layer assigns each region proposal to a class, while the regression layer refines the bounding box coordinates of each region proposal [1](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/amp/).
	The architecture of Faster R-CNN is shown in the next figure. It consists of 2 modules:
	1. **RPN**: For generating region proposals.
	2. **Fast R-CNN**: For detecting objects in the proposed regions.
	The RPN module is responsible for generating region proposals. It applies the concept of attention in neural networks, so it guides the Fast R-CNN detection module to where to look for objects in the image.
	![[Pasted image 20240112154822.png]]
	 Note how the convolutional layers (e.g. computations) are shared across both the RPN and the Fast R-CNN modules.
	One drawback of Faster R-CNN is that the RPN is trained where all anchors in the mini-batch, of size 256, are extracted from a single image. Because all samples from a single image may be correlated (i.e., their features are similar), the network may take a long time until reaching convergence [1](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/amp/).

Presentation
	
	![[Pasted image 20240110180458.png]]
	
	![[Pasted image 20240111040115.png]]
	
	![[Pasted image 20240111045714.png]]
	
	![[Pasted image 20240111045732.png]]

