![[cv_04_morphology.ipynb]]
[Morphology](https://docs.opencv.org/3.4/d9/d61/tutorial_py_morphological_ops.html)
[Skeletonize](https://scikit-image.org/docs/stable/auto_examples/edges/plot_skeleton.html)
[Convex Hull](https://scikit-image.org/docs/stable/auto_examples/edges/plot_convex_hull.html)
[Canny Edge Detection](https://docs.opencv.org/4.8.0/da/d22/tutorial_py_canny.html)

Circular Hough Transform
[Wiki on lines detection](https://en.wikipedia.org/wiki/Hough_transform)
[skimage linear doc](https://scikit-image.org/docs/stable/auto_examples/edges/plot_line_hough_transform.html)
[skimage circular doc](https://scikit-image.org/docs/stable/auto_examples/edges/plot_circular_elliptical_hough_transform.html)

Watershed segmentation
https://img-blog.csdnimg.cn/20190315153313192.png
[skimage doc](https://scikit-image.org/docs/stable/auto_examples/segmentation/plot_watershed.html)
[opencv doc](https://docs.opencv.org/4.8.0/d3/db4/tutorial_py_watershed.html)

Generic pipeline for segmentation
- setting threshold values for binarizatioin with Otsu filter
- filling small noisy dots with morphological closing
- border artifacts (objects intersection) deletion
- filtering small objects by square