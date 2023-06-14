### Get number of lines using <code> cat </code> command 

```
! cat data/adult.data.partial | wc -l
```
Result: prints content of file path and name "data/adult.data.partial" 
<code> | </code> is a pipe command that chains two commands such that output is the first and input to the second; here, the second command <code> wc </code> is "word count", specifically lines defined by <code> -l </code>
Note that the true number of data entries is the result -1 as the first line shows column names. 

### Print out the first 5 lines
```
! head -5 data/adult.data.partial
```
<code> head </code> prints few lines; 5 lines in this example. It includes the column names on the first row 

### Get the Number of columns 
1. Get first line containing column names
2. Split the first line into multiple lines (each column name will be on its own line)
3. Count the lines.

```
! head -1 data/adult.data.partial | tr ',' '\n' | wc -l
```

<code> tr </code> takes in two parameters: original symbol or string to replace, and what to replace it with. Here, we look for commas and 'translate' them to new lines. 
If the data was separated by tab instead of comma, we can use '\t' instead. 

### Initial data exploration and summary statistics with Pandas 
```
import pandas as pd
import os 

filename = os.path.join(os.getcwd(), "data", "adult.data.partial" 
df = pd.read_csv(filename,header=0)
df.head() 
df.shape
df.describe() 
```
<code> df.shape </code> gives number of rows and columns as (nrow,ncol)
<code> df.describe() </code> gives a summary statistics of data such as count, mean, std, min, 25%, 50% (average), 75%, max.
we can look for class imbalance problem, check for skewed data. when negative value for count, we would need to pre-process data. 

```
df_summ_all = df.describe(include= 'all') 

describe_vars = ['age', 'education-num', 'hours-per-week']
df_summ_selected = df[describe_vars].describe()
age25p = df_summ.loc['24%']['age']
df_summ.loc['std'].idxmax(axis=1)
```

We can identify summary values of specific variables or get specific summary statistic value. Also, we can use <code> loc[] </code> to get certain feature value. 
When use <code> .idxmax() </code> we can identify the name of column which has maximum value. Specifying as axis =1 indicates the search for highest value to be column-wise. Another version of using <code> .idxmax() </code> would be  <code> df_summ.idxmax(axis=1)['std'] </code> where we first find max value of all the rows and select only the summary statistic row of interest.

### Identifying features with negative values or highest range

```
# Do any feature have negative values? 
true_false = np.any(df_summ.loc['min'] <0) 
print(true_false) 

# Which feature has highest range? 
column_ranges = df_summ.loc['max'] - df_summ.loc['min']
column_range_name = column_ranges.idxmax(axis=1)
print(column_range_name)
```



