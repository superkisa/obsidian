U-Net - это модель, которая решает задачу сегментации

![[Pasted image 20240111012950.png]]

The main difference between U-Net and other segmentation models is that this model provide feature map from every convolution stage to unconvolution stage.

Во всем остальном он схож с предшественниками, также снижает размерность, а потом увеличивает до размера картинки, чтобы меньше параметров хранить

Также использует upsampling methods, которые описаны в пункте E7.


**U-Net** is a type of convolutional neural network that was developed specifically for biomedical image segmentation. It's named U-Net because its architecture is symmetrical, forming a letter "U". The architecture consists of an encoder (downsampling) path and a decoder (upsampling) path [1](https://lmb.informatik.uni-freiburg.de/people/ronneber/u-net/).

Here's a detailed explanation of how U-Net works:
	1. **Encoder Path (Downsampling)**: The encoder path is the first half of the network. It's a series of convolutional layers, each followed by a rectified linear unit (ReLU) activation function and a 2x2 max pooling operation. The purpose of this path is to gradually reduce the spatial dimensions of the input image while increasing the depth of the feature maps. This allows the network to learn hierarchical features [3](https://developers.arcgis.com/python/guide/how-unet-works/).
	2. **Decoder Path (Upsampling)**: The decoder path is the second half of the network. It starts with an upsampling operation that doubles the spatial dimensions of the feature map, followed by a 2x2 convolution ("up-convolution") that halves the number of feature channels. The output of this operation is then concatenated with the correspondingly cropped feature map from the encoder path. This process is repeated, allowing the network to gradually increase the spatial dimensions of the feature map while decreasing the depth. The purpose of this path is to allow the network to make precise localizations in the input image [3](https://developers.arcgis.com/python/guide/how-unet-works/).
	3. **Final Layer**: At the final layer of the network, a 1x1 convolution is used to map each feature vector to the desired number of classes. This forms the output of the network, which represents the probabilities of each pixel belonging to each class [5](https://paperswithcode.com/method/u-net).

U-Net was initially designed for biomedical image segmentation, but it has since found applications in many other areas due to its ability to handle both small and large datasets effectively [4](https://www.geeksforgeeks.org/u-net-architecture-explained/).