
**1. Question: Explain the concept of word embeddings and why they are important in Natural Language Processing (NLP).**

Answer: Word embeddings are numerical representations of words in a continuous vector space. They capture semantic relationships between words and are crucial in NLP because they enable machines to understand the contextual meanings of words, allowing for more effective language processing tasks.

**2. Question: Compare and contrast CBOW and Skip-Gram architectures in Word2Vec. How does each architecture approach the task of learning word representations?**

Answer: CBOW predicts the target word based on its context words, taking the average of the context word vectors. Skip-Gram, on the other hand, predicts context words given the target word. CBOW is computationally efficient and works well for frequent words, while Skip-Gram is effective for capturing semantic relationships and performs well for infrequent words.

**3. Question: What is negative sampling in the context of Word2Vec, and why is it used?**

Answer: Negative sampling is a training technique in Word2Vec that reduces computational complexity. Instead of adjusting all non-target words' weights during training, negative sampling randomly selects a small number of negative samples (words not in the context) and updates their weights. This makes the training process more efficient while preserving the quality of learned word embeddings.

**4. Question: Discuss the properties of Word2Vec embeddings, including semantic similarity, analogies, and vector arithmetic. Provide examples to illustrate each property.**

Answer: Word2Vec embeddings exhibit semantic similarity, meaning words with similar meanings have similar vectors. They also demonstrate analogy relationships, e.g., "king" - "man" + "woman" ≈ "queen." Vector arithmetic operations like addition and subtraction produce meaningful results, showcasing the model's ability to capture linguistic regularities.

**5. Question: How does Word2Vec leverage contextual information in learning word representations?**

Answer: Word2Vec uses contextual information by considering the surrounding words of a target word. The model learns to associate words based on their context, capturing the nuances of word semantics. This contextual understanding allows Word2Vec to generate embeddings that reflect the meaning of words in diverse contexts.

**6. Question: Explain the significance of Word2Vec embeddings in practical NLP applications. Provide examples of tasks where Word2Vec embeddings can be beneficial.**

Answer: Word2Vec embeddings are valuable in NLP applications such as sentiment analysis, machine translation, and named entity recognition. They enhance the performance of these tasks by providing meaningful representations of words, allowing models to better understand and generalize from the input data.