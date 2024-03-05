Image representation in computer. 

Image representation is the process of representing a digital image as a set of numbers. Each pixel is represented by a numerical value, which is usually: 

- • unit8, an 8-bit int number (0-255). 
- • float32 - with float values in [0,1] 

  The numerical values are used to determine the colour of the pixel. 

Представление изображения - это процесс представления цифрового изображения в виде набора чисел. Каждый пиксель представлен числовым значением, которое обычно равно: 

- • unit8, 8-разрядному числу int (0-255). 
- • float32 - со значениями с плавающей точкой в [0,1] 

  Числовые значения используются для определения цвета пикселя.



Dimentionality is defined as H, W, N 

H – height 
W – width 
N – number of channels (3 for RGB, 1 for greyscale) 

H – высота
W – ширина
N – количество каналов (3 для RGB, 1 для оттенков серого)

**Why do we store pixel values in int and not float?** 

The main reason is that you can lose precision with different operations (sum, multiple sum of pixels, etc.). That is, we do all operations on the image in int, and only normalize to 0-1 before feeding it into an NN. 

Основная причина заключается в том, что вы можете потерять точность при различных операциях (сумма, кратная сумме пикселей и т.д.). То есть мы выполняем все операции с изображением в int и нормализуем его только до 0-1, прежде чем передавать его в NN.

**Image channels.** 

An image channel is a single-colour component of an image. The most common image channels are red, green, and blue (RGB). 

RGB is a way of encoding colour by using primary colours. It is an additive mix by adding to black colour. Black (0,0,0) white (255, 255, 255) and accordingly all other RGB colours follow the same principle. Mixing all three in a certain proportion gives white.

Канал изображения - это одноцветный компонент изображения. Наиболее распространенными каналами изображения являются красный, зеленый и синий (RGB).

RGB - это способ кодирования цвета с использованием основных цветов. Это аддитивная смесь путем добавления к черному цвету. Черный (0,0,0), белый (255, 255,255) и, соответственно, все остальные цвета RGB следуют тому же принципу. Смешивание всех трех в определенной пропорции дает белый цвет.