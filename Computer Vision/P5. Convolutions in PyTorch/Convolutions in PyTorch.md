![[sem2_cv_init.ipynb]]

Лажовый [вебинар](https://youtu.be/K2QVHTaAmPc?si=tAXwRJ7JFgy5On-U) от Марата про реализацию сверточных слоев в нумпае и пайторче

#### Convolution NN
![[convolution-operation-on-a-mxnx3-image-matrix-with-a-3x3x3-kernel.gif]]

Сверточные нейронные сети (Convolutional Neural Networks, CNN) - это тип сверточной нейронной сети, который часто используется в компьютерном зрении. CNN используют серию слоев свертки и пулинга для извлечения признаков из изображений и видео, а затем используют эти признаки для классификации или обнаружения объектов или сцен [3](https://www.geeksforgeeks.org/introduction-convolution-neural-network/amp/).

Сверточная нейронная сеть состоит из нескольких слоев, включая входной слой, один или несколько сверточных слоев, пулинговые слои и полносвязные слои. Сверточный слой применяет фильтры к входному изображению для извлечения признаков, пулинговый слой уменьшает размерность изображения для уменьшения вычислительной сложности, а полносвязный слой делает окончательное предсказание [3](https://www.geeksforgeeks.org/introduction-convolution-neural-network/amp/).

В CNN, каждый нейрон в сверточном слое связан только с небольшим регионом входного изображения, называемым его "принимающей областью". Это позволяет сетям обучаться на больших изображениях, используя относительно небольшое количество параметров, что делает их эффективными для обработки изображений [2](https://www.ibm.com/topics/convolutional-neural-networks).

1. **Parameter Sharing**: CNNs use convolutional filters to scan the input image, which greatly reduces the number of parameters, making the network easier to train.
	   Parameter sharing, или обмен параметрами, - это концепция, используемая в сверточных нейронных сетях (CNN), которая позволяет существенно уменьшить количество параметров модели, что делает сеть легче для обучения [5](https://www.geeksforgeeks.org/parameter-sharing-and-typing-in-machine-learning/).
	   
	В обычной полносвязной нейронной сети каждый нейрон в слое связан с каждым входным нейроном, что приводит к большому числу параметров. В сверточных нейронных сетях, однако, каждый нейрон в сверточном слое связан только с небольшой областью входного изображения, называемой его "принимающей областью". Это означает, что каждый нейрон в сверточном слое использует одни и те же параметры (фильтр) для анализа различных областей изображения, что позволяет существенно уменьшить общее число параметров в сети [3](https://ai.stackexchange.com/questions/28320/how-is-parameter-sharing-done-in-cnn).
	
	Благодаря обмену параметров, CNN могут учиться распознавать общие свойства изображений, такие как линии, края и текстуры, независимо от их местоположения на изображении. Это делает CNN очень эффективными для работы с изображениями, поскольку они могут использовать одно и то же представление для различных частей изображения [5](https://www.geeksforgeeks.org/parameter-sharing-and-typing-in-machine-learning/).
	
	Однако стоит отметить, что обмен параметров не всегда является преимуществом. В некоторых случаях, когда конкретные свойства изображения важны для распознавания (например, положение объекта на изображении), обмен параметров может привести к ухудшению производительности модели [3](https://ai.stackexchange.com/questions/28320/how-is-parameter-sharing-done-in-cnn).
2. **Local Connectivity**: Each neuron is connected to only a local region of the input, capturing local patterns effectively.
	Локальная связность в сверточных нейронных сетях (CNN) - это концепция, которая позволяет каждому нейрону быть связанным только с небольшим локальным регионом входного изображения, вместо того, чтобы быть связанным с каждым нейроном в предыдущем слое, как в полносвязных нейронных сетях [1](https://stats.stackexchange.com/questions/159588/how-does-local-connection-implied-in-the-cnn-algorithm).
	
	Это означает, что каждый нейрон в сверточном слое обрабатывает только небольшую часть входного изображения, что позволяет CNN эффективно извлекать локальные признаки из изображения. Например, сверточный слой может обрабатывать только небольшую область изображения, чтобы определить, является ли эта область краем или границей объекта [1](https://stats.stackexchange.com/questions/159588/how-does-local-connection-implied-in-the-cnn-algorithm).
3. **Translation Invariance**: Due to the sliding filter operation, CNNs can detect patterns regardless of their position in the image.
	Translation Invariance, или инвариантность к переносу, - это свойство сверточных нейронных сетей (CNN), которое позволяет им обнаруживать шаблоны независимо от их позиции на изображении. Это достигается благодаря операции сдвига, которую выполняет сверточный слой [1](https://stats.stackexchange.com/questions/208936/what-is-translation-invariance-in-computer-vision-and-convolutional-neural-netwo).
	
	Сверточный слой в CNN применяет фильтры к входному изображению, сдвигая их по всему изображению. Это означает, что каждый фильтр проверяет различные области изображения, что позволяет обнаруживать шаблоны, независимо от их расположения на изображении. Например, если мы ищем красный цвет на изображении, сверточный слой сможет обнаружить красный цвет, независимо от того, находится ли красный цвет в верхнем левом углу, центре или нижнем правом углу изображения [1](https://stats.stackexchange.com/questions/208936/what-is-translation-invariance-in-computer-vision-and-convolutional-neural-netwo).
4. **Hierarchical Feature Learning**: CNNs learn hierarchical features, with lower layers capturing simple patterns and deeper layers capturing more complex patterns.
	Hierarchical Feature Learning, или иерархическое обучение признаков, - это концепция, которая используется в сверточных нейронных сетях (CNN), чтобы улучшить способность сети распознавать сложные шаблоны на изображениях.
	
	В иерархическом обучении признаков, сеть обучается распознавать простые шаблоны на ранних слоях (так называемые "низкоуровневые" слои), а затем использует эти простые шаблоны для распознавания более сложных шаблонов на более глубоких слоях (так называемые "высокоуровневые" слои).
	
	Например, низкоуровневые слои могут быть обучены распознавать простые геометрические формы, такие как линии и края, в то время как более глубокие слои могут быть обучены распознавать более сложные формы, такие как лица или автомобили. Это позволяет сетям обучаться распознавать более сложные объекты, используя простые, уже известные шаблоны [3](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Yan_HD-CNN_Hierarchical_Deep_ICCV_2015_paper.pdf).
	
	Иерархическое обучение признаков также позволяет сетям лучше адаптироваться к новым данным. Когда сеть сталкивается с новым объектом, который она ранее не видела, она может использовать свои уже изученные простые шаблоны для начала распознавания этого нового объекта, а затем продолжать обучение на более сложных уровнях для улучшения своего распознавания [5](https://ai.stackexchange.com/questions/31972/when-can-we-call-a-feature-hierarchical).

#### **Params of the layer**
https://pytorch.org/docs/stable/generated/torch.nn.Conv2d.html
input: $H \times W \times C_{in}$
1. Kernel\_size $\longrightarrow$ $[K_{h} \times K_{w}]$
2. Input and output channels $\longrightarrow$ $[C_{in}$, $C_{out}]$
3. Padding $\longrightarrow$ how much zeroes (or other specified elements) should be added on each side of the image $[P$, default 0]
4. Stride $\longrightarrow$ distance between two adjacent positions of the kernel on the original image $[S$, default 1]
5. Dilation $\longrightarrow$ distance between each two adjacent elements inside the kernel $[D$, default 1]
6. Bias $\longrightarrow$ linear addition to each output channel $[B$, default True]
output: $H' \times W' \times C_{out}$

#### Model parameters
Depends on $K_h, K_w, C_{in}, C_{out}, B$
Actual kernel, moving across the image, has size $K_h \times K_w \times C_{in}$. Then, for each output channel we have one **different** kernel of this size and one bias value, if $B = \text{true}$
So, weights, corresponding to one convolutional layers are: $$((K_h * K_w * C_{in}) + B) * C_{out}$$
####
1. **Model parameters** $\longrightarrow$ How many params will model have if we'll use this conv layer, and what if we'll use 3 conv layers of one type, 10 of second type and 20 of third one? We can theoretically compute and analyze this things without any additional tools
	The number of parameters in a convolutional layer depends on the size of the filters, the stride, and the number of input channels. If we have a filter size of F x F, a stride of S, and an input with C channels, then the number of parameters in a single convolutional layer is (F x F x C) + C (for bias term). For instance, if we have three types of layers with 10 filters of size 3x3 each, we would have (3x3xC) + C * 10 = 3x3xC + 10C parameters. For the second type of layer, if we have 10 filters of size 5x5 each, we would have (5x5xC) + C * 10 = 5x5xC + 10C parameters. For the third type of layer, if we have 20 filters of size 7x7 each, we would have (7x7xC) + C * 20 = 7x7xC + 20C parameters [1](https://distill.pub/2019/computing-receptive-fields).
2. **$\Delta H, \Delta W, \Delta C$** $\longrightarrow$ What will happen to the image after going through this conv layer? Especially important when you want to stack **a lot** of them one after another or create atypical architecture
	**ΔH, ΔW, ΔC**: After passing through a convolutional layer, the height and width of the feature maps will be reduced depending on the stride and padding. If we use a stride of 1 and no padding, the height and width will remain the same. If we use a stride of 2 and no padding, the height and width will be halved. The depth of the feature maps will be equal to the number of filters applied. For instance, if we have 10 filters, the depth of the output will be 10 [1](https://distill.pub/2019/computing-receptive-fields).
3. **Receptive field** $\longrightarrow$ How to interpret model results and find what went wrong, or how exactly model solved the case? How big of a patterns model can phisically capture?
	 **Receptive field**: The receptive field of a convolutional layer refers to the region in the input space that contributes to the activation of a particular unit in the feature map. It can be calculated as the product of the strides of the convolutional layers. For instance, if we have a stride of 1 in the first layer, 2 in the second layer, and 3 in the third layer, the total receptive field would be 1 * 2 * 3 = 6. This means that the unit in the feature map is sensitive to the input within a 6x6 region [4](https://theaisummer.com/receptive-field/).

