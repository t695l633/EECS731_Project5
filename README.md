# EECS731_Project5
Time Series Forecasting 

1. Set up a data science project structure in a new git repository in your GitHub account
2. Download the product demand data set from
https://www.kaggle.com/felixzhao/productdemandforecasting
3. Load the data set into panda data frames
4. Formulate one or two ideas on how feature engineering would help the data set to establish additional value using exploratory data analysis
5. Build one or more forecasting models to determine the demand for a particular product using the other columns as features
6. Document your process and results
7. Commit your notebook, source code, visualizations and other supporting files to the git repository in GitHub

# Intro
The goal of this project was to create a time series forecasting model to predict the demand of a certain product in the future, given it's past demand. Part of what differs in making a time series model is that instead of randomly creating a test train split, you train on "past" data and test on "future" data. For this project I chose to train on the first 90% of my data then test on the final 10%. Since we cannot run our algorithm on future data we do not have, we treat out most recent data as if it were future data.

# Feature Engineering
Many pieces of feature engineering were done to this data set to get it ready for my models. First, the "Date" column was read in as a datetime type so that it could be used later on. The warehouse column was label encoded, and the product and category columns were both converted to integers. Negative demand values were also removed from the table, as they were outliars that scewed the data set. Finally a "Days" column was added so that each demand would have a day count associated with it, and I could plot my data in order from the first to the last day. 

# Models 
I created 3 forecasting models to determine the demand for product 993, chosen arbitrarily because it had a large number of data points associated with it, and it was the first product seen in my data frame. 
1. The first forecasting model I created was a simple linear regression model. This performed extremely poorly, even after removing all negative demand values (likely the result of returns, or possibly incorrect data) my model had an R^2 value of ~ -0.002. Because this value was negative, it means that simply guessing the average demand would have led to better results.
2. The second forecasting model I created was a linear regression that used a 10 day moving average. This model works by taking the average of the previous 10 days for each point, and making that the point's value. While this did cut down significantly on variation, it did not do much to improve my results. This left me with an R^2 value of ~ -0.002 as well.
3. Finally, seeing as this was clearly not a linear data set, I chose to create a gradient boosting model over my data. Gradient boosting models work better than linear regression models for non-linear data sets, and I thought perhaps demand was seasonal each year. Unfortunately the gradient boosting model did even worse than my linear models, providing me with an R^2 value of ~ -0.005. 

# Results/ Conclusions
