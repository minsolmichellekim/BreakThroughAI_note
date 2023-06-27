https://en.wikibooks.org/wiki/LaTeX/Mathematics#Fractions_and_Binomials

To be continued... 

Log Loss (binary cross-entropy loss)
- measure performance of binary classification model
- Belong to either class 0 or class 1
- $y_i$ is the actual class label and $P_i$ is predicted proability that label is class 1 for same training example
  
$$L_{LL} = - \frac{1}{N} $$

Mean squared Error 
- Measure performance of regression model
- $y_i$ is label of training example and $\hat{y_i}$ is prediction value

Zero-one Loss 
- Evaluate classifiers in multiclass/binary classificatin setting
- Useful to guide optimization during training  
- Counts how many mistakes a model makes when making prediction 
- Normalized zero-one loss returns fraction of misclassified training examples out of all examples in training data 
