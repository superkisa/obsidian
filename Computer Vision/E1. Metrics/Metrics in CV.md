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
## mAP

mAP (Mean Average Precision) - a commonly used metric for evaluating the performance of object detection models. 

The mAP value is calculated the following way: 
- we firstly draw a bounding box around each object in an image 
- then comparing the predicted bounding box from the model with the ground truth bounding box. For each predicted bounding box, a "hit" is recorded if the predicted box overlaps with the ground truth box by a certain amount (usually defined as a threshold, such as an IoU of 0.5) 
- **The average precision (AP)** for an image is then calculated as the ratio of the number of hits to the total number of predicted bounding boxes. To calculate average precision we use the following steps: 
1. Sort predictions by decreasing confidence score 
2. Count the number of true positives (hits) and false positives at each step. 
3. Calculate the precision at each point on the curve, where precision is defined as true positives / (true positives + false positives) 
4. Calculate the recall at each point on the curve, where recall is defined as true positives / total number of ground truth objects 
5. Plot precision on the y-axis and recall on the x-axis to generate the precision-recall curve 
6. Calculate the area under the precision-recall curve 
- To calculate mAP, the process is repeated across all the images in a dataset, and the average precision value is calculated for each class separately 
- Then, the overall mAP is calculated as the average of mean Average precision across all classes. 

**How mAP is different from precision?** 
It is different from a simple precision in a way that, average precision gives overall performance of model for all recalls and precisions, whereas precision is only one number representing model performance at a particular recall point. 
#### What are the disadvantages of mAP? 
One disadvantage is that ==mAP does not take into account the confidence score== of the predictions, which can lead to problems when comparing models that make different numbers of predictions.  
**For example**, a model that makes many low-confidence predictions will typically have a lower mAP than a model that makes fewer high-confidence predictions, even if the latter model is less accurate overall. 

Another disadvantage of mAP is that ==it does not account for the position== of the predicted bounding boxes. A model that makes a correct prediction in the center of the object may receive the same mAP score as a model that makes a correct prediction in the corner of the object. 

The mAP metric also ==doesn't take into account partial occlusions==, a model that detects an object partially occluded gets the same score as a model that detects the same object completely visible. 

Furthermore, the authors of YOLO v3 paper suggest that the mAP metric ==can be overly sensitive to small changes in the IoU threshold==. A model that performs well at one threshold may perform poorly at another threshold, even if the model's overall performance is similar. 

Due to these limitations, the authors of YOLO v3 propose to use an alternative detection metric, called **"mean average precision across scales" (ms-AP)**, which takes into account the scale of the object and the confidence score of the predictions, which they found to better capture the performance of object detectors. 

#### Dice Similarity Coefficient (DSC) 
DSC - a measure of the similarity between the predicted segmentation and the ground truth segmentation. It is usually calculated between two binary masks, the predicted mask and the ground truth mask:  

DSC = 2*(Intersection of predicted and ground truth mask) / (Size of predicted mask + Size of ground truth mask) 

It is important to note that, even though IoU and DSC are both commonly used in evaluating segmentation algorithms they are not always interchangeable and the choice of metric often depends on the specific application. 