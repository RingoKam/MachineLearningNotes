# Objective
## learn how to process data with python

### Get the dataset
with every dataset, we will identify **independent variable** to predict the outcome of **dependent** variable. 

with our given dataset:
* Country, Age and Salary are Independent. 
* Purchased is dependent. 

### Importing the libaries
library is a tool we use for specific job.

common essential libraries
* numpy - math library
* matplotlib.pyplot - plot chat library
* pandas - import and manage dataset

our IDE of choice ise spyder in python. 
* execute lines of code with ctrl + cmd + enter

### importing dataset
we can import dataset w/ pandas

    dataset = pandas.read_csv('data.csv')

We need to distinguish the *matrix of features* and *dependent variable vector*. 

we have 
* 3 independent variable Country, Age and Salary.
* 10 Observations (aka rows)
* 1 dependent variable vector, Purchased. 

to setup the indepdent variable

    X = dataset.iloc[:, :-1].values

iloc[lines, columns], we are taking everything for lines, but skipping the last column. 

to setup the dependent variable

    Y = dataset.iloc[:, 3].values

by specifying a number, above is saying we will only take column 3 for everyrow from the dataset.

### Handling Missing Data
remove bad missing data? Quite dangerous because the observation may contain crucial info! As an alternative, lets use the mean of the column. 

using sklearn library can help us in the above situation. 

    from sklearn.preprocessing import Imputer

above will import sklearn library and bring in Imputer class. 

cmd + i allow us to look at the documentation of the class.

    imputer = Imputer();

by default, if no argument is given to the Imputer object constructor above, the default will be used. 
* missing_values = 'NaN' - indicate missing values to get rid of is 'NaN'
* stradegy = 'mean' - the stradegy use to fill missing values, here we will use mean 
* axis = 0 - the axis that we will use to calculate the missing value base on the stradegy, since we are using column, it will be 0 (default), otherwise we will use 1 for row.

we need to define where imputer will work on to fill the missing data.  

    imputer = imputer.fit(X[:, 1:3])

the above will take every row from matrix X, and column index 1 and 2. (1:3 means from 1 up to 3, excluding 3);

    X[:, 1:3] = imputer.transform(X[:, 1:3])

finally we will transform the data with our imputer, and replace the missing result with the mean of the respective column. 

