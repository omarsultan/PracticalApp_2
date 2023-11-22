# PCMLAI Practical Application 2
This project detials the effort to help a used car dealership develop a predictive tool to help better price cars.  The process will folwlthe CRISP-DM fraemwork.

## Business Understanding
The dealership wants to be able to accurately predict what a customer will pay for a used car. They need a simple, easy to implement model that will predict price based on features of the car the dealership can easily assess (age, mileage, condition, etc). Currently, the pricing is dependent on human judgement and the owner wants an aporoach that is more consistent and empirical. The expected business impact of more accurate pricing is both an increase in volume of sales and improves profitability.

## Data Understanding
We want to explore the features available in the dataset and get some validation from the customer that they seem relevant to solving the the problem.
We want to assess if we have enough data to model, make sure it is relevent and ensure we be able to update the data in the future to maintain model performance.
Finally, we want to assess the quality of the date--is there a large amount of missing data, especially for features that seem important and, for the missing data, can we credibly fill in the gaps. Conversely, if we drop missing missing data, so we drop below critical mass.
At this point, it would also be good to some basic visualizations to see if there are anby obvious relationships.

##### The raw data
![Raw data](https://github.com/omarsultan/PracticalApp_2/blob/main/images/raw-data.png)

## Data Preparation
There are a number of steps to take to prepare the data:
- Remove outliers for pricing and date--we don't want odd prices (very high or very low) swaying the model and we don't want decades old data that might not be relevant
- Futher filter the data for cars in a price range the dealership is likely to envounter
- Drop columns like 'ID' and 'VIN' that are not useful for modeling
- Fill in the missing data (or choose to drop the row or column). Decide if it is possible to impute missing values from other data in the row (i.e. using age to guess condition) or use one of the fill modes like ffill or mean, etc
- Finally, split the data in training and test sets

##### Price outliers
![Outlilers](https://github.com/omarsultan/PracticalApp_2/blob/main/images/outliers.png)

##### Quite a bit of missing data
![Missing data](https://github.com/omarsultan/PracticalApp_2/blob/main/images/missing.png)

##### The clean dataset
![Clean data](https://github.com/omarsultan/PracticalApp_2/blob/main/images/clean.png)

##### Dataset sample
![Sample of the dataset](https://github.com/omarsultan/PracticalApp_2/blob/main/images/sample.png)

##### Histogra of numerica features
![Histogra of numeric features](https://github.com/omarsultan/PracticalApp_2/blob/main/images/hist.png)

##### df.describe
![Output of df.describe](https://github.com/omarsultan/PracticalApp_2/blob/main/images/describe.png)

*The cleaning process is detailed in the "Clean" Jupyter Notebook*

## Modeling
Once we encoded catagorical data, the data set got cumbersome so made some educated guesses on what would be more relevant. We looked at OLS, Ridge and Lasso modeling and the error rates were actually quite close.  Looking at featrue significance for both the Ridge and Lasso models showed some consistency. 

*The modeling process is detailed in the "Analysis" Jupyter Notebook*

## Evaluation
Between the consistency of significant feautures and the close error rates, to some degree, it probably does not make much difference which model is used--they would probably perform in a similar manner. While a bit counter-intuitive, it might not be a bad idea to run a coupel of predicions by the sales people. While the owner wants a more empricl approach, it would be a mistake to ignore the sales people's experience and intuition to help validate the model.

##### OLS model significant features
![OLS model significant featurest](https://github.com/omarsultan/PracticalApp_2/blob/main/images/ols.png)

##### Ridge model significant features
![Ridge model significant features](https://github.com/omarsultan/PracticalApp_2/blob/main/images/ridge.png)

##### Lasso model significant features
![Lasso model significang features](https://github.com/omarsultan/PracticalApp_2/blob/main/images/lasso.png)

##### Comparative model error rates
![Comparative model error rates](https://github.com/omarsultan/PracticalApp_2/blob/main/images/error.png)


## Deployment
We will take the significant features and coefficients we discoverd through our modeling and codify them in something simple and familar like a spreadsheet. So, all the sales people need to do is plug in the info on the features we have identifeid and it will spit out target price. We should make sure the dealership understand the uncertainty in the price prediction. Maybe this is also something that can be handled in the spreadsheet where it returns a target price +/- the uncertainty in the prediction.

Finally, there should be some mechanism to capture actual selling price so the model cna be refined over time and the dealership has some reporting on the impact/benefit of the forecasting tool.

