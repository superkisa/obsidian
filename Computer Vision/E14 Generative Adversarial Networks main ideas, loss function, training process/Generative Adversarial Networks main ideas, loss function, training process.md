![[Pasted image 20240111011106.png]]
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
