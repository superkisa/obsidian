## Techniques

[Source](https://medium.com/@sumit-kr-sharma/image-representation-in-computer-vision-364e47c4e69a) (VPN)
There are several common techniques for image representation in computer vision:

**Grayscale representation:** Images are represented using a single channel where each pixel contains a grayscale value ranging from 0 (black) to 255 (white). This representation is commonly used for tasks that do not require color information.

**Color representation:** For color images, the most common representation is the RGB (Red, Green, Blue) format. Each pixel is represented by three color channels (R, G, and B), with each channel containing an intensity value ranging from 0 to 255.

**Feature extraction:** Instead of using raw pixel values, computer vision algorithms often extract relevant features from images. These features can be edges, corners, textures, or more complex representations like histograms of oriented gradients (HOG) or deep features from convolutional neural networks (CNNs).

**Histograms**: Image histograms represent the frequency distribution of pixel intensities in an image. They can provide valuable information about the image's contrast, brightness, and overall content.

**Local descriptors:** These are representations that describe local regions of an image, such as SIFT (Scale-Invariant Feature Transform) and SURF (Speeded-Up Robust Features), which are used for object recognition and matching.

**Global descriptors:** These representations describe the entire image and are often used for image classification tasks. Examples include bag-of-words models, histogram of gradients (HOG), and deep learning-based features like activations from pre-trained CNN models.

**Deep Learning-based Representations:** Convolutional neural networks (CNNs) have revolutionized image representation in recent years. CNNs automatically learn hierarchical representations from images, enabling them to capture complex patterns and features effectively.

The choice of image representation depends on the specific computer vision task at hand. Different representations may be more suitable for different applications, and the selection of the most appropriate representation significantly impacts the performance and accuracy of the computer vision system.

[Color Spaces](https://medium.com/@livajorge7/the-science-of-color-understanding-color-spaces-in-image-processing-d0e238872a0c) (VPN)

**RGB Color Space**

The RGB color space is an additive color model that is used to display colors on electronic displays, such as computer monitors and televisions. It uses three primary colors: red, green, and blue, to create all other colors. In the RGB color space, each color is represented by a combination of red, green, and blue values, ranging from 0 to 255.

 **CMYK Color Space**

The CMYK color space is a subtractive color model that is used in print media. It uses four primary colors: cyan, magenta, yellow, and black (also known as key), to create all other colors. In the CMYK color space, each color is represented by a combination of cyan, magenta, yellow, and black values, ranging from 0 to 100.

**HSL Color Space**

The HSL color space is a color model that is used to define colors based on their hue, saturation, and lightness. Hue is the actual color of the object, saturation is the intensity of the color, and lightness is how light or dark the color is. In the HSL color space, hue is represented by a degree value between 0 and 360, saturation is represented by a percentage value between 0% and 100%, and lightness is represented by a percentage value between 0% and 100%.