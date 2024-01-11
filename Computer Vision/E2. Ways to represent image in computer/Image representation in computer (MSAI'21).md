Image representation in computer. 

Image representation is the process of representing a digital image as a set of numbers. Each pixel is represented by a numerical value, which is usually: 

- • unit8, an 8-bit int number (0-255). 
- • float32 - with float values in [0,1] 

  The numerical values are used to determine the colour of the pixel. 

Dimentionality is defined as H, W, N 

H – height 
W – width 
N – number of channels (3 for RGB, 1 for greyscale) 

**Why do we store pixel values in int and not float?** 

The main reason is that you can lose precision with different operations (sum, multiple sum of pixels, etc.). That is, we do all operations on the image in int, and only normalize to 0-1 before feeding it into an NN. 

Image channels. 

An image channel is a single-colour component of an image. The most common image channels are red, green, and blue (RGB). 

RGB is a way of encoding colour by using primary colours. It is an additive mix by adding to black colour. Black (0,0,0) white (255, 255, 255) and accordingly all other RGB colours follow the same principle. Mixing all three in a certain proportion gives white.