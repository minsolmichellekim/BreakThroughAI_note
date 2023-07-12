Select Features 
Heuristic rules 
- Feature has minimum level of correlation or mutual information with the label  

Regularization 
Goal: Restrict model by minimizing feature contributions, so model doesn't overfit 
- Penalize complex models via loss penalty 
- Run hyperparameter seleciton to identify best C and remove features with seight close to 0
- Helpful when have small number of data and is risk of overfitting

  
  $$
  L_{L1 regularized} = L + {1 \over C} \sum_{j=1}^{m} |w_j|
  $$

L1 can set weights to be 0, so can select features and simplify model, but it can underfit.
L1 will try to get rid of feature if can. For L2, it will try to use both, would work best if have correlated features.
L1 is affected by outliers as penalty is smaller than L2
L2 can set weights close to 0, shrinks weights evenly, useful for correlated features. 
Elastic Net: has one parameter for each method 

**C**
C controls how much regularization is applied 
High value: less regularization, emphasis on classifying each individual datapoint 
Low value: emphasis on classifying majority of data, penalize features more 

  
