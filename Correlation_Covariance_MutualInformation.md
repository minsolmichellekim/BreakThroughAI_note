### Correlate, Covariance, Mutual Information

Both covariance and correlation find the linear dependencies between variables.
Correlation finds the strength and direction of linear dependency between two random variables and is standarized so it's easier to work with.
High covariance means the variables are highly linearly dependent on each other. Its sign shows if features are directly or indirectly related. 
Pearson correlation standardizes the range of value for covariance to always be between -1 and 1.

Mutual information finds the amount of reduction in uncertainty one variable provides for another.
An entropy of 0 means a variable is completely predictable, whereas an entropy of 1 means a variable is completely uncertain
There is high mutual information between x1 and x2 if knowing x2 greatly reduces uncertainty (entropy) of x1.
Mathematically, Mutual Information I(x1,x2) = H(x1) - H(x1|x2), where H(x1|x2): uncertainty of variable x1 given x2. 
This tells us how knowing about one variable improves our understanding of another variable.

When we have a large number of features to work with, we want to select the features that are most relevant in predicting our label. In this case, we can select the features with highest correlation and mutual information against our label.

### Outliers
Z-score is a way of translating data to understand how many standard deviations away from the mean each point is.
Compute Z-score for each point and any point with abs(Z) >K as outlier: (x-mu)/sig
```
# Calculate a z-score for one (given) value
F = [4, 6, 3, -3, 4, 5, 6, 7, 3 , 8, 1, 9, 1, 2, 2, 35, 4, 1]
value = F[0]

F_std = np.std(F)
F_mean = np.mean(F)
value_zscore = (value-F_mean)/F_std

# Calculate the z-score for all values of a feature vector (The numpy way)¶
F_std = np.std(F)
F_mean = np.mean(F)
zscores = []
for value in F:
    z = (value-F_mean)/F_std
    zscores.append(z)
   
 # Calculate using python list comprehension 
 F_std = np.std(F)
F_mean = np.mean(F)
zscores = [(value-F_mean)/F_std for value in F]

# Calculate z-score for all values of a feature vector (The scipy way)
zscores = stats.zscore(df['hours-per-week'])

# Calculate z-scores for all values of all (numeric) columns
df_zscores = df.select_dtypes(include=['number']).apply(stats.zscore)
df_zscores.head(10)
```

A percentile is a value below which a given percentage of observations exists. 
A quantile is the same thing as a percentile but written as a decimal (90th percentile = 0.90 quantile).
The interquartile range (IQR) is the difference between the Q3 and Q1 percentiles. 
IQR, accompanied by a box-and-whiskers plot, tells us how data points are distributed.
Compute IQR as distance between 25th and 75th percentile. Any point that is K times greater than IQR from 25th fr 75th percentile will be considered outlier. 

Winsorization is a method of clamping outlier data points at specific values derived from the data itself, like a percentile. Data can be Winsorized from both tails of its distribution by choosing a lower/upper percentile and capping points at those percentiles.

```
import scipy.stats as stats
# cutoff from the 'bottom' and the 'top' both set at the 1% level.
df['education-num-win'] = stats.mstats.winsorize(df['education-num'], limits=[0.01, 0.01])
```

### Univariate vs Multivariate Data
Data is univariate if it contains one variable (uni = 1, variate = variable). Data is multivariate if it contains more than one variable.  

## Handling Missing values
1. Drop record or column (Leave feature if high NA values 
2. Imputation: replace with global mean 
3. Interpolation: when there's correlation among features, predict real values from features, using remaing values as predictor features (replace based on other features) 

```
df.isnull().values.any()
nan_count = np.sum(df.isnull(), axis = 0)
condition = nan_count != 0 # look for all columns with missing values

col_names = nan_count[condition].index # get the column names
nan_cols = list(col_names) 
nan_col_types = df[nan_cols].dtypes

# Inspect columns with missing values
df.loc[df['age'].isnull()]

# compute mean for all non null age values
mean_ages=df['age'].mean()
print("mean value for all age columns: " + str(mean_ages))

# fill all missing values with the mean
df['age'].fillna(value=mean_ages, inplace=True)

# Check if successful 
np.sum(df['age'].isnull(), axis = 0)
```
