# Economic Growth Analysis
As part of our NUS DSE1101 final project, we used a data set which comes from the Sala-i-Martin et al. (2004) paper published in American Economic Review which contains 139 observations and 71 variables, which aims to identify the factors most strongly associated with long-term economic growth and evaluate how well different modelling approaches capture these relationships. We performed our following analysis in R.

**Team Members:**

  * Julian
  * James

## Our Approach
  1. Data Cleaning
  2. Exploratory Data Analysis (EDA)
  3. Linear Regression with 3 Variables (Benchmark model)
  4. K-Nearest Neighbour(KNN) with 3 Variables
  5. Decision Tree
  6. Linear Regression with Variable Selection
  7. Evaluation

## Data Cleaning
We started our data cleaning by changing all variables to type numeric to ensure that empty variables which were reflected as '.' in the dataset changes to NA, allowing us to remove missing data easier. Following which, we removed observations where the outcome variable, `GR6096` is empty as supervised learning models required an outcome variable to predict. Subsequently, to maximise number of variables while keeping observations high, we decided to remove observations with at least 2 empty values and all variables with at least 1 empty value afterwards.

### Scaling of Continuous Variables
We identified and performed scaling on the continuous variables from our dataset as machine learning models such as KNN are highly sensitive to scaling as it uses euclidean distance as its distance metric.

## EDA
With the use of scatterplot, boxplot, correlation coefficient and p-values from a linear regression full model, we investigated the relationship between the following 6 variables namely, `GR6096`, `GDPCH60L`, `LIFE060`, `P60`, `AVELF` and `EAST`. We found that the correlation coefficient between `GR6096` and `LIFE060` is 0.5409, while the correlation coefficient between `GR6096` and `P60` is 0.5726, indicating a moderately strong positive relationship for both. We also found that `IPRICE1`, `GDPCH60L`, `PRIGHTS`, `CIV72` and `P60` had the top 5 coefficients with the lowest p-value when a linear regression full model was fitted, indicating stronger statistical association with `GR6096`.

## Benchmark model
Before implementing our machine learning models, we split the dataset using a 70/30 train-test split and set seed to ensure replicability. Based on our prior economic knowledge, we chose `GDPCH60L`, `P60` and `IPRICE1` as our top 3 predictors to predict `GR6096` as our benchmark model due to its simplicity and evaluated its accuracy using the out-of-sample root mean squared error.

## KNN
Using the same 3 predictors as above, we implemented a KNN model to predict `GR6096`. By making use of a leave-one-out cross validation, we found that the optimal K value for the number of neighbours is 12. Similarly, we evaluated its accuracy using the out-of-sample root mean squared error.

## Decision Tree
For our decision tree model, we started with a full, unpruned tree based on the training data. We then performed a cross validation using deviance to determine the optimal tree size. The pruned tree model only made use of 4 predictors namely, `YRSOPEN`, `TROPPOP`, `BUDDHA` and `P60`. Using our pruned model, we evaluated its accuracy using the out-of-sample root mean squared error.

## Linear Regression with Variable Selection
By making use of the `leaps` package in R, we performed a backward elimination to select the predictors that wil give the best in-sample prediction using the adjusted R-squared as our metric. We fitted our train data to a linear regression model using these predictors and evaluated its accuracy using the out-of-sample root mean squared error.

## Evaluation
Our benchmark model performed the best in this scenario with the lowest root mean squared error of 0.795. For this scenario, despite the possibility of finding a model to better predict out-of-sample growth, we belive that the computational effort needed would outweigh the marginal improvements in our model. Hence, it is not meaningful to pursue a model beyond our benchmark model. Based on our analysis, we also believe that human capital, wealth of the economy relative to other economies and capital accumulation are the key drivers of economic growth.
