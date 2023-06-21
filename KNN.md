## K-nearest neighbors (KNN) algorithm 

Make predicitons about an example based on the labels of other examples 'near' it. 
KNN regression problems: make predictions for continuous label (predicted value is the average of the labels for the k-nearest neighbors) 
KNN classificaton problems: classify categorical label (category occurs most often is predicted label (class) 

**Separate line**
Boundary line around unlabeled example (radius= distance to the furthest of K neighbors) 
More labels cluster, better performance 
**Instance-based type**: store training examples in memory and utilize those examples on-demand to make predictions for a new, previously unseen example 
**Model-based learning**: models represented by some underlying data structure derived from training examples such as tree structure produced by decision tree supervised learning algorithm
**KNN**: instance-based type of supervised learning that stores training examples in memory and uses them to predict the labels  of new examples
Distance functions are used to measure similarity (nearness) between two points
**Neighbor Count (K)**: the number of nearest neighbors to use in prediction 
- hyperparameter chosen by the ML engineer; it can be determined based on domain knowledge, heuristics, or experimentation 
- High K: underfitting, model estimation bias, distance boundary becomes smoother and less susceptible to noise, but may misidentify 
- Low K: increase model complexity, overfitting, estimation variance, sensitive to nosiy data (high varaince) 
When increasing dimension, data points become farther away from each other and the distance between become.larger and less distinguisahble
Therefore needs to go through hyperparameter optimization
**Distance Function**: the functional form of distance metric and weights used on each nearest neighbor
ex) Euclidean Distance 
ex) Mahalanobis Distance: account for correlation among features and scale
- S: covariance matrix. If S: identity matrix, there's no correlation among features, so Mahalanobis distance will reduce to Euclidean distance. 
- If along principal components (direction of highest variance/ direction where data is most stretched out, would be considered to be closer to blue
ex) Manhattan Distance: sum of the absolute difference between each feature 
**Normalization**: method to ensure features are on the same scale
- Since Euclidean distance doesn't regards scaling, without normalization, higher scale will receive higher implicit weight in KNN
- Makes each feature has a similar scale of distribution, making them equal importance in distance function


### Steps for KNN model
1. Train KNN model on X_train and y_train 
2. Apply trained model to X_test to produce predicted class labels
3. Compare predicted class labels against true labels provided in y_test

```
import pandas as pd
import matplotlib
%matplotlib notebook 
import matplotlib.pyplot as plt
from helper2 import visualize_knn
import os 

filename = os.path.join(os.getcwd(), "data", "Iris_Data.csv" 
df_iris = pd.read_csv(filename, header=0) 

#pick a few random examples
df_iris.sample(n=10, replace=False, random_state = 1)

#KNN
number_of_neighbors = 3
visualize_knn(number_of_neighbors)

#Create labeled examples from dataset for training phase
X = df_iris[['sepal_length', 'sepal_width', 'petal_length', 'petal_width']] #features 
y = df_iris['species'] #labels

#Model
X_train, X_test, y_train, y_test = train_test_split(X,y, test_size=0.2, random_state =4) 
model = KNeighborsClassifier(n_neighbors =3) 
model.fit(X_train, y_train) 
prediction = model.predict(X_test) 
print(prediction) 

#Checking Accuracy 
score = accuracy_score(y_test, prediction) 
print('Accuracy score of model: ' + str(score))
```

### Enhancing KNN
1. Resolving ties: case without most common label --> fall back onto majority label within the k-2 closest neighbors (If 3NN results tie, then fall back to 1NN and get definitive label)
2. Choosing distance function
3. Use data structures such as k-d trees or ball trees for speedup (compute distance to the box containing those points) 

For more information on KNN: 
https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html
