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