**1. Question: Explain how Convolutional Neural Networks (CNNs) are adapted for text processing. What are the key components involved?**

Answer: In text processing, CNNs are adapted by using one-dimensional convolutions to capture local patterns and relationships within sequential data. The key components include convolutional layers, pooling layers, and fully connected layers. Convolutional filters slide over input sequences to extract relevant features, and pooling layers downsample the output, preserving important information.

**2. Question: Describe the architecture of a typical CNN for text classification.**

Answer: A typical CNN for text classification comprises an embedding layer to convert words into vectors, one or more convolutional layers with activation functions (e.g., ReLU), pooling layers for downsampling, and fully connected layers for classification. The model processes text hierarchically, learning local and global features to make predictions.

**3. Question: How do convolutional filters capture local features in text data?**

Answer: Convolutional filters slide over sequential data, capturing local features by learning patterns of neighboring words. The filters operate on small windows of input data, allowing the network to recognize meaningful sequences of words that contribute to the overall understanding of the text.

**4. Question: Explain the purpose of pooling layers in a text processing CNN.**

Answer: Pooling layers in a text processing CNN serve to downsample the spatial dimensions of the data obtained from convolutional layers. Commonly used pooling operations include max pooling, which extracts the maximum value from each region, preserving the most significant features. Pooling helps reduce the computational load and retains important information.

**5. Question: How can CNNs be used for sentiment analysis in text data?**

Answer: For sentiment analysis, CNNs can learn hierarchical features from text. The model processes input sequences, capturing local patterns and global context to understand sentiment. The final fully connected layers are designed for binary (positive/negative) or multi-class classification (positive, neutral, negative).

**6. Question: Discuss a potential limitation of using CNNs in text processing.**

Answer: One limitation of CNNs in text processing is their fixed-size receptive fields. Convolutional filters are designed to capture patterns within a specified window size, making it challenging for the model to handle variable-length sequences effectively. This limitation is often addressed by using padding or combining CNNs with recurrent architectures.

**7. Question: How do CNNs contribute to feature learning in text data, and how does this aid in downstream NLP tasks?**

Answer: CNNs contribute to feature learning by automatically extracting hierarchical features from text data. Local patterns, such as n-grams or key phrases, are captured during convolution, aiding the model's understanding of the input. These learned features can be beneficial for various downstream NLP tasks, such as sentiment analysis, named entity recognition, and text classification.