VAEs were introduced in 2013 by Diederik et al. in their paper [Auto-Encoding Variational Bayes](https://arxiv.org/abs/1312.6114). They extended the idea of autoencoders to learn useful data distributions. Rooted in Bayesian inference, VAEs aim to model the underlying probability distribution of data, enabling the generation of new samples from that distribution.

The key distinction between VAEs and traditional autoencoders is the design of their latent spaces. VAEs ensure continuous latent spaces, facilitating random sampling and interpolation, making them invaluable for generative modeling.

In a standard autoencoder, every image corresponds to a singular point within the latent space. Conversely, as shown in **Figure 1**, in a variational autoencoder, each image is associated with a multivariate normal distribution centered around a specific point in the latent space.

![[Pasted image 20240112134607.png]]

VAEs are a type of autoencoder, designed to learn efficient input data codings or representations. However, unlike traditional autoencoders that learn deterministic encodings, VAEs introduce a probabilistic twist. The encoder in a VAE doesn’t produce a fixed point in the latent space. Instead, it outputs parameters (typically mean and variance) of a probability distribution, which we sample to obtain our latent representation.
#### [**Comparison with Convolutional Autoencoder**](https://pyimagesearch.com/2023/10/02/a-deep-dive-into-variational-autoencoders-with-pytorch/#TOC-h4Comparison)

---

##### [**Architecture**](https://pyimagesearch.com/2023/10/02/a-deep-dive-into-variational-autoencoders-with-pytorch/#TOC-h5Architecture)

- **Convolutional Autoencoder (CAE):** A CAE typically consists of an encoder and a decoder. The encoder uses convolutional layers to compress the input into a compact latent representation, and the decoder uses transposed convolutional layers to reconstruct the input from this representation.
- **VAE:** Similar to a CAE, a VAE also has an encoder and a decoder. However, the encoder in a VAE produces parameters of a probability distribution (typically Gaussian) in the latent space rather than a deterministic point, as shown in **Figure 2**.

![[Pasted image 20240112134700.png]]
##### [**Latent Space**](https://pyimagesearch.com/2023/10/02/a-deep-dive-into-variational-autoencoders-with-pytorch/#TOC-h5LatentSpace)

- **CAE:** The latent space in a CAE is deterministic. Given the same input, the encoder will always produce the same point in the latent space.
- **VAE:** The latent space in a VAE is probabilistic. The encoder produces a distribution’s parameters (mean and variance), and the actual latent representation is sampled from this distribution.

---

##### [**Loss Function**](https://pyimagesearch.com/2023/10/02/a-deep-dive-into-variational-autoencoders-with-pytorch/#TOC-h5LossFunction)

- **CAE:** The loss function of a CAE typically focuses on the reconstruction error, which measures the difference between the original input and its reconstruction.
- **VAE:** The VAE loss function has two components:
    - **Reconstruction Loss:** Like the CAE, this measures the fidelity of the reconstructed input.
    - **Kullback-Leibler (KL) Divergence:** This term ensures that the learned distribution in the latent space is close to a prior distribution, usually a standard Gaussian. It acts as a regularizer, preventing the model from encoding too much information in the latent space and ensuring smoothness in the latent space.
#### [**Why Does VAE Stand Out?**](https://pyimagesearch.com/2023/10/02/a-deep-dive-into-variational-autoencoders-with-pytorch/#TOC-h4StandOut)

VAEs have garnered attention due to their ability to learn smooth and continuous latent spaces. This continuity ensures that small changes in the latent space result in coherent changes in the generated data, making VAEs suitable for tasks like interpolation between data points. Additionally, the probabilistic nature of VAEs introduces a level of randomness that can benefit generative tasks, allowing the model to produce diverse outputs.

---

#### [**Why Does the Encoder of a VAE Follow a Gaussian Distribution?**](https://pyimagesearch.com/2023/10/02/a-deep-dive-into-variational-autoencoders-with-pytorch/#TOC-h4Gaussian)

- **Regularization and Continuity:** The Gaussian distribution acts as a regularizer, ensuring the latent space is continuous. This continuity allows for smooth interpolations between data points, making it possible to generate new, similar data points by sampling from regions between known data points.
- **Simplicity and Universality:** The Gaussian distribution is mathematically tractable and is a universal approximator. VAEs can leverage their properties for efficient training and representation by constraining the latent variables to follow this distribution.
- **Reparameterization Trick:** The Gaussian distribution facilitates the reparameterization trick, a crucial component in VAEs. This trick allows for the backpropagation of gradients through the stochastic sampling process, enabling end-to-end training of the model.
- **Balanced Latent Space:** By pushing the encoder’s outputs to approximate a standard Gaussian distribution, VAEs prevent the model from assigning too much importance to any particular region of the latent space. This ensures a balanced representation where different regions of the space can be effectively utilized for data generation.

---

#### [**Objective Functions of VAE**](https://pyimagesearch.com/2023/10/02/a-deep-dive-into-variational-autoencoders-with-pytorch/#TOC-h4ObjectiveFunctions)

VAEs optimize two primary loss functions:

**Reconstruction Loss:** This loss ensures that the images generated by the decoder closely resemble the input images. It’s typically computed using the Mean Squared Error (MSE) between the original and reconstructed images.

![L_\text{MSE}(\theta,\phi) = \displaystyle\frac{1}{N}\sum_{i=1}^{N}{\left(x_i -f_\theta (g_\phi (x_i))\right)^2}](https://b2633864.smushcdn.com/2633864/wp-content/latex/67d/67d7e6c31558343cdc040c66ad345fdf-ffffff-000000-0.png?size=266x49&lossy=2&strip=1&webp=1 "L_\text{MSE}(\theta,\phi) = \displaystyle\frac{1}{N}\sum_{i=1}^{N}{\left(x_i -f_\theta (g_\phi (x_i))\right)^2}")

- ![L_\text{MSE}(\theta ,\phi)](https://b2633864.smushcdn.com/2633864/wp-content/latex/818/818f98a590dbf69596d717dbbc5149b8-ffffff-000000-0.png?size=74x18&lossy=2&strip=1&webp=1 "L_\text{MSE}(\theta ,\phi)") represents the reconstruction loss.
- ![\theta](https://b2633864.smushcdn.com/2633864/wp-content/latex/255/2554a2bb846cffd697389e5dc8912759-ffffff-000000-0.png?size=8x11&lossy=2&strip=1&webp=1 "\theta") and ![\phi](https://b2633864.smushcdn.com/2633864/wp-content/latex/1ed/1ed346930917426bc46d41e22cc525ec-ffffff-000000-0.png?size=10x14&lossy=2&strip=1&webp=1 "\phi") are the parameters of the decoder and encoder, respectively.
- ![N](https://b2633864.smushcdn.com/2633864/wp-content/latex/8d9/8d9c307cb7f3c4a32822a51922d1ceaa-ffffff-000000-0.png?size=15x11&lossy=2&strip=1&webp=1 "N") is the number of samples.
- ![x_i](https://b2633864.smushcdn.com/2633864/wp-content/latex/1ba/1ba8aaab47179b3d3e24b0ccea9f4e30-ffffff-000000-0.png?size=13x10&lossy=2&strip=1&webp=1 "x_i") is the original input image.
- ![f_\theta](https://b2633864.smushcdn.com/2633864/wp-content/latex/f95/f95dbc5e6ca7517c76671b7b2f72474f-ffffff-000000-0.png?size=14x14&lossy=2&strip=1&webp=1 "f_\theta") is the decoder function, and ![g_\phi](https://b2633864.smushcdn.com/2633864/wp-content/latex/1a6/1a6317a7865929248bc6b1e3e0469bde-ffffff-000000-0.png?size=15x12&lossy=2&strip=1&webp=1 "g_\phi") is the encoder function.
- The formula calculates the squared difference between each original image ![x_i](https://b2633864.smushcdn.com/2633864/wp-content/latex/1ba/1ba8aaab47179b3d3e24b0ccea9f4e30-ffffff-000000-0.png?size=13x10&lossy=2&strip=1&webp=1 "x_i") and its corresponding reconstructed image ![f_\theta (g_\phi(x_i))](https://b2633864.smushcdn.com/2633864/wp-content/latex/7cf/7cf5d85e6a6f949b63da203c387a4fd9-ffffff-000000-0.png?size=68x19&lossy=2&strip=1&webp=1 "f_\theta (g_\phi(x_i))"), then averages these squared differences over all samples.

**KL Divergence:** This measures the difference between the encoder’s distribution and a standard normal distribution. It is a regularizer, ensuring the latent variables are close to a standard normal distribution. It encourages the model to maintain a structured and continuous latent space, which is particularly beneficial for generative tasks.

![L_\text{KL}[G(Z_{\mu}, Z_{\sigma})  |  \mathcal{N}(0, 1)] = -0.5 * \sum_{i=1}^{N}{1 + \log(Z_{\sigma_{i}^2}) - Z_{\mu_{i}}^2 -  Z_{\sigma_{i}}^2}](https://b2633864.smushcdn.com/2633864/wp-content/latex/4e0/4e060015dd5a90a210fac12cd6c9157b-ffffff-000000-0.png?size=448x24&lossy=2&strip=1&webp=1 "L_\text{KL}[G(Z_{\mu}, Z_{\sigma})  |  \mathcal{N}(0, 1)] = -0.5 * \sum_{i=1}^{N}{1 + \log(Z_{\sigma_{i}^2}) - Z_{\mu_{i}}^2 -  Z_{\sigma_{i}}^2}")

- ![L_\text{KL}](https://b2633864.smushcdn.com/2633864/wp-content/latex/1f1/1f150fbeb1728057a59d67d1aa0f9176-ffffff-000000-0.png?size=27x15&lossy=2&strip=1&webp=1 "L_\text{KL}") represents the KL divergence loss.
- ![G(Z_{\mu}, Z_{\sigma})](https://b2633864.smushcdn.com/2633864/wp-content/latex/f18/f189de5c0abefcdb20d60add2b74420e-ffffff-000000-0.png?size=69x19&lossy=2&strip=1&webp=1 "G(Z_{\mu}, Z_{\sigma})") is the Gaussian distribution defined by the encoder’s outputs ![Z_{\mu}](https://b2633864.smushcdn.com/2633864/wp-content/latex/3c3/3c3992a836dc10f16083f526c13b7f79-ffffff-000000-0.png?size=18x16&lossy=2&strip=1&webp=1 "Z_{\mu}") (mean) and ![Z_{\sigma}](https://b2633864.smushcdn.com/2633864/wp-content/latex/2e1/2e100224cae81152659641f4b9082080-ffffff-000000-0.png?size=18x14&lossy=2&strip=1&webp=1 "Z_{\sigma}") (standard deviation).
- ![\mathcal{N}(0, 1)](https://b2633864.smushcdn.com/2633864/wp-content/latex/3b3/3b3f99a5588e1cd0c235b04edc563f25-ffffff-000000-0.png?size=52x18&lossy=2&strip=1&webp=1 "\mathcal{N}(0, 1)") is the standard normal distribution.
- The formula calculates the difference between the encoder’s distribution and the standard normal distribution for each sample and sums these differences.

The combined VAE loss is a weighted sum of the reconstruction and KL divergence losses:

![\mathcal{L}_\text{VAE} = \mathcal{L}_\text{recon} + \mathcal{L}_\text{KL}](https://b2633864.smushcdn.com/2633864/wp-content/latex/331/3318c9bd2bc57d6b6777d1343bfaafb2-ffffff-000000-0.png?size=145x16&lossy=2&strip=1&webp=1 "\mathcal{L}_\text{VAE} = \mathcal{L}_\text{recon} + \mathcal{L}_\text{KL}")
#### [**Reparameterization Trick**](https://pyimagesearch.com/2023/10/02/a-deep-dive-into-variational-autoencoders-with-pytorch/#TOC-h4Reparameterization)

In the realm of Variational Autoencoder, one of the pivotal challenges is the integration of randomness in the latent space. This stochasticity, while essential for the VAE’s generative capabilities, poses a significant hurdle during training. Specifically, the sampling operation’s inherent randomness obstructs the smooth flow of gradients, making backpropagation infeasible.

This is where the reparameterization trick comes into play. It helps avoid the problem by transforming the random node in the latent space into a deterministic counterpart. Doing so ensures that gradients can propagate seamlessly through the network (**Figure 3**), facilitating effective training. The essence of the trick lies in introducing an auxiliary random variable, typically drawn from a standard normal distribution.

![[Pasted image 20240112134748.png]]

**Figure 3:** The reparameterization trick transforms a stochastic node into a deterministic one, facilitating gradient flow (source: image designed by the author for the [LearnOpenCV Blog](https://learnopencv.com/wp-content/uploads/2020/11/reparam-vae-2048x959.jpg)).

Mathematically, this can be represented as:

![Z = Z_\mu + Z_\sigma^2 \odot \varepsilon](https://b2633864.smushcdn.com/2633864/wp-content/latex/52d/52d342b2d22e73d7f2204133a35cc40b-ffffff-000000-0.png?size=120x19&lossy=2&strip=1&webp=1 "Z = Z_\mu + Z_\sigma^2 \odot \varepsilon")

Here, ![\varepsilon](https://b2633864.smushcdn.com/2633864/wp-content/latex/f8b/f8b1c5a729a09649c275fca88976d8dd-ffffff-000000-0.png?size=8x7&lossy=2&strip=1&webp=1 "\varepsilon") is sampled from a standard normal distribution, that is, ![\varepsilon \sim \mathcal{N}(0, 1)](https://b2633864.smushcdn.com/2633864/wp-content/latex/be3/be3f6fb4d31886a209ebafdc65802c1c-ffffff-000000-0.png?size=81x18&lossy=2&strip=1&webp=1 "\varepsilon \sim \mathcal{N}(0, 1)"). The symbol ![\odot](https://b2633864.smushcdn.com/2633864/wp-content/latex/319/319d584a4a5166ee6c51f4b8348856ea-ffffff-000000-0.png?size=11x12&lossy=2&strip=1&webp=1 "\odot") stands for element-wise multiplication.

By adopting this approach, the VAE can harness the benefits of randomness in the latent space while still maintaining the tractability of training. This balance is crucial for the VAE’s dual objectives of accurate reconstructions and effective generation.

Having delved deep into the theoretical underpinnings of VAE, it’s time to bring that knowledge to life. We’ll embark on a comprehensive code walkthrough in the next segment, demystifying each component step-by-step. Following that, we’ll dive into some exciting experiments, showcasing the prowess of our trained VAE in action.

------------------------------

![[Pasted image 20240113011806.png]]

![[Pasted image 20240113011815.png]]

![[Pasted image 20240113011837.png]]

Sampler берет и создает латентное пространство с помощью семплирования

![[Pasted image 20240113011916.png]]

![[Pasted image 20240113011933.png]]

Мы хотим, чтобы все mu были равны 0

![[Pasted image 20240113012005.png]]

Почему взяли такой лосс?

![[Pasted image 20240113012059.png]]

![[Pasted image 20240113012142.png]]

