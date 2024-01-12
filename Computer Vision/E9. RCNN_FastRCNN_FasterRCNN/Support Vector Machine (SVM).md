Support Vector Machines (SVMs) are a set of supervised learning methods used for classification, regression, and outlier detection. They are particularly effective in high-dimensional spaces and are still effective even when the number of dimensions is greater than the number of samples [3](https://scikit-learn.org/stable/modules/svm.html).

Here's a detailed explanation of how SVMs work:

1. **Training**: Given a set of labeled training data, the SVM learns to find the hyperplane that best separates the data into different classes. This hyperplane is defined by a set of weights and a bias term. The goal is to maximize the margin between the closest points from different classes, known as support vectors. These points lie on the boundary of the decision boundary and are used to define the hyperplane [1](https://monkeylearn.com/blog/introduction-to-support-vector-machines-svm/).

2. **Decision Function**: Once trained, the SVM uses the learned hyperplane to classify new instances. This is done by calculating the distance from the instance to the hyperplane and assigning it to the class that corresponds to the sign of this distance. For regression tasks, the SVM tries to minimize the sum of squared residuals, which is equivalent to finding the line of best fit [3](https://scikit-learn.org/stable/modules/svm.html).

3. **Kernel Trick**: While SVMs are capable of performing linear classification, they can also handle non-linear classification problems using a method called the kernel trick. This involves transforming the input data into a higher-dimensional space where it becomes linearly separable. Common kernels include linear, polynomial, radial basis function (RBF), and sigmoid kernels [2](https://en.wikipedia.org/wiki/Support_vector_machine).

4. **Regularization**: To prevent overfitting, especially when the number of features is much greater than the number of samples, SVMs often use a regularization term in the cost function. This term penalizes models with large weights, encouraging simpler models that are less likely to overfit [3](https://scikit-learn.org/stable/modules/svm.html).

SVMs are widely used in various fields, including text classification, bioinformatics, handwriting recognition, and medical diagnosis. They are also the basis for many other machine learning algorithms [1](https://monkeylearn.com/blog/introduction-to-support-vector-machines-svm/).

Rewrite