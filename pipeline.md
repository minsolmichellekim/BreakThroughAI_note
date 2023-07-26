## Conceptual Pipeline

<img width="637" alt="Screenshot 2023-07-25 at 8 04 14 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/1ffa86f4-e3a3-4540-8f2c-8323cb09b47f">

## Text Modeling Pipeline 
- Setup pipeline
  ```
  from sklearn.pipeline import Pipeline
  text_pipe = Pipeline( [ ('vectorizer', TfidVectorizer(min_df =10 ), ('model', LogisticRegression(C=1)])

  text_pipe.fit(X_train, y_train)
  text_predictions = text_pipe.predict_proba(X_test) 
  ```
- Combine with model selection
  ```
  X= df['text_feature'] 
  y= df['label']
  
  X_train, X_test, y_train, y_test = train_test_split(X,y, test_size=.20, random_state = 1234) 

  text_pipe = Pipeline([('vectorizer', TfidVectorizer(), ('model', LogisticRegression()])
  param_grid = {'model_C': [0.1, 10], 'vectorizer_min_df': [10,100], 'vectorizer_ngram_range': [(1,1), (1,2)]}

  grid_search = GridSearchCV(text_pipe, param_grid, cv=5, scoring = 'roc_auc')
  grid_search.fit(X_train, y_train) 

  ```
