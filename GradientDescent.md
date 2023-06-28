## Gradient Descent 
GD is a numeric optimization algorithm to find minimum or maximum of mathematical function 
It finds optimal weights of logistic regression, by finding feature weight X that gives lowest value of log loss. 
Gradient descent can also run for multiple variables at same time

Steps for Gradient Descent 
1. x=0 make a guess 
2. Compute gradient of initial guess (first derivative of function to minimize) : slope at given point 
3. Sign of gradient at initial guess 
4. Since we want to minimize, move oposite direction of gradient 
5. Gradient line at minimum will be when slope=0, then we found the minimum 
Define a rule where gradient is close to 0, then stop --> stopping criterion 

$$ w_{t+1} = w_t - \gamma * \nabla F(w_t) $$

$\gamma$ is step size, or learning rate, which we multiply to gradient. It can be constant or variable, that determines the speed. 

```
func df gradient_descent(w_0, stepsize, gradient_function, tolerance= 10**-6, max_iter=100):
  w_prior = w_0
  for i in range(max_iter):
    grad= gradient_function(w_prior)
    w = w_prior - stepsize * grad # update
    if np.abs(w-w_prior) < tolerance:
      break #until the criteria is met

    w_prior = w

  return w
```

## How to choose learning rate
Find learning rate that will converge the gradient descent function 

$$w_{t+1} = w_t - H(w_t)^{-1} * \nabla F(w_t)$$

Second derivative of F(w), Hessian at current value of w, determines the curvature of function. 
Large curvature = steep quickly, then we would want lower steps. 
Like this, we can dynamically determine using below. 
```
stepsize =1 /hessian_function(w_prior)
```
However, Hessian can become expensive if have large features or using Neural networks. 
