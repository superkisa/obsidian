
**1. Question: What is the Bag of Words (BoW) model, and how does it represent text?**

- **Answer:** The BoW model represents text by counting the frequency of words in a document, disregarding word order and structure. It creates a vector where each element corresponds to a unique word in the corpus, and the value represents the frequency of that word in the document.

**2. Question: Explain the process of creating a Bag of Words representation for a document.**

- **Answer:** The process involves tokenization, creating a vocabulary of unique words, and counting the frequency of each word in the document. The resulting vector is a sparse representation where each element corresponds to a word, and the value is the count of that word in the document.

**3. Question: What are the limitations of the Bag of Words model?**

- **Answer:** The BoW model ignores word order, context, and semantics. It treats each document as an unordered set of words, which may lead to a loss of information, especially in tasks where word order and context are crucial.

### TF-IDF:

**4. Question: What does TF-IDF stand for, and how is it calculated?**

- **Answer:** TF-IDF stands for Term Frequency-Inverse Document Frequency. It is calculated by multiplying the term frequency (TF), which measures how often a term appears in a document, with the inverse document frequency (IDF), which measures the importance of a term across a collection of documents.

**5. Question: How does TF-IDF help in text representation?**

- **Answer:** TF-IDF helps in text representation by assigning weights to words based on their importance in a document relative to the entire corpus. Words that are frequent in a document but rare across the corpus receive higher weights, capturing their significance in the document.

**6. Question: Can TF-IDF values be directly used as feature vectors for machine learning models? Why or why not?**

- **Answer:** Yes, TF-IDF values can be used as feature vectors. They provide a numerical representation of the importance of each term in a document. However, they may need additional normalization or dimensionality reduction, depending on the specific requirements of the machine learning model.

**7. Question: In what type of NLP tasks is TF-IDF commonly applied?**

- **Answer:** TF-IDF is commonly applied in tasks such as document classification, information retrieval, and text mining, where understanding the importance of words in documents is crucial.

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