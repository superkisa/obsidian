U-Net - это модель, которая решает задачу сегментации

![[Pasted image 20240111012950.png]]

The main difference between U-Net and other segmentation models is that this model provide feature map from every convolution stage to unconvolution stage.

Во всем остальном он схож с предшественниками, также снижает размерность, а потом увеличивает до размера картинки, чтобы меньше параметров хранить

Также использует upsampling methods, которые описаны в пункте E7.