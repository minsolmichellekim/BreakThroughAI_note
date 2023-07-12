**Performing Out-of-sample validation**
Definition: Computing evaluation metrics on non-training data

Consider Expected Loss from theoretical data  vs training loss from training data
Full Data Universe (unobserved) --> sampled Data (observed) --> training data + test data
1. Test set should be representative of data the model will be applied to 
2. Test set should be independent from training (no overlap in units) 
3. No model selection or training should be done after evaluating on test set 

Do units of analysis appear multiple times in the data? 
Is there a time dimension? 
If no, then we can do random selection 

´´´
sample_pct = 0.2
n= df.shape[0]
randomizer = np.random.random(n)
train = df([randomizer>sample_pct)]
test =  df([randomizer<=sample_pct)]
´´´

**Determining splitting method**
Multiple same userID --> might violate independent rule
Use hash bucket that is deterministic. Example with same id will only be in one of the set

´´´
def id_hasher(x, buckets= 100): 
  return (has(x) %buckets)/float(buckets) 
df['hash_bucket'] = df['id'].apply(id_hasher) 
train = df([df.hash_bucket>sample_pct)]
test =  df([df.hash_bucke<=sample_pct)]
´´´

**Model Selection Overview**
Two criteria
1. Identify sufficiently varied set of model candidate
2. Applying appropriate out-of sample evaluation

**Test loss vs Model complexity**
Sufficient explor
Model design dimensions

**Algorithm**
´´´
model candidates = [ ] 
feature_sets = []

for candidate in model_candidates: 
  for X_set is feature sets: 
    candidate.fit(df[X_set], d[y]
´´´
Linear algorithms, fewer features, restrictive hyper-parameter, low complexity unlike non-linear algorithms 


Out of Sample Validation Techniques 
Holdout method: randomly splitting dataset into training and validation subsets

K-fold cross-validation method: split data set into equally sized subsets or folds, with k representing number of folds. 

´´´
folds = KFold(n_splits=5, shuffle = True, random_state=10) 
model_scores = []
model_params = [] 
max_depths = [2**i for i in range(10)]

for md in max_depths: 
  model= decisionTreeClassifier(max_depth = md) 
  score = run_cross_valdiation(df, X, y, model, folds) 

  model_scores.append(score) 
  model_params.append(md) 
score_df = pd.DataFrame({'score': model_scores, 'param': model_params})
´´´

´´´
folds= KFold(n_splits=5, shuffle=True, random_state=10) 
clf = GridSearchCV(DecisionTreeClassifier(), param_grid = {'max_depth'= max_depths}, cv= folds, scoring = 'roc_auc'}
clf.fit(df[X], df[y])
print(clf.best_estimator_)
´´´

Choosing hyperparameter configurations 
Grid search: goes through various combinations of hyperparameters systematically
Random Search: electing the hyperparameter values at random in order to capture a wide variety of combinations that could otherwise be missed by being systematic about choosing our hyperparameters.

