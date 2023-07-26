## Word Embedding
Converts words to numerical vectors, capturing meanings of words within body of text
<img width="565" alt="Screenshot 2023-07-25 at 8 14 41 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/3ce92f02-d03c-4cba-9f46-c9ff3468f61d">

### Characteristics
1. Pools similar words; words with similar semantic meanings will have word embedding vectors with high cosine similarity. 
2. Massively reduce feature count and data sparsity

### How do we know when to use word embeddings vs. TF-IDF? 
One thing to consider is the size of the vocabulary and frequency of words. 
For a small vocabulary full of high-frequency words, TF-IDF is a good choice. 
For larger vocabularies full of low-frequency words, word embeddings are a good choice.

<img width="535" alt="Screenshot 2023-07-25 at 8 44 24 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/8231f944-fa19-43a8-966e-8d64a16b3f71">

<img width="535" alt="Screenshot 2023-07-25 at 8 44 33 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/76279c11-abe5-48e5-ace4-a0006eef6cbb">

Pooling layer (Average/Max) to aggregate multiple vectors into one. We can also weight them before aggregating 
First compute TF-IDF weight for each word in each document and multiply associated weights with associated word vectors. 
<img width="608" alt="Screenshot 2023-07-25 at 8 45 21 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/c95fb6da-b643-4050-a3d2-2cb4d0c4b431">

### Design decisions 
1. Should I use embeddings or not?
2. What dimensionality should I use?
3. Which pooling functions should I use?
4. Should I weigh the individual word vectors? 
