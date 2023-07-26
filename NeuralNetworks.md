## Neural Networks 
- Identify nonlinear relationship
- Use many linear models with nonlinear transformation at each node
- Multiply features with weighted sum --> activation function 

 <img width="293" alt="Screenshot 2023-07-25 at 9 09 24 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/6452b3a9-9c53-4c05-9999-44bc2b989e54">

Linear function applied to input layer (matrix vector multiplication involving multiplying input features by weights and adding up results) 
Output of linear function is then amplified by nonlinear activation function.
It takes output summation of linear function and determines how little/much lienar function should contribute to the next layer in network. 
The linear and nonlinear transformation process continues for every hidden layer. 

## Activation functions
<img width="689" alt="Screenshot 2023-07-25 at 9 19 04 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/461eb176-0382-443e-8692-7bf76e795a40">
1. ReLU: Nonlinear Activation Function (rectivied linear unit) 
- If input is less than 0, outputs 0. Otherwise, for positive input value, outputs z. 
- But may have problem in learning process, gradient descent. 

2. Sigmoid
- outputs values between 0 and 1 (used when producing probabilities) 
- Linear function switched off (transition close to 0) or switched on (close to 1) 
- Two ends too flat for stochastic GD and weights may saturate because transition values stuck in flat regions

3. Hyperbolic tangent (tanh) function
- Range between -1 and 1 (Negative values become very negative while values near 0 stay 0)
- Useful for binary classification


## Designing Neural Network 
1. Number of hidden layers
2. Number of nodes within each layer
3. Activation function use within each node

## Training Neural Network 
A lot of parameters 
Loss function: tells how much current prediction deviates from truth or label 
- MSE for regression etc
- Softmax Loss
- Backpropagation and chain rule

### Stochastic Gradient Descent
- In GD, batch is total number of training examples that are used to calculate gradient in single iteration.
- SGD: version of GD mitigating issue by selecting subset of examples chosen at random from data set. (mini-batch 10-1000 examples)
- SGD is useful for deep neural networks as evaluating and calculating loss and gradients of every single example is expensive

### Process
1. Sample a mini-batch of m training examples without replacement
2. Evaluate output of these m training examples
3. Calculate loss using loss function
4. Calculate gradient of loss wrt weights
5. Take gradient step to update weights
6. Repeat steps until training loss doesn't decrease
