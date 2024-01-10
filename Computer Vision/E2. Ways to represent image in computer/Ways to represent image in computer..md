## Techniques

There are several common techniques for image representation in computer vision:

**Grayscale representation:** Images are represented using a single channel where each pixel contains a grayscale value ranging from 0 (black) to 255 (white). This representation is commonly used for tasks that do not require color information.

**Color representation:** For color images, the most common representation is the RGB (Red, Green, Blue) format. Each pixel is represented by three color channels (R, G, and B), with each channel containing an intensity value ranging from 0 to 255.

**Feature extraction:** Instead of using raw pixel values, computer vision algorithms often extract relevant features from images. These features can be edges, corners, textures, or more complex representations like histograms of oriented gradients (HOG) or deep features from convolutional neural networks (CNNs).

**Histograms**: Image histograms represent the frequency distribution of pixel intensities in an image. They can provide valuable information about the image's contrast, brightness, and overall content.

**Local descriptors:** These are representations that describe local regions of an image, such as SIFT (Scale-Invariant Feature Transform) and SURF (Speeded-Up Robust Features), which are used for object recognition and matching.

**Global descriptors:** These representations describe the entire image and are often used for image classification tasks. Examples include bag-of-words models, histogram of gradients (HOG), and deep learning-based features like activations from pre-trained CNN models.

**Deep Learning-based Representations:** Convolutional neural networks (CNNs) have revolutionized image representation in recent years. CNNs automatically learn hierarchical representations from images, enabling them to capture complex patterns and features effectively.

The choice of image representation depends on the specific computer vision task at hand. Different representations may be more suitable for different applications, and the selection of the most appropriate representation significantly impacts the performance and accuracy of the computer vision system.
[Source](https://medium.com/@sumit-kr-sharma/image-representation-in-computer-vision-364e47c4e69a) (VPN)