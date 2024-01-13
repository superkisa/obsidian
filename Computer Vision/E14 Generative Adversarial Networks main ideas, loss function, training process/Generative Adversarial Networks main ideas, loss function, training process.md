[Ссылка](https://pyimagesearch.com/2021/09/13/intro-to-generative-adversarial-networks-gans/)
![[Pasted image 20240111011106.png]]


## Loss function
![[Pasted image 20240113001313.png]]
(пример со сравнением долларовой купюры)
In the end the **Generator** generates dollar bills indistinguishable from real ones and the **Discriminator** is forced to guess (with probability = 1/2).
NOTE: Both the Discriminator and Generator actually start from scratch meaning they are both randomly initialized at start and then simultaneously trained.
![[Pasted image 20240111181045.png]]
Среднее значение по всем обучающим примерам m.
Так как логарифм единицы равен нулю, то в начале $D(G(z^{(i)}))$ будет равен нулю.
Дескриминатор хочет максимизировать выражение $1-D(G(z^{(i)}))$, так как логарифм в таком случае даст ответ равный нулю. 
![[Pasted image 20240111181900.png]]
С точки зрения генератора мы хотим обмануть распознаватель и заставить его поверить, что генератор даёт реальное изображение, поэтому генератор стремится выражение $1-D(G(z^{(i)}))$ минимизировать.
Затем эти потери складываются вместе и получается выражение:
![[Pasted image 20240111182331.png]]
По формуле можно заметить, что по отношению к генератору эти значения необходимо минимизировать.
$x$ берётся из каких-то реальных данных. $z$ - ожидаемое значение, которое берётся из некоторого случайного распределения $z$.
Для упрощения обучения используется второй вариант (связано с получаемыми градиентами).

## **How GANs work**

GANs are a type of **generative** models, which observe many sample distributions and generate more samples of the same distribution. Other generative models include variational autoencoders ([VAE](https://arxiv.org/abs/1906.02691)) and [Autoregressive](https://arxiv.org/abs/1601.06759) models.

### **The GAN architecture**

There are two networks in a basic GAN architecture: the generator model and the discriminator model. GANs get the word **“adversarial”** in its name because the two networks are trained simultaneously and competing against each other, like in a zero-sum game such as chess.

The **generator** model generates new images. The goal of the generator is to generate images that look so real that it fools the discriminator. In the simplest GAN architecture for image synthesis, the input is typically random noise, and its output is a generated image.
![[Pasted image 20240111011532.png]]
The **discriminator** is just a binary image classifier which you should already be familiar with. Its job is to classify whether an image is real or fake.

**_Note:_** _In more complex GANs, we could condition the Discriminator with image or text for Image-to-Image translation or Text-to-Image generation)._
![[Pasted image 20240111011613.png]]
Putting it all together, here is what a basic GAN architecture looks like: the generator makes fake images; we feed both the real images (training dataset) and the fake images into the discriminator in separate batches. The discriminator then tells whether an image is real or fake.
![[Pasted image 20240111011653.png]]
### **Training GANs**

#### **The Minimax game: G vs. D**

Most deep learning models (for example, image classification) are based on optimization: finding the low value of the cost function. GANs are different because the two networks: the generator and discriminator, each has its own cost with opposite objectives:

- The generator tries to fool the discriminator into thinking the fake images as real
- The discriminator tries to classify real and fake images correctly

The minimax game math function below illustrates this adversarial dynamic during training.
![[Pasted image 20240111011845.png]]
Both the generator and discriminator improve over time during training. The generator gets better and better at producing images that resemble the training data, while the discriminator gets better at telling the real and fake images apart.

Training GANs is to find an **equilibrium** in the game when:

- The generator makes data that looks almost identical to the training data.
- The discriminator can no longer tell the difference between the fake images from the real images.
### **Image-to-image translation**

Image-to-image translation is a computer vision task that translates the input image to another domain (e.g., color or style) while preserving the original image content. This is perhaps one of the most important tasks to use GANs in art and design.

[Pix2Pix](https://arxiv.org/abs/1611.07004) (Image-to-Image Translation with Conditional Adversarial Networks) is a conditional GAN that was perhaps the most famous image-to-image translation GAN. However, one major drawback of Pix2Pix is that it requires paired training image datasets.
![[Pasted image 20240111012119.png]]
### **Text-to-Image**

We’ve seen a lot of Image-to-Image translation examples by GANs. We could also use words as the condition to generate images, which is much more flexible and intuitive than using class labels as the condition.

Combining NLP and computer vision has become a popular research area in recent years. Here are a few examples: [StyleCLIP](https://github.com/orpatashnik/StyleCLIP) and [Taming Transformers for High-Resolution Image Synthesis](https://arxiv.org/abs/2012.09841v3).
![[Pasted image 20240111012226.png]]


https://neptune.ai/blog/gan-loss-functions#:~:text=The%20standard%20GAN%20loss%20function%2C,of%20the%20loss%20seemed%20effective

-------------------------------------------
![[Pasted image 20240113110950.png]]

До этого был VAE

![[Pasted image 20240113111344.png]]

![[Pasted image 20240113111352.png]]

Во время декодирования модель пытается предсказать средний фон для лиц, так как фон - это не основное, что мы пытаемся закодировать.

![[Pasted image 20240113111951.png]]

![[Pasted image 20240113112018.png]]

Уберем часть с энкодером

![[Pasted image 20240113112047.png]]

![[Pasted image 20240113112057.png]]

То есть нам понадобится еще одна модель, которая будет говорить, хорошо получилась картинка или нет

![[Pasted image 20240113112321.png]]

![[Pasted image 20240113112341.png]]

![[Pasted image 20240113112359.png]]

То есть с одной стороны генератор хочет максимизировать вероятность, что пришла хорошая картинка, а классификатор, наоборот, хочет минимизировать и показать, что картинка пришла не из датасета, а со стороны 

![[Pasted image 20240113112534.png]]

![[Pasted image 20240113112648.png]]

![[Pasted image 20240113112733.png]]

![[Pasted image 20240113113014.png]]

Поэтому модель и называется состязательной, так как дискриминатор пытается уменьшить вероятность сгенерированной картинки быть хорошей, а генератор, наоборот, пытается генерировать хорошую картинку

![[Pasted image 20240113113200.png]]

Берем среднее по бачам

![[Pasted image 20240113113707.png]]

Сначала семплируем из латентного пространства что-то. пропускаем через генератор и получаем изображение

![[Pasted image 20240113113747.png]]

После этого мы говорим то, что сгенерировано генератором - у него метка будет 0, а то, что из датасета - 1. таким образом генерируем батчи, то есть допустим 16 картинок, берем 16 картинок из датасета. Конкатенируем их и получаем батч размером 32 с метками.

![[Pasted image 20240113114123.png]]



