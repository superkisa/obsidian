
**Key points**
- Kullback-Leibler (KL) divergence, or relative entropy, is a metric used to compare two data distributions. It is a concept of information theory that contrasts the information contained in two probability distributions
- KL divergence is defined as the **number of bits required to convert one distribution into another**. The lower bound value is zero and is achieved when the distributions under observation are identical.
- When using KL divergence as the loss, the network optimises to bring the divergence value down to zero
- Applications:
	- monitoring data drift (when it is time to retrain a model)
	- loss function in neural networks (bring it to zero at training)
	- VAE variational auto-encoder optimisation (VAE projects input data onto a probability distribution)
		- The VAE architecture employs two loss functions: mean-squared error (MSE) to measure the image reconstruction loss and KL divergence to assess the statistical gap between the true and approximating distributions.
	- Generative adversarial networks 
		- uses KL divergence to create a comparable metric to evaluate whether the model is learning


**Ключевые моменты**
- Дивергенция Кульбака-Лейблера (KL), или относительная энтропия, - это показатель, используемый для сравнения двух распределений данных. Это концепция теории информации, которая противопоставляет информацию, содержащуюся в двух распределениях вероятности
- Расхождение KL определяется как **количество бит, необходимое для преобразования одного распределения в другое**. Значение нижней границы равно нулю и достигается, когда наблюдаемые распределения идентичны.
- При использовании расхождения KL в качестве потери сеть оптимизирует значение расхождения до нуля
- Приложения:
	- мониторинг дрейфа данных (когда приходит время переобучать модель)
	- функция потерь в нейронных сетях (сводит ее к нулю при обучении)
	- Оптимизация вариационного автокодера VAE (VAE проецирует входные данные на распределение вероятностей)
		- Архитектура VAE использует две функции потерь: среднеквадратичную ошибку (MSE) для измерения потерь при восстановлении изображения и расхождение KL для оценки статистического разрыва между истинным и аппроксимирующим распределениями.
	- Порождающие состязательные сети 
		- использует дивергенцию KL для создания сопоставимой метрики для оценки того, обучается ли модель



**Simple explanation**
Kullback-Leibler (KL) Divergence, often referred to as KL Divergence or relative entropy, is a measure of how one probability distribution diverges from a second, expected probability distribution. In simple terms, it tells us how different two probability distributions are from each other.

**Простое объяснение**
Дивергенция Кульбака-Лейблера (KL), часто называемая дивергенцией KL или относительной энтропией, является мерой того, насколько одно распределение вероятностей отличается от второго, ожидаемого распределения вероятностей. Простыми словами, это говорит нам о том, насколько два распределения вероятностей отличаются друг от друга.

Now, let's talk about its relation to cross-entropy:

### Cross-Entropy:
Cross-entropy is a concept commonly used in machine learning, especially in classification tasks. It measures the difference between two probability distributions while considering the labels or true probabilities of the events. The formula for cross-entropy between two probability distributions \( P \) and \( Q \) is:

Перекрестная энтропия - это концепция, обычно используемая в машинном обучении, особенно в задачах классификации. Она измеряет разницу между двумя распределениями вероятностей при рассмотрении меток или истинных вероятностей событий. Формула для перекрестной энтропии между двумя распределениями вероятностей \(P\) и \(Q\) является:

$$ H(P, Q) = - \sum_{i} P(i) \cdot \log(Q(i)) $$

### KL Divergence:
KL Divergence is related to cross-entropy but focuses on measuring the extra amount of information needed to encode events from one distribution when using the optimal code for another distribution. The formula for KL Divergence from \( P \) to \( Q \) is:

Расхождение KL связано с перекрестной энтропией, но фокусируется на измерении дополнительного объема информации, необходимого для кодирования событий из одного распределения при использовании оптимального кода для другого распределения. Формула для расхождения KL от \(P\) до \(Q\) такова:

$$ D_{KL}(P \parallel Q) = \sum_{i} P(i) \cdot \log\left(\frac{P(i)}{Q(i)}\right) $$

### Relation:
The key connection is that the cross-entropy between \( P \) and \( Q \) is composed of two parts: the entropy of \( P \) and the KL Divergence from \( P \) to \( Q \). The formula for cross-entropy can be expressed as:

$$ H(P, Q) = H(P) + D_{KL}(P \parallel Q) $$

- \( H(P) \) is the entropy of distribution \( P \).
- $$D_{KL}(P \parallel Q) $$ is the KL Divergence from \( P \) to \( Q \).

In simpler terms, when you calculate cross-entropy, you can think of it as two components: how surprised you are on average (entropy) and how much extra you need to know about \( P \) to encode it optimally using \( Q \) (KL Divergence). The KL Divergence term captures the extra information needed to move from one distribution to another.

In practical terms, minimizing cross-entropy during training often translates to making the predicted probability distribution (Q) as close as possible to the true distribution (P), which is a common goal in many machine learning tasks.


Ключевая связь заключается в том, что перекрестная энтропия между \(P\) и \(Q\) состоит из двух частей: энтропии \(P\) и расхождения KL от \(P\) до \(Q\). Формула для перекрестной энтропии может быть выражена следующим образом:

$$ H(P, Q) = H(P) + D_{KL}(P \параллельно Q) $$

- \(H(P)\) - энтропия распределения \(P\).
- $$D_{KL}(P \ параллельно Q) $$ - это расхождение KL от \(P\) до \(Q\).

Проще говоря, когда вы вычисляете перекрестную энтропию, вы можете думать о ней как о двух компонентах: насколько вы удивлены в среднем (энтропия) и сколько еще вам нужно знать о \ (P\), чтобы оптимально закодировать ее, используя \(Q\) (расхождение KL). Термин "Дивергенция KL" отражает дополнительную информацию, необходимую для перехода от одного распределения к другому.

На практике минимизация перекрестной энтропии во время обучения часто приводит к тому, что прогнозируемое распределение вероятностей (Q) максимально приближается к истинному распределению (P), что является общей целью во многих задачах машинного обучения.