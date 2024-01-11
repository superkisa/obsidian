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

### Original Yolo

![[Pasted image 20240111042312.png]]

In YOLO v1 there was 2 objects for each cell. 

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

