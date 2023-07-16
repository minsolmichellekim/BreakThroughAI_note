Ensemble Modeling 
- combining independent model predicting same outcome
- both classification and regression problems

Model estimation bias vs variance tradeoff 
bias: model rigidly prevents adaption to nuances of data
varance: flexibility cause estimated model to be sensitive to data nuances

logistic regression: higher bias, decision tree: higher variance

Hyperparameters could have tradeoff as well 

Types of Ensemble Model
- average out the error individual methods might have
- Stacking: take weighted combination of prediction of total of K models
- Bagging: generating multiple models from same data, taking bootstrapped samples and averaging individual model predictions
  
- Boosting: iterating building model by focusing cumulative errors from prior iterations' predictions
