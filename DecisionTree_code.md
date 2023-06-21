### Loading Dataset 
```
filename = os.path.join(os.getcwd(), "data", "cell2celltrain.csv") 
df = pd.read_csv(filename, header=0) 

# Drop column with missing vales
df.isnull().values.any() 
df.drop(columns=['Married', inplace= True])
```

### One-hot Encoding 
```
# Get columns with object datatypes for one hot encoding 
to_encode = list(df.select_dtypes(include=['object']).columns) 
df[to_econde].nunique() #get total number of observations of each column of to_encode 

# Since ServiceArea have a lot of value, use one-hot encoding on frequent values only
top_10_SA= df["ServiceArea"[.value_counts().head(10).index
for val in top_10_SA: 
  df["ServiceArea_"+val] = np.where(df["ServiceArea"]==val, 1, 0) 
df.drop[columns= "ServiceArea", inplace=True)

# One hot coding on remaining values
for col_name in to_encode[1:]: 
  temp_df = pd.get_dummies(df[col_name], prefix= col_name + '_') #Pandas
  df = df.join(temp_df) 
  df.drop(columns = col_name)
```

### Create Labeled Examples from Dataset 
```
y = df["Churn"] 
X = df.drop(columns= "Churn", axis=1) 
print("Number of examples: " + str(X.shape[0]))]
print("\nNumber of Features:" + str(X.shape[1]))

# Creating training and test dataset 
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.3, random_state = 123) 

# Decision Tree Classifier
# @ Leaf:= min number of samples required to be leaf node 
# @ Depth:= max depth of tree
# @ crit:= function to measure the quality fo split. Defaulted as gini 

def train_test_DT(X_train, X_test, y_train, y_test, leaf, depth, crit= "entropy"): 
  model = DecisionTreeClassifier(criterion= crit, max_depth = depth, min_samples_leaf = leaf) 
  model.fit 
```
