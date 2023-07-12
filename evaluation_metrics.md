
### Confusion Matrix 

<img width="348" alt="confusion_classification_metrics" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/319e2186-5b00-4af3-8043-40b37239be72">

### Classification Evaluation Metrics
**I. Accuracy**
- Number of correct predictions
- most commonly used in multi-class problems
- may overstate the fit of model
  
$$
Model Accuracy = {TP+TN \over TP+TN+FP + FN}
$$

Kappa is used to adjust model accuracy.

$$
Kappa = {Model Accuracy - Random Accuracy \over 1 - Random Accuracy}
$$


**II. Precision**
- how well model can correctly predict specific outcome
- Measure of quality 
- favored in binary classification when false positives are much worse than false negatives

$$
Model Precision = {TP \over TP + FP }
$$

**III. Recall**
- Number of times model correctly predict a specific outcome, focusing on quantity
- Calculates proportion of actual positive classes that were predicted (ex. correct purchse/actual purchase)
- favored in binary classificaiton when false negatives are much worse than false positives

$$
Model Recall = {TP \over TP + FN} 
$$
