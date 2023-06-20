## Predictive models from data 

### Basic Model training models
1) K-Nearest label
2) Decision tree
3) Logistic Regression 
4) Random Forest 
5) Gradient Boosting
6) Neural Network 

### Keywords
**Lost function**: mathematical function that quantify how well model is performing --> Minimize loss on expected law (unseen data) 
**Overfitting**: model generalization to be poor --> adjust hyperparameters (parameters set prior to learning, with trade off btweeen complexity and simplicity of models) 
- This occurs when model learns the idiosyncrasies that are particular to only the training data set 
**Underfitting**: high training error, can't generalize well to new data 
**Generalization**: Model's ability to adapt to new, previously unseen data 
--> Avoid problems of overfitting and underfitting by incorporating validation phase after model training to tunde hyperparameters to optimal values

Hyperparameters are often used to adapt model to particular setting, tuned for given predictive modeling problem, or specified by practitioner or heuristics . 
Ex) Learning rate or step size in gradient descent, depth of tree in decision trees, size of neighborhood in KNN

**General pipeline should be as below:** 
1. Train Data Sample (finite) from data distributon of interest
2. Fit Model with low training loss 
3. New Data --> check if overfitting 

### The Core Skylearn API (scikit-learn) 
Provides three steps of modeling
1. Model specification (how to configure) 
2. Model fitting (training model) 
3. Model prediction

```
from sklearn.linear_model import LogisticRegression 
model = LogisticRegression (C=1) 
model.fit(df[x], df[y])
prediction = model.predict(df[x]) 
```

### Model Selection 
```
from sklearn.linear_model import LogisticRegression 
from sklearn.neighbors import KNeighborsClassifier 
from sklearn.tree import DecisionTreeClassifier

models = {
'LR': LogisticRegression(C=1), 
'KNN': KNeighborsClassifier(n_neighbors = 100), 
'DT': DecisionTreeClassifier(min_samples_leaf = 256) }

for m in models: 
  models[m].fit(df[X], df[y]
```

