Dominos - Predictive Purchase Order System

Objectives:
To forecast the pizza sales for a week future and provide an Inventory with Ingredients required for the Pizza sales next week. 
Also to prepare a Purchase order for the Pizza sales ingredients.

Libraries Used:
•	Pandas
•	Numpy
•	Seaborn
•	Matplotlib
•	Scikit learn
•	Statsmodels
•	Pmdarima
•	Prophet
•	Pickle
•	Tensorflow
•	Holidays
•	Itertools
•	Datetime

Datasets: (Note: the code was executed from Google Colab hence for the folder path '/content/drive/MyDrive/Colab Notebooks/' can be removed while executing locally)
Pizza Sale:
•	Columns: 
pizza_id, order_id, pizza_name_id, quantity, order_date, order_time, unit_price, total_price, pizza_size, pizza_category, pizza_ingredients
•	Shape: 
(48620, 12)

Pizza Ingredients:
•	Columns:
pizza_name_id, pizza_name, pizza_ingredients, Items_Qty_In_Grams
•	Shape:
(518, 4)


Data processing:
	The missing values in the Pizza_sales data is filled by the dictionary mapping method and unit price to total price conversion.
	The missing values in the Pizza_Ingredients data is filled by the mean of the data.

Feature Engineering:
	The order date field is split into the Year, Month, Day, Hours, time.
	With the help of holidays library, the holiday column is set as True or False if the order date is a holiday
	With help of date time, the weekends are calculated and considered as promotional offers days and the Offer columns is set as True or False if the order date is Saturday/Sunday.
	We can see that the pizzas are sold highly during the Weekends and Holidays rather normal days.
	The most populous Pizza is the California Chicken Pizza with more than 10000 units sold.
	The large size pizza is sold mostly.
	The pizza sales and ingredients datasets are merged as Merged Dataset for model selection, training and evaluation.

Models:
	ARIMA Model:
•	Weekly pizza sales data frame is created for the ARIMA model training.
•	Parameters (p,d,q) : (3,1,5)
•	MAPE = 0.1976

SARIMA Model:
•	Weekly pizza sales data frame is created for the SARIMA model training.
•	MAPE = 0.2327

Prophet Model:
•	Daily sales date field is converted to date time using datetime library and Weekly pizza sales data frame is created for the Prophet model training.
•	MAPE = 0.2163

Linear Regression Prediction:
•	Weekly pizza sales data frame is created for the Linear Regression model training.
•	The order date field is split into the week, day, month and year
•	The above data is given as input for Linear Prediction model
•	MAPE = 0.1906

LSTM Model:
•	Weekly pizza sales data frame is created for the LSTM model training.
•	The data is normalized using MinMaxScaler
•	Input for LSTM model training is created by create_lstm_dataset
•	MAPE = 0.2493

Sales Forecasting:
	From the MAPE scores, we can see that the Linear Regression Prediction model is best.
	prepare_weekly_sales_by_pizza function returns the quantity of pizza sold in a week by pizza_name_id
	forecast_sales_per_pizza_type_linear_regression is used to foresee the pizza type and quantity prediction.
	forecast_next_week_sales_by_pizza_type_linear_regression forecasts the pizza type and quantity prediction for the next 1 week.
	The model is then saved as best_model.pkl  and can be loaded for future forecasts.

Ingredient Calculation:
	The best_model.pkl is loaded as loaded model
	The next 7 days is created as an array using datetime library
	The future dates are converted in to a dataframe using create_regression_features
	The forecasting is predicted using the best_model.pkl and the output is mapped as predicted_quantity weight in grams.
	The ingredients predicted grouped by pizza_ingredients is exported as predicted_ingredient_totals.csv 

Purchase Order Creation:
	The ingredients predicted is exported as Predicted Data.csv 
