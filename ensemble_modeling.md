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
1. Stacking: take weighted combination of prediction of total of K models
2. Bagging: generating multiple models from same data, taking bootstrapped samples and averaging individual model predictions
3. Boosting: iterating building model by focusing cumulative errors from prior iterations' predictions
  
<img width="949" alt="Screenshot 2023-07-19 at 4 36 47 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/a3c78b8d-c648-482a-bdd0-2d52a748137e">

