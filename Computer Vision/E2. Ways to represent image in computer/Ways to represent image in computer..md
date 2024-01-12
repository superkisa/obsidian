## Techniques

[Source](https://medium.com/@sumit-kr-sharma/image-representation-in-computer-vision-364e47c4e69a) (VPN)
There are several common techniques for image representation in computer vision:

**Grayscale representation:** Images are represented using a single channel where each pixel contains a grayscale value ranging from 0 (black) to 255 (white). This representation is commonly used for tasks that do not require colour information.

**Colour representation:** For colour images, the most common representation is the RGB (Red, Green, Blue) format. Each pixel is represented by three colour channels (R, G, and B), with each channel containing an intensity value ranging from 0 to 255.

**Histograms**: Image histograms represent the frequency distribution of pixel intensities in an image. They can provide valuable information about the image's contrast, brightness, and overall content.

**Local descriptors:** These are representations that describe local regions of an image, such as SIFT (Scale-Invariant Feature Transform) and SURF (Speeded-Up Robust Features), which are used for object recognition and matching.

**Global descriptors:** These representations describe the entire image and are often used for image classification tasks. Examples include bag-of-words models, histogram of gradients (HOG), and deep learning-based features like activations from pre-trained CNN models.

**Feature extraction:** Instead of using raw pixel values, computer vision algorithms often extract relevant features from images. These features can be edges, corners, textures, or more complex representations like histograms of oriented gradients (HOG) or deep features from convolutional neural networks (CNNs).

**Deep Learning-based Representations:** Convolutional neural networks (CNNs) have revolutionized image representation in recent years. CNNs automatically learn hierarchical representations from images, enabling them to capture complex patterns and features effectively.

The choice of image representation depends on the specific computer vision task at hand. Different representations may be more suitable for different applications, and the selection of the most appropriate representation significantly impacts the performance and accuracy of the computer vision system.

[Color Spaces](https://medium.com/@livajorge7/the-science-of-color-understanding-color-spaces-in-image-processing-d0e238872a0c) (VPN)

**RGB Colour Space**

The RGB colour space is an additive colour model that is used to display colours on electronic displays, such as computer monitors and televisions. It uses three primary colors: red, green, and blue, to create all other colors. In the RGB color space, each color is represented by a combination of red, green, and blue values, ranging from 0 to 255.
![[Pasted image 20240112181855.png]]

 **CMYK Colour Space**

The CMYK colour space is a subtractive colour model that is used in print media. It uses four primary colours: cyan, magenta, yellow, and black (also known as key), to create all other colours. In the CMYK colour space, each colour is represented by a combination of cyan, magenta, yellow, and black values, ranging from 0 to 100.
![[Pasted image 20240112181820.png]]

**HSL Colour Space**

The HSL colour space is a colour model that is used to define colours based on their hue, saturation, and lightness. Hue is the actual colour of the object, saturation is the intensity of the colour, and lightness is how light or dark the colour is. In the HSL colour space, hue is represented by a degree value between 0 and 360, saturation is represented by a percentage value between 0% and 100%, and lightness is represented by a percentage value between 0% and 100%.
![[Pasted image 20240112182205.png]]

# Bayer filter

The raw images coming from the camera are bayerized. They are represented as a two-dimensional array, where individual pixels encode the intensity of blue, green, and red colors.

![Bayer filter](https://github.com/alexmelekhin/cv_course_2023/blob/main/seminars/seminar_01/data/bayer.jpeg?raw=1)

OpenCV allows you to convert such images into familiar three-channel images. This process is called debayerization or demosaicing.


Дописать треугольник цветов, картинки с цветовыми пространствами, фильтр Байера. 