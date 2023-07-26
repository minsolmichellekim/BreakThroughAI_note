### I. Import Data, Load DataSet
```
import pandas as pd
import numpy as np
import os 
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import roc_auc_score

filename = os.path.join(os.getcwd(), "data", "bookReviews.csv")
df = pd.read_csv(filename, header=0)

y = df['Positive Review'] 
X = df['Review']
#print(X.shape) (1973,)
```

## II. Split Labeled Examples into Training and Test Sets
```
X_train, X_test, y_train, y_test = train_test_split(X, y, train_size=.75, random_state=1234)
```
## III. Implement TF-IDF Vectorizer to Transform Text 
```
from sklearn.feature_extraction.text import TfidfVectorizer

document_collection = [
    'My cat loves yarn. Blue yarn.',
    'I have a blue dog.'
]

# 1. Create a TfidfVectorizer oject
vectorizer = TfidfVectorizer()

# 2. Fit the vectorizer to document_collection
vectorizer.fit(document_collection)

# 3. Print the vocabulary
print("Vocabulary size {0}: {1}\n".format(len(vectorizer.vocabulary_), vectorizer.vocabulary_))

# 4. Transform the data into numerical vectors 
print("Matrix:\n")
resulting_matrix = vectorizer.transform(document_collection)

# 5. Print the matrix
print(resulting_matrix.todense())

# 6. Visualize the matrix in a heatmap
print("\nHeatmap of Matrix:\n")
df_print = pd.DataFrame(resulting_matrix.toarray(), columns=vectorizer.get_feature_names())
plt.rcParams['figure.figsize'] = [6, 5]  
ax = sns.heatmap(df_print, annot=True, cmap='coolwarm', cbar=False, yticklabels=["Document 1: My cat loves yarn. Blue yarn", "Document 2: I have a blue dog."]);
_ =ax.set_title('TF-IDF Matrix');
_ =ax.set_yticklabels(ax.get_yticklabels(), rotation = 0, fontsize = 15)
```

### Transform Book review textural features into numerical vectors with TfidVectorizer
```
# 1. Create a TfidfVectorizer oject
tfidf_vectorizer = TfidfVectorizer()

# 2. Fit the vectorizer to X_train
tfidf_vectorizer.fit(X_train)

# 3. Print the first 50 items in the vocabulary
print("Vocabulary size {0}: ".format(len(tfidf_vectorizer.vocabulary_)))
print(str(list(tfidf_vectorizer.vocabulary_.items())[0:50])+'\n')

      
# 4. Transform *both* the training and test data using the fitted vectorizer and its 'transform' attribute
X_train_tfidf = tfidf_vectorizer.transform(X_train)
X_test_tfidf = tfidf_vectorizer.transform(X_test)


# 5. Print the matrix
print(X_train_tfidf.todense())
```
## IV. Fit Logistic Regression Model to Transformed Training Data and Evaluate Model 
```
# 1. Create a LogisticRegression model object, and fit a Logistic Regression model to the transformed training data
model = LogisticRegression(max_iter=200)
model.fit(X_train_tfidf, y_train)

# 2. Make predictions on the transformed test data using the predict_proba() method and 
# save the values of the second column
probability_predictions = model.predict_proba(X_test_tfidf)[:,1]

# 3. Make predictions on the transformed test data using the predict() method 
class_label_predictions = model.predict(X_test_tfidf)

# 4. Compute the Area Under the ROC curve (AUC) for the test data. Note that this time we are using one 
# function 'roc_auc_score()' to compute the auc rather than using both 'roc_curve()' and 'auc()' as we have 
# done in the past
auc = roc_auc_score(y_test, probability_predictions)
print('AUC on the test data: {:.4f}'.format(auc))

# 5. Print out the size of the resulting feature space using the 'vocabulary_' attribute of the vectorizer
len_feature_space = len(tfidf_vectorizer.vocabulary_)
print('The size of the feature space: {0}'.format(len_feature_space))

# 6. Get a glimpse of the features:
first_five = list(tfidf_vectorizer.vocabulary_.items())[1:5]
print('Glimpse of first 5 entries of the mapping of a word to its column/feature index \n{}:'.format(first_five))
```
## V. Experiment with Different Document Frequency Values and Analyze Results 
```
for min_df in [1,10,100,1000]:
    
    print('\nMin Document Frequency Value: {0}'.format(min_df))
    
    # 1. Create a TfidfVectorizer oject
    tfidf_vectorizer = TfidfVectorizer(min_df=min_df, ngram_range=(1,2))

    # 2. Fit the vectorizer to X_train
    tfidf_vectorizer.fit(X_train)

    # 3. Transform the training and test data
    X_train_tfidf = tfidf_vectorizer.transform(X_train)
    X_test_tfidf = tfidf_vectorizer.transform(X_test)

    # 4. Create a LogisticRegression model object, and fit a Logistic Regression model to the transformed 
    # training data
    model = LogisticRegression(max_iter=200)
    model.fit(X_train_tfidf, y_train)
    
    # 5. Make predictions on the transformed test data using the predict_proba() method and save 
    # the values of the second column
    probability_predictions = model.predict_proba(X_test_tfidf)[:,1]

    # 6. Compute the Area Under the ROC curve (AUC) for the test data.
    auc = roc_auc_score(y_test, probability_predictions)
    print('AUC on the test data: {:.4f}'.format(auc))

    # 7. Compute the size of the resulting feature space using the 'vocabulary_' attribute of the vectorizer
    len_feature_space = len(tfidf_vectorizer.vocabulary_)
    print('The size of the feature space: {0}'.format(len_feature_space))
    
    # 8. Get a glimpse of the features:
    first_five = list(tfidf_vectorizer.vocabulary_.items())[1:5]
    print('Glimpse of first 5 entries of the mapping of a word to its column/feature index \n{}:'.format(first_five))

    # 9: Print the first five "stop words" - words that we are ignoring
    first_five_stop = list(tfidf_vectorizer.stop_words_)[1:5]
    print('Glimpse of first 5 stop words \n{}:'.format(first_five_stop))
    ```
