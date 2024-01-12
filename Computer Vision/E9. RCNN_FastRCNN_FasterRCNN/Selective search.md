https://paperswithcode.com/method/selective-search

![[Pasted image 20240112142749.png]]

Selective Search is a region proposal algorithm used in object detection. It's designed to be fast with a very high recall. The algorithm is based on computing hierarchical grouping of similar regions based on color, texture, size, and shape compatibility [3](https://learnopencv.com/selective-search-for-object-detection-cpp-python/).

Here's a step-by-step explanation of how Selective Search works:
	1. **Initial Segmentation**: The algorithm starts by over-segmenting the image based on the intensity of the pixels using a graph-based segmentation method by Felzenszwalb and Huttenlocher. This results in a large number of small regions that cover the entire image [2](https://www.geeksforgeeks.org/selective-search-for-object-detection-r-cnn/).
	2. **Greedy Merging**: Then, the algorithm uses a greedy algorithm to combine similar regions into larger ones. The idea is to start with the smallest regions and progressively merge them until only a few large regions remain. Two regions are considered similar if they have similar color, texture, size, and shape [2](https://www.geeksforgeeks.org/selective-search-for-object-detection-r-cnn/).
	3. **Region Proposals**: At each iteration of the greedy algorithm, the merged regions are added to the list of region proposals. This results in a hierarchy of region proposals, starting with small, fine-grained proposals and ending with larger, coarse-grained proposals. The final region proposals are the areas of the image that the algorithm considers likely to contain an object [4](https://paperswithcode.com/method/selective-search).

While Selective Search is powerful and versatile, it's worth noting that it's not perfect. Its performance can be affected by the complexity of the scene, the quality of the initial segmentation, and the specific definition of "similarity" used to merge regions. Despite these challenges, Selective Search remains a popular choice for object detection tasks due to its speed and high recall [3](https://learnopencv.com/selective-search-for-object-detection-cpp-python/).