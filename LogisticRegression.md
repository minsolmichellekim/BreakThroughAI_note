Using Logistic Regression to make predictions 
https://lms.ecornell.com/courses/1710629/pages/4-dot-1-5-read-using-logistic-regression-to-make-predictions?module_item_id=26782067

- General linear model using linear combination of features and set of weights to compute the label of unlabeled example 
- Estimate probability that a new, unlabeled example belons to. agiven class
- Best suited for binary classification
- Simplicity of algorithm is motivation  ex) Medical domain: Datasets to be collected from patient data and to be small, interpret very high 

Steps 
1. Linear step: generate output taking the sum of fetaure values * learned weights + intercept term
2. Inverse Logit (sigmoid) : Use inverse logit function to transform output into predicted probability between 0 and 1 tht an example belongs to class 1
3. Mapping: use probability threshold to output the class label from the predicted probaiblity generated. 

```
from sklearn.linear_model import LogisticRegression 

model = LogisticRegression(C=1) 
model.fit(X_train,y_train) 
probs = model.predict_proba(X_test) #logistic regression return probability 
```

C: less regularization, higher model complexity --> hyperparameter 

```
def log_reg_predict(X, weight, alpha): 
 # x := array; weight := array; alpha := float 
 
  XW = alpha + (X* weight).sum() # intercept: alpha 
  P = 1/(1+np.exp(-1*XW))
  
  return P 
```
Higher slope for larger value of weight, direction determined by positive/negative

