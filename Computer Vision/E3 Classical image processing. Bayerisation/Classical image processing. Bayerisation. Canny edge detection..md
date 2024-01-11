![[cv_04_morphology.ipynb]]
#### Quantization
To save some memory we could use less colour values.
1. Define clusters in image
2. Define colour for each cluster
3. Fill cluster with its colour
Image will contain a palette and pixels referring to it.
#### Histogram equalization for adjusting contrast
#### [Gamma correction](https://en.wikipedia.org/wiki/Gamma_correction)
This transform is related to difference in eye and camera light perception, [see more info here](https://www.cambridgeincolour.com/tutorials/gamma-correction.htm)
#### [Morphology](https://docs.opencv.org/3.4/d9/d61/tutorial_py_morphological_ops.html):
![[Pasted image 20240110192603.png]]
 1. Erosion -- делает линии тоньше (make lines thiner)
```python
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
 [фильтр Гаусса](https://homepages.inf.ed.ac.uk/rbf/HIPR2/gsmooth.htm)
 [Алгоритм состоит из пяти отдельных шагов](https://habr.com/ru/articles/114589/):
1. **Сглаживание**. Размытие изображения для удаления шума.
2. **Поиск градиентов**. Границы отмечаются там, где градиент изображения приобретает максимальное значение.
3. **Подавление не-максимумов**. Только локальные максимумы отмечаются как границы.
4. **Двойная пороговая фильтрация**. Потенциальные границы определяются порогами.
5. **Трассировка области неоднозначности**. Итоговые границы определяются путём подавления всех краёв, несвязанных с определенными (сильными) границами.

#### Circular Hough Transform
ищет кружочки на картинках (и эллипсы)
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

#### [Bayerisation](https://en.wikipedia.org/wiki/Bayer_filter)
or mosaicing (?) короче что-то с мазаикой, но тип оно встраивается мозаикой из красных, синих и зеленых блоков разной интенсивности.
Обратный процесс называется demosaicing (так что ли или короче демозаика :) ) or debayerisation
The raw images coming from the camera are bayerized. They are represented as a two-dimensional array, where individual pixels encode the intensity of blue, green, and red colors.
![[Pasted image 20240111001932.png]]
```
def rgb_to_bayer(img_rgb: np.ndarray) -> np.ndarray:
    H, W = img_rgb.shape[0], img_rgb.shape[1]
    bayer_img = np.zeros((H, W))
    bayer_img[0:H:2, 0:W:2] = img_rgb[0:H:2, 0:W:2, 2]
    bayer_img[1:H:2, 0:W:2] = img_rgb[0:H:2, 0:W:2, 1]
    bayer_img[0:H:2, 1:W:2] = img_rgb[0:H:2, 1:W:2, 1]
    bayer_img[1:H:2, 1:W:2] = img_rgb[1:H:2, 1:W:2, 0]

    return bayer_img.astype(np.uint8)
```
![[Pasted image 20240111002147.png]]
![[Pasted image 20240111002155.png]]
![[Pasted image 20240111002204.png]]

**Demosaicing

Converting an image captured in RGGB Bayer pattern to RGB involves a process called demosaicing or debayering. In the RGGB pattern, each pixel has a color filter that allows only one of the Red (R), Green (G), or Blue (B) components to be captured. To reconstruct a full-color RGB image, the missing color information must be interpolated.

Here's a simplified explanation of the demosaicing process:

1. **Interpolation of Green Channel:**
    
    - Since there are two green pixels for every one red and one blue pixel in RGGB, the green channel is often the first to be interpolated. The missing green values for red and blue pixels are estimated based on the surrounding green pixels.
2. **Interpolation of Red and Blue Channels:**
    
    - Once the green channel is interpolated, the red and blue channels can be filled in. For a red pixel, the missing red value is interpolated using neighboring green and blue pixels. Similarly, for a blue pixel, the missing blue value is estimated using neighboring green and red pixels.
3. **Adjustments and Refinement:**
    
    - Various algorithms and techniques may be applied to refine the interpolated values and improve the overall image quality. These may include color correction, noise reduction, and sharpening.
4. **Conversion to RGB:**
    
    - After the interpolation process, you have three separate color channels (red, green, and blue). These channels are combined to form the final RGB image.

The specific demosaicing algorithm used can vary, and there are different approaches, such as bilinear interpolation, nearest-neighbor interpolation, or more sophisticated algorithms like adaptive homogeneity-directed demosaicing (AHDD). The choice of algorithm can impact the quality of the final RGB image.