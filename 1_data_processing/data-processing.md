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

### Categorical Data
In our dataset, there are 2 categorical data, Country and Purchased. Since machine learning is equation based, we need to encode our variable into numbers. We will use...

    from sklearn.preprocessing import LabelEncoder

we will transform the existing catogorial column into numbered column.

    labelencoder_X = LabelEncoder()
    X[:, 0] = labelencoder_X.fit_transform(X[:,0])

However, just by turning column into number is not good enough. Since number express an relationship (1 > 0, 2 < 3, etc). Hence we will need dummy columns. dummy columns will separate each categories into multiple column, with bool to indicate if that row belongs to that category. to do this, we can leverage onehotencoder class from sklearn.

    onehotencoder = OneHotEncoder(categorical_features=[0])
    X = onehotencoder.fit_transform(X).toarray()
    
since purchased is a dependent variable, our machine learning equation will know that this is a categorical data. only label encoder will be needed. 

### Splitting Dataset into Trainning Set and Test Set
we need 2 set of data so we can test how effective our machine learning model is. we can use sklearn library to help us. 

    from sklearn.cross_validation import train_test_split
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state = 0)

here we have train_test_split which will take our matrix, X and Y and create 2 set of data, with a test size of 20% and 80% train set base on the original data size. 

### Feature Scaling 

