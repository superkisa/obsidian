# Metrics for CV problems: IoU, mAP. 
## IoU (aka Jaccard index) 
![[Pasted image 20240107145135.png]]
[[cv_lect_CV_Tasks_1.pdf|Presentation]] pp 43-48
It is a measure of the overlap between the predicted segmentation and the ground truth 
segmentation. 

IoU = area of overlap / area of union 
IoU ~ 0.7-0.9 is considered to be pretty good. 

**What if IoU is equal to 0?**
When there is no intersection BBxs, then we do not know how far these objects are from 
each other - so also use other metrics such as GIoU - generalized IoU. 

**What is GIoU?**
Generalized IoU (GIoU) takes into account not only the overlap between the predicted 
bounding box and the ground truth bounding box, but also the overlap between the predicted 
bounding box and the surrounding context. 
$$
GIoU = IoU - (Union(Bbox,Context) - Bbox)
$$
*Bbox* is the predicted bounding box,  
*Context* is the surrounding context (usually defined as the area outside the ground truth 
bounding box but inside an expanded bounding box that is larger than the ground truth by a 
certain factor.),  
*IoU* is the standard intersection over union  
*Union(Bbox,Context)* is the union between *Bbox* and *Context*.
![[Pasted image 20240113133601.png]]
## mAP
https://learnopencv.com/mean-average-precision-map-object-detection-model-evaluation-metric/#What-is-Mean-Average-Precision-(mAP)?
 - a commonly used metric for evaluating the performance of object detection models. 

The mAP value is calculated the following way: 
- we firstly draw a bounding box around each object in an image 
- then comparing the predicted bounding box from the model with the ground truth bounding box. For each predicted bounding box, a "hit" is recorded if the predicted box overlaps with the ground truth box by a certain amount (usually defined as a threshold, such as an IoU of 0.5) 
Значение  mAP вычисляется следующим образом:
- сначала мы рисуем ограничивающую рамку вокруг каждого объекта на изображении
- затем сравниваем предсказанную ограничивающую рамку из модели с реальной ограничивающей рамкой. Для каждого прогнозируемого ограничивающего прямоугольника регистрируется "попадание", если прогнозируемый прямоугольник перекрывается с основным прямоугольником истинности на определенную величину (обычно определяемую как пороговое значение, например,  IoU в размере 0,5).

- **The average precision (AP)** for an image is then calculated as the ratio of the number of hits to the total number of predicted bounding boxes. To calculate average precision we use the following steps: 
1. Sort predictions by decreasing confidence score 
2. Count the number of true positives (hits) and false positives at each step. 
3. Calculate the precision at each point on the curve, where precision is defined as true positives / (true positives + false positives) 
4. Calculate the recall at each point on the curve, where recall is defined as true positives / total number of ground truth objects 
5. Plot precision on the y-axis and recall on the x-axis to generate the precision-recall curve 
6. Calculate the area under the precision-recall curve 
- To calculate mAP, the process is repeated across all the images in a dataset, and the average precision value is calculated for each class separately 
- Then, the overall mAP is calculated as the average of mean Average precision across all classes. 

**Затем вычисляется средняя точность (AP)** для изображения как отношение количества просмотров к общему количеству прогнозируемых ограничивающих рамок. Для вычисления средней точности мы используем следующие шаги:
1. Сортируем прогнозы по убыванию доверительного балла
2. Подсчитайте количество истинных срабатываний (попаданий) и ложных срабатываний на каждом шаге.
3. Вычислите точность в каждой точке кривой, где точность определяется как истинные срабатывания / (истинные срабатывания + ложные срабатывания)
4. Вычислите отзыв в каждой точке кривой, где отзыв определяется как истинные положительные результаты / общее количество объектов, подтверждающих достоверность данных.
5. Отложите точность по оси y и отзыв по оси x, чтобы сгенерировать кривую точности-отзыва
6. Вычислите площадь под кривой точности воспроизведения
- Для вычисления карты процесс повторяется для всех изображений в наборе данных, и среднее значение точности вычисляется для каждого класса отдельно
- Затем общая mAP вычисляется как среднее значение средней точности по всем классам.

**How mAP is different from precision?** 
It is different from a simple precision in a way that, average precision gives overall performance of model for all recalls and precisions, whereas precision is only one number representing model performance at a particular recall point. 

