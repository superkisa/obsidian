Понятная [статья](https://habr.com/ru/articles/556404/)
![[Pasted image 20240111031753.png]]

![[Pasted image 20240111032459.png]]

Как можно видеть на слайде, точность Yolo не такая хорошая, но зато скорость и время работы в разы выше, чем у аналогов. И то на сегодняшний день новые версии yolo по точности приблизились к аналогам. 


![[Pasted image 20240111032642.png]]

Суть в том, что раньше модели были двухстадийные (R-CNN). YOLO является одностадийной моделью, то есть мы просто передаем картинку в нейронку и получаем результаты.

## Algorithm of YOLO

1) We apply CNN with several layers and then we get feature map
2) The difference here is that we split the image into a grid

![[Pasted image 20240111033152.png]]

And for each cell we predict objectness

![[Pasted image 20240111033237.png]]

So, is it some object here or not?
In parts where the answer was yes, we apply anchors

![[Pasted image 20240111033458.png]]

The idea of anchors: we get our anchors from dataset by clustering actual bounding boxes and we apply these bounding boxes into these points.


![[Pasted image 20240111033657.png]]

In this point we get set of bounding boxes, which we think could contain some objects.

![[Pasted image 20240111041143.png]]

4) Then to predict a class of an object in bounding box we do not crop it, because it is an expensive action. Instead of, we predict class for each cell.

![[Pasted image 20240111041346.png]]

5) Based on this we calculate class for each bounding box based on which part of cell is covered by this bbox

![[Pasted image 20240111041522.png]]

And finally we use Non Maximum Suppression to get the result.

### The  problem of YOLO

Some boxes are overlapping

The limitation of YOLO algorithm is that it struggles with small objects within the image, for example it might have difficulties in detecting a flock of birds

### Original Yolo

![[Pasted image 20240111042312.png]]

In YOLO v1 there was 2 objects for each cell. 

[Вот тут](https://habr.com/ru/articles/460869/#:~:text=%D0%9C%D0%BE%D0%B4%D0%B5%D0%BB%D1%8C%20YOLOv3%20%D0%B2%20%D0%BA%D0%B0%D1%87%D0%B5%D1%81%D1%82%D0%B2%D0%B5%20%D0%B2%D1%8B%D1%85%D0%BE%D0%B4%D0%B0%20%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D1%83%D0%B5%D1%82%20%D1%82%D1%80%D0%B8%20%D1%81%D0%BB%D0%BE%D1%8F) как-то для меня понятнее расписали, как формируется выход сети:
![[Pasted image 20240111223607.png]]

Также можно увидеть, что изначально картинку делили на 49 частей, 7х7. И для каждой клетки вот это все прогнозировалось при условии, что там обнаружен объект.

![[Pasted image 20240111042743.png]]

### How to make YOLOv1 more accurate? YOLO v2

![[Pasted image 20240111044539.png]]

1) They used more datasets. They pretrained model in ImageNet and then fine-tune it in coco.
Тут стоит подчеркнуть, что количество классов также сильно увеличилось.

![[Pasted image 20240111044630.png]]

2) Also they take more anchors
3) They did multi-scale training (подавали на вход сети изображения те же, но масштабированные)

![[Pasted image 20240111044747.png]]

They train their convolutional layers over different size of input data

As a result, 

![[Pasted image 20240111044929.png]]

They also written their own framework for neural networks and their own backbone architecture (darknet19), which was pretrained on data

![[Pasted image 20240111045206.png]]

How did they join datasets?

![[Pasted image 20240111045420.png]]

Взяли из 22k только 9k, так как CE работает не очень хорошо, когда так много классов. 

![[Pasted image 20240111121755.png]]

![[Pasted image 20240111121814.png]]

![[Pasted image 20240111121841.png]]

![[Pasted image 20240111121854.png]]

WordTree было сделано вручную.

![[Pasted image 20240111122024.png]]

Таким образом можно было совместить 2 этих датасета, так как всегда можно остановится на определенном уровне.

![[Pasted image 20240111122142.png]]

Здесь мы считаем несколько softmax на каждом уровне.

### Yolov3

https://pjreddie.com/darknet/yolo/ - this site is about yolov3 by authors

Если посмотреть на график справа

