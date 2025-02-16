[[Intro to CV, classic CV, libraries overview]]
1. **Image Classification:**
    
    - **Problem Statement:** Given an input image, the task is to assign a label or category to the entire image.
    - **Example:** Identifying whether an image contains a cat or a dog.
    - **Applications:** Object recognition, scene understanding, and image categorisation.
2. **Object Detection:**
    
    - **Problem Statement:** Locating and classifying objects within an image, often by drawing bounding boxes around them.
    - **Example:** Detecting and localising multiple pedestrians, cars, and bicycles in a street scene.
    - **Applications:** Autonomous vehicles, surveillance, and image-based search.
3. **Image Segmentation:**
    
    - **Problem Statement:** Dividing an image into multiple segments or regions based on certain criteria, such as colour, intensity, or texture.
	    -Classify every pixel of an image as belonging to some class (tree, grass, cow)
    - **Example:** Identifying and outlining individual objects within an image.
    - **Applications:** Medical image analysis, autonomous navigation, and scene understanding
    
    - 1. **Semantic Segmentation:**
    
    - **Definition:** Semantic segmentation is a computer vision task that involves classifying each pixel in an image into predefined categories or classes, without distinguishing between different instances of the same class.
    - **Example:** In a street scene, semantic segmentation would label each pixel as road, sidewalk, car, pedestrian, etc., providing a detailed understanding of the scene at a pixel level.
    - **Applications:** Scene understanding, autonomous navigation, and image analysis where a detailed understanding of different parts of an image is necessary.
    
		2.**Instance Segmentation:**
    
    - **Definition:** Instance segmentation is a more advanced form of segmentation that not only categorises each pixel but also distinguishes between different instances of the same class. It assigns a unique identifier to each individual object instance in an image.
    - **Example:** In an image with multiple cars, instance segmentation would not only label each pixel as "car" but also assign a unique label or colour to each individual car, effectively distinguishing between them.
    - **Applications:** Robotics, autonomous vehicles, and any scenario where precise identification and tracking of individual objects in an image are essential.

- Classification



**Classification**
** Постановка задачи: ** Учитывая входное изображение, задача состоит в том, чтобы п**рисвоить ярлык или категорию всему изображению**.
- ** Пример:** Определение того, содержит ли изображение кошку или собаку.
- ** Приложения: ** Распознавание объектов, понимание сцен и категоризация изображений.

**Detection**
** Постановка задачи:** Определение местоположения и классификация объектов на изображении, часто **путем рисования ограничивающих рамок вокруг них**.
- ** Пример:** Обнаружение и локализация множества пешеходов, автомобилей и велосипедов на уличной сцене.
- ** Области применения:** Автономные транспортные средства, наблюдение и поиск по изображениям.

**Segmentation**
** Постановка задачи: ** Разделение изображения на несколько **сегментов или областей на основе определенных критериев, таких как цвет, интенсивность или текстура.**
-Классифицировать каждый пиксель изображения как принадлежащий к некоторому классу (дерево, трава, корова)
- ** Пример:** Идентификация и выделение отдельных объектов на изображении.
- ** Приложения: ** Анализ медицинских изображений, автономная навигация и понимание сцены

**Semantic Segmentation**
** Определение:** Семантическая сегментация - это задача компьютерного зрения, которая включает в себя классификацию каждого пикселя изображения по предопределенным категориям или классам без проведения различия между различными экземплярами одного и того же класса.
- ** Пример:** В уличной сцене семантическая сегментация помечает каждый пиксель как дорогу, тротуар, автомобиль, пешехода и т.д., обеспечивая детальное понимание сцены на уровне пикселей.
- ** Области применения:** Понимание сцены, автономная навигация и анализ изображений, где необходимо детальное понимание различных частей изображения.

**Сегментация экземпляра
**Определение: ** Сегментация экземпляра - это более продвинутая форма сегментации, которая не только классифицирует каждый пиксель, но и проводит различие между различными экземплярами одного и того же класса. Она присваивает уникальный идентификатор каждому отдельному экземпляру объекта на изображении.
- ** Пример:** На изображении с несколькими автомобилями сегментация экземпляра не только помечает каждый пиксель как "автомобиль", но и присваивает уникальную метку или цвет каждому отдельному автомобилю, эффективно различая их.
- ** Области применения: ** Робототехника, автономные транспортные средства и любые сценарии, где необходима точная идентификация и отслеживание отдельных объектов на изображении.
![[Pasted image 20240107194300.png]]
- Localization
![[Pasted image 20240107194343.png]]
- Detection
![[Pasted image 20240107194516.png]]
- Semantic Segmentation
![[Pasted image 20240107194655.png]]
- Instance Segmentation
![[Pasted image 20240107195100.png]]
- Image Generation
![[Pasted image 20240107195454.png]]
![[Pasted image 20240107195643.png]]
- Adversarial Attacks
![[Pasted image 20240107195802.png]]
![[Pasted image 20240107200117.png]]