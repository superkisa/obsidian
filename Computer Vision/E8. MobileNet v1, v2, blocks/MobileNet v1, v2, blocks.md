MobileNet is the same as ResNet but with optimised convolutions

**MobileNetV1:** MobileNetV1 is designed for efficient image processing on mobile devices. It introduces depthwise separable convolutions and inverted residuals to reduce computational complexity, making it lightweight. It optimizes for model size and computational resources, striking a balance between efficiency and accuracy.

**MobileNetV2:** Building upon MobileNetV1, MobileNetV2 enhances performance by introducing linear bottlenecks, skip connections, and width and resolution multipliers. It achieves improved accuracy while maintaining computational efficiency, making it well-suited for real-time applications on mobile and edge devices. The design includes smarter ways of processing information and utilizing shortcuts, resulting in a more efficient and effective convolutional neural network architecture.

![[Pasted image 20240111182944.png]]

Watch Separable Convolutions to understand better DepthWise Conv and 1x1 Conv.
Сеть работает быстрее, за счет меньшего количества параметров и вычислений. Дает те же результаты, что и полноценная сверточная VGG (которая в разы сложнее по количеству параметров и вычислений). Также слои свертки разделенные на dw и pw менее склонны к переобучению, на ограниченном количестве данных. 

It achieves the same results as VGG

![[Pasted image 20240111183655.png]]

![[Pasted image 20240111183912.png]]
MobileNetV1 and MobileNetV2 are two versions of lightweight convolutional neural network (CNN) architectures designed for efficient deployment on mobile and edge devices. These architectures aim to provide a good balance between model accuracy and computational efficiency, making them suitable for real-time applications on devices with limited computational resources.

### MobileNetV1:

1. **Depthwise Separable Convolutions:**
    
    - MobileNetV1 introduces depthwise separable convolutions, which consist of two separate operations: depthwise convolution and pointwise convolution. This factorization reduces the number of parameters and computations compared to traditional convolutions.
2. ==**Inverted Residuals:**==
    
    - ==MobileNetV1 also introduces the concept of inverted residuals, where the input is first expanded to a higher-dimensional space, processed with depthwise separable convolutions, and then projected back to a lower-dimensional space. This design helps capture more complex features while maintaining efficiency.==
    чет какая-то лажа
1. **Parameter Efficiency:**
    
    - MobileNetV1 is designed to be parameter-efficient, making it suitable for mobile and edge devices with limited memory and processing power. It achieves a good trade-off between model size and accuracy.

### MobileNetV2:

1. **Inverted Residuals with Linear Bottlenecks:**
    
    - MobileNetV2 builds on the inverted residuals concept of MobileNetV1 but introduces linear bottlenecks. The linear bottleneck architecture helps retain more information during the network's forward pass, contributing to better feature representation.
2. **Inverted Residual Block with Skip Connections:**
    
    - MobileNetV2 incorporates skip connections in its inverted residual blocks, similar to those found in ResNet architectures. Skip connections help with the flow of gradients during backpropagation, enabling better training of deep networks.
3. **Linear Bottlenecks and Shortcut Connections:**
    
    - The combination of linear bottlenecks and shortcut connections allows MobileNetV2 to capture complex features effectively while maintaining efficiency. It achieves better accuracy compared to MobileNetV1 with a similar level of computational efficiency.
4. **Width Multiplier and Resolution Multiplier:**
    
    - MobileNetV2 introduces the notion of a width multiplier and a resolution multiplier. The width multiplier adjusts the number of channels in each layer, providing a trade-off between accuracy and computational cost. The resolution multiplier scales down the input image resolution, further reducing computation.

Both MobileNetV1 and MobileNetV2 have been widely adopted for various computer vision tasks on mobile and edge devices, including image classification, object detection, and image segmentation. MobileNetV2, in particular, improves upon the original design and is often preferred for its enhanced performance.
[Источник](https://habr.com/ru/articles/352804/)
V1:
![[Pasted image 20240112211735.png]]
V2:
![[Pasted image 20240112212300.png]]
![[Pasted image 20240112212355.png]]
![[Pasted image 20240112212416.png]]