Feature distribution informs us what data preparation techniques we can use. 
By observing how two or more features are distributed, we can identify correlation or redundant variables.
Then, we will be able to select features that are correlated with label. 

Univariate distribution can be shown by histogram, a bar chart with x-axis representing range of data and y representing count. 
Histogram works for both numerical and categorical data.

For a regression task, we can use check if there is ...
- Different segments with different patterns --> create different model for each section 
- Skewness --> take log of features to check if make bell-curve --> make functional transformation 


### Using Seaborn and Matplotlib to Visualize data 

```
import pandas as pd 
import numpy as np 
import os 

fileame = os.path.join(os.getcwd(), "data", "adult.data.partial") 
df = pd.read_csv(filename, header=0) 
```

***Matplotlib*** offers plotting functionality centered on Pandas DataFrames. 
***matplotlib.pyplot*** provides functions for plotting data, such as customizing plots and annotating plots.
***Seaborn*** specialized and refines nterface to support visualization of tabular data and statistical properties . 

```
import matplotlib.pyplot as plt 
import seaborn as sns
sns.set_theme() #makes seaborn plots look better
```

### Produce Histogram for a feature 
```
sns.histplot(data=df, x= "age") 

#Two ways to produce histogram for logarithm of feature
sns.histplot(data=df, x="age", log_scale= True)
sns.histplot(data=np.log(df['age'])
```

Also, plot can be re-scaled
```
sns.histplot(data=df, x="hours-per-week", log_scale = True)
plt.ylim(0, 600)
```

### Produce a Bar Plot for Categorical Feature
```
fig1 = plt.figure(figsize = (13,7)) #image can be rescaled
ax = sns.histplot(data=df, x="education") 
t1 = plt.xticks(rotation =45) #rotate x-axis ticks label to fit all
```

### Enforcing Order of Categories 
```
cat_order = ['Preschool', '1st-4th', '5th-6th', '7th-8th', 
             '9th', '10th', '11th', '12th', 'HS-grad', 
             'Prof-school', 'Assoc-acdm', 'Assoc-voc', 
             'Some-college', 'Bachelors', 'Masters', 'Doctorate']
df['education'] = pd.Categorical(df['education'], cat_order)

fig2 = plt.figure(figsize = (13,7))
ax = sns.histplot(data=df, x="education") 
t2 = plt.xticks(rotation =45) 
```


