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

**ROC curve** 
ROC: Receiver Operating Characteristic curve
When don't commit to single threshold such as
- Uncertain about prediction budget
- Relative false positive/negative costs
- Used for ranking or classification metrics

To construct AUC, go through iterative process. 
This show tradeoffs for all classification thresholds. 
Model with Higher, steeper ROC, meaning high AUC is a better model.

  
<img width="348" alt="Screenshot 2023-07-11 at 10 54 11 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/049fcbe4-e05b-4d89-bae7-8d8e55226857">

<img width="348" alt="Screenshot 2023-07-11 at 10 55 58 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/8fb80307-1e36-4a0d-9db5-2e1058a402bb">
  
  <img width="348" alt="Screenshot 2023-07-11 at 10 54 56 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/2f046656-1a88-4602-8c95-ca3dbeef4635">

<img width="348" alt="Screenshot 2023-07-11 at 10 55 10 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/16d2f82b-e0e1-4d79-b31b-f6959d43f327">
