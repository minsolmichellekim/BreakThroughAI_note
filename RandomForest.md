## Random Forest 
**Description** : Random forest combines decision trees into an ensemble. The models
are trained independently (possibly in parallel) on data bootstraps with
one small modification: For each split in each tree, a small subset of k
features is randomly sampled and all other features are ignored. This
procedure reduces the variance of the final model as training trees on
random features results in them being uncorrelated further.

**Goal**: achieve optimal balance of low bias and low variance
Ensemble of decison trees that generalizes better than individual decision tree
Takes more time and resources to train 

**Assumption**: Data set is not too high dimensional; similar inputs have similar labels.

Complexity of supervised learning model is controlled by hyperparameters 
- When overly complex, tends to overfit and leads to high variance error 
- When overly simple, tends to underfit and leads to high bias error 

<img width="423" alt="Screenshot 2023-07-18 at 6 38 38 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/4c3a1c45-3649-4e0a-9aec-5228414e5254">

 Individual trees will be using only a subset of the feature, for sufficient differences between the trees

### Pseudocode
**Training**
For i in number of estimators:
  Bootstrap data = sample N examples randomly, with replacement
  Randomly select a subset of features
  Build a decision tree with bootstrap data and add it to the ensemble 

**Prediction**
For a given X, get predictions from all the decision trees in the ensemble and average them.
