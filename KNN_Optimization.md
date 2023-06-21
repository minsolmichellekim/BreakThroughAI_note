```
import pandas as pd
import numpy as np
import os 
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

filename = os.path.join(os.getcwd(), "data", "cell2celltrain.csv")
df = pd.read_csv(filename, header=0)

# Remove string columns (as distance computation is impossible) 
# Or this can be handled with one-hot-encoding 
to_exclude = list(df.select_dtypes(include=['object']).columns)
df.drop(columns = to_exclude, axis = 1, inplace=True)

# Create labeled examples from dataset for training phase and create train/test data sets
y = df['Churn'] 
X = df.drop(columns = 'Churn', axis=1)

def train_test_knn(X_train, X_test, y_train, y_test, k):
    '''
    Fit a k Nearest Neighbors classifier to the training data X_train, y_train.
    Return the accuracy of resulting predictions on the test data.
    '''
    
    # 1. Create the  KNeighborsClassifier model object below and assign to variable 'model'
    model = KNeighborsClassifier(k)

    # 2. Fit the model to the training data below
    model.fit(X_train, y_train)
    
    # 3. Make predictions on the test data below and assign the result to the variable 'class_label_predictions'
    class_label_predictions = model.predict(X_test)
    
    # 4. Compute the accuracy here and save the result to the variable 'acc_score'
    acc_score= accuracy_score(y_test, class_label_predictions)
    
    return acc_score

# Tuning K 
k_values = [10,100,1000] 
accl = [] 
for k in k_values:
    score = train_test_knn(X_train, X_test, y_train, y_test, k)
    print('k=' + str(k) + ', accuracy score: ' + str(score))
    acc1.append(float(score))

# Visualizing accuracy:
fig = plt.figure()
ax = fig.add_subplot(111)
p1 = sns.lineplot(x=k_values, y=acc1, color='b', marker='o', label = 'Full training set')
p2 = sns.lineplot(x=k_values, y=acc2, color='r', marker='o', label = 'First 1500 of the training examples')

plt.title('Accuracy of the kNN predictions, for k$\in{10,100,1000}$')
plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)
ax.set_xlabel('k')
ax.set_ylabel('Accuracy on the test set')
plt.show()
```

### One-hot encoding 
Turns categorical values into binary representations 
Create a new binary indicator column for every unique value in the original categorical column 

```
to_encode = list(df.select_dtypes(include=['object']).columns)
df[to_encode].nunique()
# Convert top 10 most frequenct values instead of transforming all categorical values
top_10_SA = list(df['ServiceArea'].value_counts().head(10).index)

## Create ten one-hot encoded columns for ServiceArea
for value in top_10_SA:
    df['ServiceArea_'+ value] = np.where(df['ServiceArea']==value,1,0)
# Remove the original column from your DataFrame df
df.drop(columns = 'ServiceArea', inplace=True)
# Remove from list to_encode
to_encode.remove('ServiceArea')

## One-hot encode for Married
df_Married = pd.get_dummies(df['Married'], prefix='Married_')
# Concatenate with the encoded dataframe:
df = df.join(df_Married)
# Remove the original column from your DataFrame df
df.drop(columns = 'Married', inplace=True)
# Remove from list to_encode
to_encode.remove('Married')

## Using Scikit-Learn 
from sklearn.preprocessing import OneHotEncoder
# Create the encoder:
encoder = OneHotEncoder(handle_unknown="error", sparse=False)
# Apply the encoder:
df_enc = pd.DataFrame(encoder.fit_transform(df[to_encode]))
# Reinstate the original column names:
df_enc.columns = encoder.get_feature_names(to_encode)
# Concatenate with the encoded dataframe:
df = df.join(df_enc)
# Remove the original categorical features from X_train and X_test:
df.drop(columns = to_encode ,axis=1, inplace=True)
```
