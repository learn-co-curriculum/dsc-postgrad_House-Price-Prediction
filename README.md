![for sale context image from lending tree: https://www.lendingtree.com/home/mortgage/how-to-buy-a-house-when-your-current-home-hasnt-sold/](images/for-sale-header.jpg)

# Housing Price Prediction Project

## Project Goal

My project aims to predict the sale price of houses. By predicting the sale price of houses, a prospective buyer could have a good understanding of whether the house they are looking to buy is valued at about what you'd expect, given the data provided on the home. Conversely, a prospective seller could use this tool to determine what price to list for their home.

## Findings

My current preferred model is able to explain about 78% of the variance in the sale prices of homes, and on average predicts a sale price that is $24,244 away from the actual sale price.

## Data Source and Data Exploration

This data comes from a [Kaggle competition](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/) which provides details about homes in Ames, Iowa. 

The target variable shows that there are some outliers in the data, which are homes that were sold at much higher prices than most of the other homes in the dataset.

I used 33 columns for my analysis, which included variables about the age and quality of the house, the total size of both the lot and the house itself, the number of bedrooms and bathrooms, and additional features like any porch, garage, basement, etc.

## Data Preparation

Because I used only numeric columns, I did not perform any encoding techniques. However, I did scale my data, using Sci-Kit Learn's Robust Scaler.

## Modeling

I began with a baseline that predicts only the mean house price from the training data for each house. My final model is a Ridge regression model, which uses L-2 regularization to manage the multicollinearity between the features used in the model.

The most important feature to my preferred model was the Overall Quality of the home, according to permutation importance:

![feature importance from eli5 output for the ridge regression model](images/feature-importance-ridge.png)

## Evaluation

I used both the Coefficient of Determination (R2 Score) and Mean Absolute Error to evaluate my models. I wanted to make sure these two very different metrics were evaluated so I could see how my models are trending overall. The benefit of R2 Score is I can see how well my model explains the variance of the target, the house sale price, while the Mean Absolute Error is able to explain how off my predictions were on average in real dollar terms. I trained my model on two-thirds of the data for which I knew the actual sale price, then tested my results on the remaining third.

My final preferred model, a Ridge regression model, achieved an R2 Score of `.78` and a Mean Absolute Error of `24,244` on the test set. In real terms, this means the Ridge regression model explains about 78% of the variance of the target variable, the house sale price, and that on average my predictions are about $24,244 away from the actual value. 

## Next Steps

In the future I would like to first use more of the categorical features, and perhaps encode some of the discrete features I used in my final model. I would also like to then only use the most important features, perhaps by regularizing using both LASSO and Ridge through an ElasticNet model. I could also only use the top 5-10 features based on Permutation Importance. 

I'd also like to explore capping my training data so that I create a model that only works on houses priced up to a certain point. This would narrow the target audience of my model, but at the same time Could make it work better on houses that are priced within a specific range. Thus, if I received a result from my model outside that range I could know that my model is likely not accurately pricing that home and thus should be handled using different techniques or models. 

## Sources:

- [Data Source: Kaggle](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data)
- [README Header Image Source: Lending Tree](https://www.lendingtree.com/home/mortgage/how-to-buy-a-house-when-your-current-home-hasnt-sold/)
