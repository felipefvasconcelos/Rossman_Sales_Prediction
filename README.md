# Rossmann_Sales_Prediction

This repository contains all steps based on CRISP-DS process model methodology to build a prediction sales model for a large drugstore chain. The data used in this model is available at the [Rossmann Store Sales competition page ate Kaggle.](https://www.kaggle.com/competitions/rossmann-store-sales/overview/description)

All information below is fictional.

## 1. Business Problem

Rossmann is one of largest drug store chain in Europe, operating over 3,000 drug stores in 7 countries across the continent.

Recently, the CFO received the task to renovate Rossmann stores and, in order to decide the amount of money each store will receive in the next period budget for renovation, he or she wants to know how much each store will sell in the next six weeks.

Therefore, this project was developed to use historical data from the stores to create a model that predicts sales in the next six weeks.

## 2. Data

The data used in this project can be found at:<br>
https://www.kaggle.com/competitions/rossmann-store-sales/data
<br>

<details><summary>Click here to see the original attibutes table</summary><br>
  
Attribute | Definition
------------ | -------------
|Id  | an Id that represents a (Store, Date) duple within the test set|
|Store | a unique Id for each store|
|Sales| the turnover for any given day (this is what you are predicting)|
|Customers | the number of customers on a given day|
|Open | an indicator for whether the store was open: 0 = closed, 1 = open|
|StateHoliday  | indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all schools are closed on public holidays and weekends. a = public holiday, b = Easter holiday, c = Christmas, 0 = None|
|SchoolHoliday | indicates if the (Store, Date) was affected by the closure of public schools|
|StoreType| differentiates between 4 different store models: a, b, c, d|
|Assortment | describes an assortment level: a = basic, b = extra, c = extended|
|CompetitionDistance | distance in meters to the nearest competitor store|
|CompetitionOpenSince[Month/Year]| Agives the approximate year and month of the time the nearest competitor was opened|
|Promo  | indicates whether a store is running a promo on that day|
|Promo2 | Promo2 is a continuing and consecutive promotion for some stores: 0 = store is not participating, 1 = store is participating|
|Promo2Since[Year/Week]  | describes the year and calendar week when the store started participating in Promo2|
|PromoInterval | describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. "Feb,May,Aug,Nov" means each round starts in February, May, August, November of any given year for that store|
</details>


<details><summary>Click here to see the created attibutes table in Feature Engineering session</summary><br>
  
Attribute | Definition
------------ | -------------
|year  | year the sale took place|
|month | month the sale took place|
|day| day the sale took place|
|week_of_year | week number of the year the sale took place|
|year_week | year and week number the sale took place|
|competition_time_month  | number of months competition started|
|promo_time_week| number of weeks since promotion has began based on sales date|
</details>

## 3. Business Assumptions

* For the stores with missing <i>"CompetitionDistance"</i> it was assigned a large distance, assuming that there is no competidor nearby.
* All lines with values in the column <i>"Open"</i> equal to 0 (meaning store closed) were removed.
* For all lines with missing values for <i>"CompetitionOpenSince[Month/Year]"</i> and <i>"Promo2Since[Year/Week]"</i>, the missing value was filled using the <i>"Date"</i>.

## 4. Solution Strategy

1. Data Description Analysis
2. Feature Engineering
3. Data Filtering
4. Exploratory Data Analysis
5. Data Preparation
6. Feature Selection
7. Machine Learning Modeling 
8. Hyperparameter Fine Tuning
9. Understand Model Performance
10. Deploy

## 5. Tools and Machine Learning Models

* Python 3.8.13
* Boruta as feature selector
* Linear Regression
* Regularized Linear Regression (LASSO)
* Random Forest Regressor
* XGBoost Regressor

## 6. Models Performance

The image below shows values of MAE (Mean Absolute Error), MAPE (Mean Absolute Percentage Error) and RMSE (Root-Mean_Square Deviation) for each model after performing Cross-Validation.

<img src="https://github.com/felipefvasconcelos/Rossman_Sales_Prediction/blob/main/assets/cross_val.png" width="500" height="150"><br>

Even though Random Forest Regressor model presented a slightly better performance, it was decided to proceed with XGBoost Regressor model because of the signicant lower memory and time consuming.

After running hyperparameter fine tuning for XGBoost Regressor model, the final performance was found as showed below.

<img src="https://github.com/felipefvasconcelos/Rossman_Sales_Prediction/blob/main/assets/final_performance.png" width="300" height="50"><br>

Error (real sales - prediction) scatter plot:

<img src="https://github.com/felipefvasconcelos/Rossman_Sales_Prediction/blob/main/assets/error.png" width="600" height="275"><br>

## 7. Business Results

According to the model, in the next six weeks all stores together will sell R$ 285,047,136.00. Assuming the error found after running fine tuning, we can assume that the stores will sell R$ 284,322,899.11 in the worst case scenario and R$ 285,771,403.20 in the best case scenario.

<img src="https://github.com/felipefvasconcelos/Rossman_Sales_Prediction/blob/main/assets/Scenarios.png" width="300" height="150"><br>

## 8. Telegram Bot

It was created a Telegram Bot in order to easily accesss predictions for individual stores by texting the store number you want the see the sales prediction. Bot can be accessed at https://t.me/rossmann_ffv_bot.

## 9. Conclusion

The objective of this project was to simulate a real life business problem and address the solution using Machine Learning models. By using CRISP-DS methodoly, it was possible to build an organized structure in order to understand the business problem, analyse the data, test models and finally provide an accurate sales predictions for the stores. 

## 10. Next Steps
Next step would be run a second cycle for CRISP-DM proccess with focus on following points:
* Create new and more relevant parameter at feature engineering.
* Create more hypotesis in order to find more relevant variables.
* Test more Machine Learning models.
* Improve messages in the Telegram Bot.
<br>

---
## References:

* Datasets Rossmann Store Sales from [Kaggle](https://www.kaggle.com/competitions/rossmann-store-sales/data)
* Variables meaning on [Kaggle discussion](https://www.kaggle.com/competitions/rossmann-store-sales/overview)
* Blog [Seja um Data Scientist](https://sejaumdatascientist.com/os-5-projetos-de-data-science-que-fara-o-recrutador-olhar-para-voce/)
