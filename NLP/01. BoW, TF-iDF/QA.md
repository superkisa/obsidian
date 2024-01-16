
**1. Question: What is the Bag of Words (BoW) model, and how does it represent text?**

- **Answer:** The BoW model represents text by counting the frequency of words in a document, disregarding word order and structure. It creates a vector where each element corresponds to a unique word in the corpus, and the value represents the frequency of that word in the document.

**2. Question: Explain the process of creating a Bag of Words representation for a document.**

- **Answer:** The process involves tokenization, creating a vocabulary of unique words, and counting the frequency of each word in the document. The resulting vector is a sparse representation where each element corresponds to a word, and the value is the count of that word in the document.

**3. Question: What are the limitations of the Bag of Words model?**

- **Answer:** The BoW model ignores word order, context, and semantics. It treats each document as an unordered set of words, which may lead to a loss of information, especially in tasks where word order and context are crucial.

**2. Question: Discuss the trade-off between granularity and information loss in the Bag of Words model. Provide examples illustrating this trade-off.**

- **Answer:** The trade-off involves choosing the granularity of representation. Finer granularity captures more details but might lead to sparsity and overfitting. Coarser granularity reduces sparsity but results in information loss. For example, distinguishing between "run" and "running" captures details but increases sparsity.

**3. Question: Can the Bag of Words model handle out-of-vocabulary words effectively? Explain the challenges associated with out-of-vocabulary words in BoW representations.**

- **Answer:** BoW struggles with out-of-vocabulary words as they are not part of the predefined vocabulary. These words are either ignored or treated as unknown, leading to a loss of information. The challenge lies in adapting the model to handle new or rare words not present in the training set.

### TF-IDF:

**4. Question: What does TF-IDF stand for, and how is it calculated?**

- **Answer:** TF-IDF stands for Term Frequency-Inverse Document Frequency. It is calculated by multiplying the term frequency (TF), which measures how often a term appears in a document, with the inverse document frequency (IDF), which measures the importance of a term across a collection of documents.

**5. Question: How does TF-IDF help in text representation?**

- **Answer:** TF-IDF helps in text representation by assigning weights to words based on their importance in a document relative to the entire corpus. Words that are frequent in a document but rare across the corpus receive higher weights, capturing their significance in the document.

**6. Question: Can TF-IDF values be directly used as feature vectors for machine learning models? Why or why not?**

- **Answer:** Yes, TF-IDF values can be used as feature vectors. They provide a numerical representation of the importance of each term in a document. However, they may need additional normalization or dimensionality reduction, depending on the specific requirements of the machine learning model.

**7. Question: In what type of NLP tasks is TF-IDF commonly applied?**

- **Answer:** TF-IDF is commonly applied in tasks such as document classification, information retrieval, and text mining, where understanding the importance of words in documents is crucial.

**4. Question: Discuss the impact of document length on TF-IDF scores. How does document length normalization mitigate this impact, and what are its limitations?**

- **Answer:** Longer documents tend to have higher raw term frequencies, leading to higher TF-IDF scores. Document length normalization, such as dividing by the total number of words, mitigates this impact. However, it may not completely eliminate the bias, especially if document lengths vary significantly in the corpus.

**5. Question: In what scenarios might TF-IDF fail to capture the relevance of a term in a document? Provide examples and explain the limitations of TF-IDF in these cases.**

- **Answer:** TF-IDF may fail when terms have high frequency across the corpus or when they are present in short documents. For example, common words like "the" may get high scores. Additionally, TF-IDF may overlook the semantic similarity of terms, affecting its performance in capturing relevance.

**6. Question: How can the concept of term weighting be extended beyond TF-IDF for improved information retrieval? Provide alternatives and explain their advantages and disadvantages.**

- **Answer:** Alternatives include BM25, which adjusts for document length, and Okapi BM, which combines term frequency and document frequency. These models adapt term weighting for better information retrieval, considering factors like document length and term saturation. Each has its strengths and weaknesses, depending on the specific requirements.

**1. Вопрос: Что такое модель Bag of Words (BoW), и как она представляет текст?**

- **Ответ:** Модель BoW представляет текст путем подсчета частоты слов в документе, игнорируя порядок слов и структуру. Создается вектор, где каждый элемент соответствует уникальному слову в корпусе, а значение представляет собой частоту этого слова в документе.

**2. Вопрос: Объясните процесс создания представления Bag of Words для документа.**

- **Ответ:** Процесс включает в себя токенизацию, создание словаря уникальных слов и подсчет частоты каждого слова в документе. Результирующий вектор представляет собой разреженное представление, где каждый элемент соответствует слову, а значение - количеству этого слова в документе.

**3. Вопрос: Каковы ограничения модели Bag of Words?**

- **Ответ:** Модель BoW игнорирует порядок слов, контекст и семантику. Она рассматривает каждый документ как неупорядоченный набор слов, что может привести к потере информации, особенно в задачах, где порядок слов и контекст имеют важное значение.

### TF-IDF:

**4. Вопрос: Что означает аббревиатура TF-IDF, и как она рассчитывается?**

- **Ответ:** TF-IDF означает Term Frequency-Inverse Document Frequency. Рассчитывается умножением частоты термина (TF), которая измеряет, насколько часто термин встречается в документе, на обратную частоту документа (IDF), которая измеряет важность термина в коллекции документов.

**5. Вопрос: Как TF-IDF помогает в представлении текста?**

- **Ответ:** TF-IDF помогает в представлении текста, присваивая веса словам на основе их важности в документе относительно всего корпуса. Слова, часто встречающиеся в документе, но редкие в корпусе, получают более высокие веса, отражая их значимость в документе.

**6. Вопрос: Могут ли значения TF-IDF использоваться непосредственно в качестве векторов признаков для моделей машинного обучения? Почему да или почему нет?**

- **Ответ:** Да, значения TF-IDF могут использоваться в качестве векторов признаков. Они предоставляют числовое представление важности каждого термина в документе. Тем не менее, может потребоваться дополнительная нормализация или уменьшение размерности, в зависимости от конкретных требований модели машинного обучения.

**7. Вопрос: В каких типах задач NLP обычно применяется TF-IDF?**

- **Ответ:** TF-IDF обычно применяется в задачах, таких как классификация документов, информационный поиск и текстовый майнинг, где важно понимание значимости слов в документах.