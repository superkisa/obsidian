Upsampling или Unpooling - это метод противоположный pooling. То есть когда мы делали Max pooling, Avg pooling, мы снижали размерность, а здесь мы наоборот хотим ее увеличивать. Это нужно, например, для задачи сегментации в модели U-NET

## Pooling upsampling methods

![[Pasted image 20240110190321.png]]

![[Pasted image 20240110190421.png]]

## Transposed convolution

![[Pasted image 20240110190531.png]]


Transpose convolution is a technique used for upsampling or increasing the resolution of feature maps in neural networks. Let's delve a bit deeper into transpose convolution in simple terms:

1. **Basic Convolution Recap:**
    
    - In a regular convolution operation, a small filter (also called a kernel) moves over an input image or feature map, performing a series of multiplications and additions to produce an output (feature map). Each pixel in the output is influenced by a small region in the input.
2. **Transposed Convolution as Upsampling:**
    
    - Transposed convolution works in the opposite direction. Instead of going from input to output, it goes from output to input. It is used for upsampling or increasing the size of the feature map.
        
    - Imagine you have a small image, and you want to make it larger. Transposed convolution helps in this process by filling in the gaps and generating a higher-resolution version of the input.
        
3. **Learnable Parameters:**
    
    - Transposed convolution involves learnable parameters, just like regular convolution. These parameters are adjusted during the training process based on the error between the predicted and actual output. The network learns how to spread and refine information during upsampling.
    - Learnable parameters: filter weight, bias term, stride, padding
1. **Stride and Padding:**
    
    - Stride determines how much the filter moves between each operation. In transpose convolution, a stride greater than 1 can be used to increase the output size. Padding can also be applied to control the spatial dimensions of the output.
5. **Upsampling Factor:**
    
    - The upsampling factor is determined by the stride used in the transpose convolution operation. A larger stride leads to a larger upsampling factor, resulting in a more substantial increase in size.
6. **Use in Autoencoders and Generative Models:**
    
    - Transposed convolution is often employed in autoencoders and generative models (like Generative Adversarial Networks - GANs) for upsampling. In autoencoders, it helps reconstruct a higher-resolution version of the input, while in generative models, it aids in generating realistic images.

In summary, transpose convolution is a technique used in neural networks for increasing the resolution of feature maps. It involves a learnable operation that spreads and refines information to produce a higher-resolution output. This is particularly useful in tasks such as image generation, where the network needs to generate detailed and realistic images.

