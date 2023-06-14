Correlate, Covariance, Mutual Information

Both covariance and correlation find the linear dependencies between variables.
Correlation finds the strength and direction of linear dependency between two random variables and is standarized so it's easier to work with.
High covariance means the variables are highly linearly dependent on each other. Its sign shows if features are directly or indirectly related. 
Pearson correlation standardizes the range of value for covariance to always be between -1 and 1.

Mutual information finds the amount of reduction in uncertainty one variable provides for another.
An entropy of 0 means a variable is completely predictable, whereas an entropy of 1 means a variable is completely uncertain
There is high mutual information between x1 and x2 if knowing x2 greatly reduces uncertainty (entropy) of x1.
Mathematically, Mutual Information I(x1,x2) = H(x1) - H(x1|x2), where H(x1|x2): uncertainty of variable x1 given x2. 
This tells us how knowing about one variable improves our understanding of another variable.
