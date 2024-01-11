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