Она отличается от простой точности тем, что средняя точность дает общую производительность модели для всех отзывов и уточнений, тогда как точность - это всего лишь одно число, представляющее производительность модели в определенный момент отзыва.
![[Pasted image 20240112184421.png]]
![[Pasted image 20240112184509.png]]
![[Pasted image 20240112184524.png]]
![[Pasted image 20240112184539.png]]
#### What are the disadvantages of mAP? 
One disadvantage is that ==mAP does not take into account the confidence score== of the predictions, which can lead to problems when comparing models that make different numbers of predictions.  
**For example**, a model that makes many low-confidence predictions will typically have a lower mAP than a model that makes fewer high-confidence predictions, even if the latter model is less accurate overall. 

Another disadvantage of mAP is that ==it does not account for the position== of the predicted bounding boxes. A model that makes a correct prediction in the center of the object may receive the same mAP score as a model that makes a correct prediction in the corner of the object. 

The mAP metric also ==doesn't take into account partial occlusions==, a model that detects an object partially occluded gets the same score as a model that detects the same object completely visible. 

Furthermore, the authors of YOLO v3 paper suggest that the mAP metric ==can be overly sensitive to small changes in the IoU threshold==. A model that performs well at one threshold may perform poorly at another threshold, even if the model's overall performance is similar. 

Due to these limitations, the authors of YOLO v3 propose to use an alternative detection metric, called **"mean average precision across scales" (ms-AP)**, which takes into account the scale of the object and the confidence score of the predictions, which they found to better capture the performance of object detectors. 

### Importance of mAP:

- mAP provides a holistic measure of a model's performance, considering both precision and recall.
- It helps assess how well a model generalizes to different classes and different levels of difficulty.

In summary, mAP is a versatile metric in computer vision, providing a comprehensive evaluation of models for tasks like object detection and instance segmentation. Its use is prevalent in research, competitions, and benchmarking in the computer vision community.

#### Dice Similarity Coefficient (DSC) 
DSC - a measure of the similarity between the predicted segmentation and the ground truth segmentation. It is usually calculated between two binary masks, the predicted mask and the ground truth mask:  

DSC = 2*(Intersection of predicted and ground truth mask) / (Size of predicted mask + Size of ground truth mask) 

It is important to note that, even though IoU and DSC are both commonly used in evaluating segmentation algorithms they are not always interchangeable and the choice of metric often depends on the specific application. 

#### Focal Loss

![[Pasted image 20240111030536.png]]

Суть в том, что при CE (cross entropy) мы пытаемся просто хорошо классифицировать объекты, из-за чего пытаемся даже улучшать объекты, которые показывают 80%, 90%, чтобы устремить к 100%. Это видно на графике

А если посмотрите на Focal Loss, то тут ситуация интереснее. Допустим при gamma = 5 наша модель уже не будет штрафовать или как-то реагировать на прогнозы с 60% вероятностью! То есть благодаря данному лоссу, мы можем сфокусировать модель именно на низких вероятностях при верности ответа.

The main idea behind focal loss is to assign different weights to different examples during the training process. It aims to give more emphasis to hard, misclassified examples (those with a low probability of being correctly classified) and less emphasis to well-classified examples. This helps the model focus more on challenging instances and improve its ability to handle imbalanced datasets.

Here are the key concepts of focal loss:

1. **Modulation of Loss Weights:**
    
    - The focal loss introduces a modulating factor for each training example, which adjusts the loss contribution based on the predicted probability of the true class. The formula for focal loss is:
        
        $FL(p_t)=−(1−p_t)^{\gamma}⋅log⁡(p_t)$
        
        where $p_t$​ is the predicted probability of the true class, and γ is a user-defined focusing parameter. The term $(1−p_t)^γ$ modulates the loss based on the predicted probability, giving higher weight to misclassified examples.
        
2. **Handling Class Imbalance:**
    
    - The focal loss is particularly effective in handling class imbalance, as it down-weights the easy-to-classify examples and up-weights the hard-to-classify examples. This is crucial in tasks like object detection, where the number of background regions is much larger than the number of object regions.
3. **Improved Learning for Rare Classes:**
    
    - Focal loss improves the model's ability to learn from rare or minority classes by assigning higher importance to challenging examples. This is beneficial in scenarios where certain classes occur less frequently in the dataset.
4. **Adjustable Focusing Parameter:**
    
    - The parameter γ is adjustable and allows users to control the level of emphasis given to hard examples. A higher γ puts more focus on misclassified examples.

In summary, the focal loss is designed to address the challenges posed by imbalanced datasets in object detection tasks by assigning varying weights to training examples based on their predicted probabilities. It has proven effective in improving the performance of models on tasks with imbalanced class distributions.