![[Pasted image 20240111030536.png]]

То можно уивдеть, что YOLOv2 сильно отстает по показателям от моделей. Но не YOLOv3

![[Pasted image 20240111122935.png]]

https://arxiv.org/pdf/1804.02767.pdf - here you can find scientific paper of YOLOv3

1) They added corrections for bounding boxes
![[Pasted image 20240111130018.png]]
![[Pasted image 20240111130044.png]]

2) They make predictions across scales
They use 3 different networks. One network for small size, one network median size, one network for bigger size. It's started to be possible because of development of GPUs.
3) They increase size of convolutional network

[Source](https://medium.com/@venkatakrishna.jonnalagadda/object-detection-yolo-v1-v2-v3-c3d5eca2312a) (VPN)
### The changes from YOLO to YOLO v2:

**Batch Normalization**: it normalise the input layer by altering slightly and scaling the activations. Batch normalization decreases the shift in unit value in the hidden layer and by doing so it improves the stability of the neural network. By adding batch normalization to convolutional layers in the architecture MAP (mean average precision) has been improved by 2% [2]. It also helped the model regularise and overfitting has been reduced overall.

**Higher Resolution Classifier:** the input size in YOLO v2 has been increased from 224x224 to 448x448. The increase in the input size of the image has improved the MAP (mean average precision) upto 4%. This increase in input size is been applied while training the YOLO v2 architecture DarkNet 19 on ImageNet dataset. [3]

**Anchor Boxes:** one of the most notable changes which can visible in YOLO v2 is the introduction the anchor boxes. YOLO v2 does classification and prediction in a single framework. These anchor boxes are responsible for predicting bounding box and this anchor boxes are designed for a given dataset by using clustering(k-means clustering).[4]

**Fine-Grained Features:** one of the main issued that has to be addressed in the YOLO v1 is that detection of smaller objects on the image. This has been resolved in the YOLO v2 divides the image into 13*13 grid cells which is smaller when compared to its previous version. This enables the yolo v2 to identify or localize the smaller objects in the image and also effective with the larger objects. [4, 5]

**Multi-Scale Training:** on YOLO v1 has a weakness detecting objects with different input sizes which says that if YOLO is trained with small images of a particular object it has issues detecting the same object on image of bigger size. This has been resolved to a great extent in YOLO v2 where it is trained with random images with different dimensions range between 320*320 to 608*608 [5]. This allows the network to learn and predict the objects from various input dimensions with accuracy.

**Darknet 19:** YOLO v2 uses Darknet 19 architecture with 19 convolutional layers and 5 max pooling layers and a softmax layer for classification objects. The architecture of the Darknet 19 has been shown below. Darknet is a neural network framework written in Clanguage and CUDA. It’s really fast in object detection which is very important for predicting in real-time.

### YOLO v2 to YOLO v3:

**Bounding Box Predictions:** In YOLO v3 gives the score for the objects for each bounding boxes. It uses logistic regression to predict the objectiveness score.

**Class Predictions:** In YOLO v3 it uses logistic classifiers for every class instead of softmax which has been used in the previous YOLO v2. By doing so in YOLO v3 we can have multi-label classification. With softmax layer if the network is trained for both a person and man, it gives the probability between person and man let’s say 0.4 and 0.47. With the independent classifier gives the probability for each class of objects. For example if the network is trained for person and a man it would give the probability of 0.85 to person and 0.8 for the man and label the object in the picture as both man and person.

**Feature Pyramid Networks (FPN):** YOLO v3 makes predictions similar to the FPN where 3 predictions are made for every location the input image and features are extracted from each prediction. By doing so YOLO v3 has the better ability at different scales. As explained from the paper by [7] each prediction is composed with boundary box, objectness and 80 class scores. Doing upsampling from previous layers allows getting meaning full semantic information and finer-grained information from earlier feature map. Now, adding few more convolutional layers to process improves the output.

**Darknet-53:** the predecessor YOLO v2 used Darknet-19 as feature extractor and YOLO v3 uses the Darknet-53 network for feature extractor which has 53 convolutional layers. It is much deeper than the YOL v2 and also had shortcut connections. Darknet-53 composes of the mainly with 3x3 and 1x1 filters with shortcut connections.