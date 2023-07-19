## Gradient boosted decision trees (GBDT) 
### Ensemble method with individual trees

Initialize shallow decision tree and compute residual respect to training data. 
Then train another tree. Use new residual tree as gradient and move our original tree toward direction of residual tree by small step. 
Repeat process until reach number of trees desired. 

<img width="337" alt="Screenshot 2023-07-18 at 7 30 00 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/b702f032-70b2-4bf5-8b82-bab5621ee9f6">

Base model: individual trees 
Full model: weighted sum over the trees 

<img width="839" alt="Screenshot 2023-07-18 at 7 49 24 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/3808288a-0d59-4788-8c78-5308d1a33704">

1. Start with simple model $f(X) = T_0(X)$ that prediction of $0$ regardless of $X$.
2. Calculate how much each point is off from data to get residuals (blue dots) 
3. Train shallow decision tree $T_1(X)$ against blue dots to get gradient
4. Produce new $f(X)$ by adding $\gamma \cdot v1_1 \cdot T_1(X)$ to our previous version of $f(X)$. 
5. Repeat until reach number of trees desired (Residual graph will flatten out as error of $f(X)$ is reduced.

### Pseudocode 


### Random Forest vs. Gradient Boosted Decision Trees Comparison 

<img width="654" alt="Screenshot 2023-07-18 at 9 46 35 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/2968216b-befd-4e8f-8e4f-3b0bfa5755b6">

In random forest, take simple average over individual decision trees for Random Forest
- Each decision tree uses subset of features
- Bootstrap sample of data, which is typically overfit

In GBDT, each tree has weight that learning algorithm determines 
- Use all features
- Use original data
- Generally shallow trees (max_depth <6)
- Trained on cumulative prediction error, not original label 

Compute residual (error) --> Between data and the first model (average value of target variable) 
Fit decision tree to residual 
Compute residual again, with latest tree added
Process repeat until stopping criteria 

<img width="782" alt="Screenshot 2023-07-18 at 7 41 02 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/72243ff4-b72e-4261-82d7-d0d98015cd05">

Decision boundary for 9 trees, each model is simple model, but adding together over iterations (orders of magnitude up to about 700) will result below
<img width="782" alt="Screenshot 2023-07-18 at 7 43 09 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/123d50d5-666c-4ccf-aa0f-b4f1de95b212">
As number of trees grow, capture circular shape as expected. 
When we see small patterns of blue embedded in the red, it is sign of overfitting.
Unlike the tradeoff between overfitting and scalability, GBDT can suffer both overfitting and reduce in scalability with increase number of trees. 

Ensemble method need more data, tend to be slow in training and prediction. (Logistic regression will be faster. )
While it is generalizable, it can lose interpretability (that is needed in healthcare, finance) 
