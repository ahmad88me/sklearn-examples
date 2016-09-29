# sklearn-examples
This repo is to have examples that helps people starting on sklearn and pandas to check how the api works instead of checking the good but intensive documentations which can be time consuming to look for the information

source: http://stackoverflow.com/questions/30023927/sklearn-cross-validation-stratifiedshufflesplit-error-indices-are-out-of-bou
e.g. 
```
import pandas as pd
import numpy as np
# UCI's wine dataset
wine = pd.read_csv("https://s3.amazonaws.com/demo-datasets/wine.csv")

# separate target variable from dataset
target = wine['quality']
data = wine.drop('quality',axis = 1)

# Stratified Split of train and test data
from sklearn.cross_validation import StratifiedShuffleSplit
sss = StratifiedShuffleSplit(target, n_iter=3, test_size=0.2)

for train_index, test_index in sss:
    xtrain, xtest = data[train_index], data[test_index]
    ytrain, ytest = target[train_index], target[test_index]

# Check target series for distribution of classes
ytrain.value_counts()
ytest.value_counts()
```
error: "IndexError: indices are out-of-bounds"

Solution: 
```
data_array = data.values
for train_index, test_index in sss:
    xtrain, xtest = data_array[train_index], data_array[test_index]
    ytrain, ytest = target[train_index], target[test_index]
```
or 
```
for train_index, test_index in sss:
    xtrain, xtest = data.iloc[train_index], data.iloc[test_index]
    ytrain, ytest = target[train_index], target[test_index]
```
