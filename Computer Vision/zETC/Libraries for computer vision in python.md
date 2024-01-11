For different tasks is more convenient to choose library. For example: 

- • for augmentation is convenient to use OpenCV - there are built-in methods for this, 
- • PIL provides better antialiasing. 


*What is Antialiasing? 

In computer graphics, antialiasing is a technique used to smooth out the jagged edges of shapes and lines that are displayed on a screen. This is accomplished by applying a filter to the image that slightly blends the colors of the pixels near the edge of the shape or line with the background pixels, making the transition between the two less noticeable. 

Antialiasing can be applied to both vector graphics and raster images, and it is commonly used to improve the visual quality of text and graphics displayed on screens with low resolution. 

**OpenCV

language C++ is used with almost all languages: 

- • there is also support for apple, CUDA, etc., 
- • has bindings for java, python, etc.   

Custombinding for OpenCV is cv2 for python, it is now an official part of OpenCV. There is also a built-in for visualization - but not very stable and has problems, so better use matplotlib or plotly. 

Image data type 

numpy array - H x W x channels (in pytorch channels come first). 

BGR format (not RGB) - so we need to change colors (using cv2.cvtColor()). 

0 - always top left for all libraries. 

Image options: 

- • 0-255: 8U 
- • 0-65535 : 16U 
- • 0-1: 32F 
  

**Pillow (PIL Python Image Library) 

Only for python and optimized for Python. Sometimes faster than openCV, but in most cases openCV is faster. Pillow does not have as much functionality as OpenCV. 

It is better to download not just pillow, but also **pillow-SIMD**. It is single instruction multiple data (i.e. basic instructions to processors for adding, multiplication, ...). In SIMD this is done for all pairs (vector operations are done faster): 

- • GPU is more about SIMD (Single-Instruction-Multiple-Data) 
- • CPU is more about MIMD (Multiple-Instruction-Multiple-Data). 

  

More info on Flynn’s taxonomy 

In pillow there is the Image class, not a data type like in OpenCV but an object: 

import Image 

img = Image.open('image.jpeg') 

type(img) - does not contain the number of channels, because it is always assumed to be 3. 

To convert an object we just use numpy.array(img) - only unlike OpenCV we get RGB (not BGR). 

**Skimage (depends on Pillow, pure python) 

Provides extra functionality to pillow. Less efficient than OpenCV.