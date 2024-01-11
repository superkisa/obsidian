![[Pasted image 20240111031216.png]]

### Algorithm

When we have several bounding boxes as guesses for our problem (for the same class), we have to choose only one of them

Given bboxes from one class we look at overlap of this bboxes. And if bboxes overlap enough (let's say IoU is 0.5) we take the bbox with highest prediction score (probability). The rest of them we just get rid.

