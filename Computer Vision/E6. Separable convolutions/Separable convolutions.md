Разделяемые свертки

Separable convolutions are a type of convolutional operation that decomposes a standard convolution into two simpler operations: a depthwise convolution and a pointwise convolution. This decomposition reduces the number of parameters and computations, making the model more efficient and potentially faster to train and run.

Разделяемые свертки - это тип сверточной операции, которая разлагает стандартную свертку на две более простые операции: глубинную свертку и поточечную свертку. Такая декомпозиция сокращает количество параметров и вычислений, делая модель более эффективной и потенциально более быстрой в обучении и запуске.

Here's a breakdown of the two components of separable convolutions:

1. **Depthwise Convolution:**
    
    - In a standard convolution, each input channel is convolved with a different filter, resulting in a separate set of output channels. Depthwise convolution, on the other hand, applies a separate filter for each input channel independently. Essentially, it performs a spatial convolution independently for each input channel.
    - This operation reduces the number of parameters compared to a standard convolution, as there is only one set of filters per input channel.
    - The output of the depthwise convolution has the same number of channels as the input.
2. **Pointwise Convolution:**
    
    - After the depthwise convolution, a pointwise convolution (1x1 convolution) is applied. This operation uses 1x1 filters to combine information from different channels.
    - Pointwise convolution helps capture complex relationships between channels, allowing the network to model more abstract features.
    - The output of the pointwise convolution has a different number of channels, which can be adjusted based on the desired model architecture.


**Свертка по глубине:**
    
    - В стандартной свертке каждый входной канал свертывается с помощью другого фильтра, что приводит к отдельному набору выходных каналов. Свертка по глубине, с другой стороны, применяет отдельный фильтр для каждого входного канала независимо. По сути, он выполняет пространственную свертку независимо для каждого входного канала.
    - Эта операция уменьшает количество параметров по сравнению со стандартной сверткой, поскольку на каждый входной канал приходится только один набор фильтров.
    - Выходной сигнал глубинной свертки имеет то же количество каналов, что и входной.
2. **Поточечная свертка:**
    
    - После свертки по глубине применяется поточечная свертка (свертка 1x1). В этой операции используются фильтры 1x1 для объединения информации из разных каналов.
    - Поточечная свертка помогает фиксировать сложные взаимосвязи между каналами, позволяя сети моделировать более абстрактные объекты.
    - Выходные данные поточечной свертки содержат различное количество каналов, которое может быть скорректировано в зависимости от желаемой архитектуры модели.



The overall operation of a separable convolution is the composition of these two steps: depthwise convolution followed by pointwise convolution. By separating spatial and channel-wise information, separable convolutions reduce the number of parameters and computations, leading to a more efficient and lightweight model.

This technique is often used in deep learning architectures, particularly in mobile and edge devices where computational resources are limited, and efficiency is crucial. Separable convolutions are a key component in architectures like MobileNet and Xception.


Общая операция разделяемой свертки представляет собой совокупность этих двух этапов: свертка по глубине, за которой следует поточечная свертка. Разделяя пространственную информацию и информацию о каналах, разделяемые свертки сокращают количество параметров и вычислений, что приводит к созданию более эффективной и облегченной модели.

Этот метод часто используется в архитектурах глубокого обучения, особенно в мобильных и периферийных устройствах, где вычислительные ресурсы ограничены, а эффективность имеет решающее значение. Разделяемые свертки являются ключевым компонентом в таких архитектурах, как Mobile Net и Exception.
----------------------------------------------

Let's suppose that we have kernel and can transform kernel in such way 

![[Pasted image 20240111175958.png]]

![[Pasted image 20240111180241.png]]

![[Pasted image 20240111180853.png]]

In the second image we have 256 chennels, because we apply 256 kernels 

![[Pasted image 20240111180955.png]]

Here we have less weights.

This works faster, but disadvantage is that we can't change number of channels..(

If you don;t want to overfit model with small data, use depthwise convolution

![[Pasted image 20240111181618.png]]

This approach used in ResNet, for instance.

It is a linear layer over channels.

[Источник](https://habr.com/ru/articles/347564/)
![[Pasted image 20240112191114.png]]
![[Pasted image 20240112191330.png]]

Еще [источник](https://puzzlelib.org/ru/documentation/base/modules/ConvND/)
![[Pasted image 20240112193502.png]]
![[Pasted image 20240112193522.png]]