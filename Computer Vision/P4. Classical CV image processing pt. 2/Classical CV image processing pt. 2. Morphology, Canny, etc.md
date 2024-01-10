![[cv_04_morphology.ipynb]]
#### [Morphology](https://docs.opencv.org/3.4/d9/d61/tutorial_py_morphological_ops.html):
![[Pasted image 20240110192603.png]]
 1. Erosion -- делает линии тоньше (make lines thiner)
```
    import cv2 as cv
	import numpy as np
	img = cv.imread('j.png', cv.IMREAD_GRAYSCALE)
	kernel = np.ones((5,5),np.uint8)
	erosion = cv.erode(img,kernel,iterations = 1)
```
![[Pasted image 20240110192641.png]]
 2. Dilation -- делает линии толще (makes lines thiker)
    `dilation = cv.dilate(img,kernel,iterations = 1)`
    ![[Pasted image 20240110192841.png]]
3. Opening -- erosion потом dilation (erosion fallowed by delation). Убирает мелкий белый шум.
	   `opening = cv.morphologyEx(img, cv.MORPH_OPEN, kernel)`
	   ![[Pasted image 20240110193050.png]]
   1. Closing -- dilation потом erosion (dilation fallowed by erosion). Убирает мелкий черный шум на белом фоне.
	`closing = cv.morphologyEx(img, cv.MORPH_CLOSE, kernel)`
      ![[Pasted image 20240110193253.png]]
5.  Morphological Gradient = dilation - erosion (It is the difference between dilation and erosion of an image). Выделяет границу объекта.
	`gradient = cv.morphologyEx(img, cv.MORPH_GRADIENT, kernel)`
	   ![[Pasted image 20240110193757.png]]
6. Top Hat = original img - opening img (It is the difference between input image and Opening of the image). Убирает большие белые объекты изображения.
	`tophat = cv.morphologyEx(img, cv.MORPH_TOPHAT, kernel)`
	![[Pasted image 20240110194253.png]]
7. Black Hat = original img - closing img (It is the difference between input image and Closing of the image). Выделяет черные "внутренности" объекта.
	 `blackhat = cv.morphologyEx(img, cv.MORPH_BLACKHAT, kernel)`
	 ![[Pasted image 20240110195335.png]]

#### [Skeletonize](https://scikit-image.org/docs/stable/auto_examples/edges/plot_skeleton.html)
__Подходы к построению остова__

Метод skeletonize работает, выполняя последовательные проходы изображения, удаляя пиксели на границах объекта. Это продолжается до тех пор, пока больше не удастся удалить пиксели. Изображение коррелируется с маской, которая присваивает каждому пикселю номер в диапазоне [0… 255], соответствующий каждому возможному шаблону из его 8 соседних пикселей. Затем используется таблица поиска для присвоения пикселям значения 0, 1, 2 или 3, которые выборочно удаляются во время итераций. 

Существует метод построения остова по методу Lee (skeletonize (..., method = 'lee')), который использует структуру данных октодерева для исследования окрестности пикселя размером 3x3х3. Алгоритм выполняется путем итеративного прохождения по изображению и удаления пикселей на каждой итерации, пока изображение не перестанет изменяться. Каждая итерация состоит из двух шагов: во-первых, составляется список кандидатов на удаление; затем пиксели из этого списка последовательно перепроверяются, чтобы лучше сохранить связность изображения.

Обратите внимание, что метод Ли разработан для использования с трехмерными изображениями и выбирается для них автоматически. В иллюстративных целях мы применяем этот алгоритм к двухмерному изображению.

Также мы можем применить morphological thinning:
![[Pasted image 20240110210430.png]]

#### [Convex Hull](https://scikit-image.org/docs/stable/auto_examples/edges/plot_convex_hull.html)
![[Pasted image 20240110210552.png]]
![[Pasted image 20240110210627.png]]

#### [Canny Edge Detection](https://docs.opencv.org/4.8.0/da/d22/tutorial_py_canny.html)
детекция граней

#### Circular Hough Transform
[Wiki on lines detection](https://en.wikipedia.org/wiki/Hough_transform)
[skimage linear doc](https://scikit-image.org/docs/stable/auto_examples/edges/plot_line_hough_transform.html)
[skimage circular doc](https://scikit-image.org/docs/stable/auto_examples/edges/plot_circular_elliptical_hough_transform.html)

#### Watershed segmentation
https://img-blog.csdnimg.cn/20190315153313192.png
[skimage doc](https://scikit-image.org/docs/stable/auto_examples/segmentation/plot_watershed.html)
[opencv doc](https://docs.opencv.org/4.8.0/d3/db4/tutorial_py_watershed.html)

#### Generic pipeline for segmentation
- setting threshold values for binarizatioin with Otsu filter
- filling small noisy dots with morphological closing
- border artifacts (objects intersection) deletion
- filtering small objects by square