
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

Let's see steps of training R-CNN models

![[Pasted image 20240110135047.png]]

![[Pasted image 20240110135217.png]]

![[Pasted image 20240110135427.png]]

![[Pasted image 20240110135455.png]]

![[Pasted image 20240110135529.png]]

