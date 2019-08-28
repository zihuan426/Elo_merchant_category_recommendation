# Elo_merchant_category_recommendation (Kaggle)

## Introduction
This repository contains the Jupyter Notebook I wrote for the [Elo Kaggle Competition](https://www.kaggle.com/c/elo-merchant-category-recommendation). I got top 11% in this competition. This code produces predictions with root mean squared error (RMSE) 3.613 in the private leaderboard while the first place got 3.578.

## Description
Elo, one of the largest payment brands in Brazil, has built partnerships with merchants in order to offer promotions or discounts to cardholders. But do these promotions work for either the consumer or the merchant? Do customers enjoy their experience? Do merchants see repeat business? Personalization is key.
 
In this competition, the goal is to develop algorithms to identify and serve the most relevant opportunities to individuals, by uncovering signal in customer loyalty. Your input will improve customers’ lives and help Elo reduce unwanted campaigns, to create the right experience for customers.

## Data
Due to the [Competition Rules](https://www.kaggle.com/c/elo-merchant-category-recommendation/rules), the data cannot be shared. If you want to play with the data, you can download the competition dataset at [Elo Competition Dataset](https://www.kaggle.com/c/elo-merchant-category-recommendation/data).

## Main Idea
1. The provided datasets have historical transactions and new transactions, so the key to feature engineering for this competitin is how to appropriately aggregate transactions to credit card level:
    - groupby each category to get the sum, min, max, mean and var of the purchase amount
    - get the day difference between historical transactions and new transactions
    - generate finer aggregation using pandas pivot table
    - aggregate categorical feature in transactions with NLP embedding 
2. This kind of regression task works nicely with tree_based methods, I used LightGBM and XGBoost library along scikit-learn to make the predictions.
3. In model tuning stage, I used both manual training and auto training using BayesianOptimization package.
4. For stacking, I used methods as follows:
    - Create 3 LightGBM models with top 3 tuned parameters
    - Create 3 XGBoost models with top 3 tuned parameters
    - Create out-of-fold predictions for the above 6 models (Level 1)
    - Train a Rigde Regressor as level 2 model with level 1 features only
    
## Installation
To replicate the findings and execute the code in this repository you will need basically the following Python packages:
- Numpy
- pandas
- scikit-learn
- Xgboost
- LightGBM
- bayes_opt
