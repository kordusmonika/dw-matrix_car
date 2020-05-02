Car price forecasting with DataWorkshop 

1.Notebook: day2, day3, day4, day5 is my first attempt to approach car price dataset lead by DataWorkshop Challenge (Transformation 2).

2. After a while I decided to get back to car dataset and transfer the knowledge I've learned over the months.
All the notebooks I will name with prefix _update. The aim of my second attempt is to progress a bit more on a given dataset

ad.1 day2_update: 
Look almost the same. We focus on the visualization here. We extracted a target variable: 'price_value' and started investigating the correlation within the dataset. The brand ('param_marka-pojazdu'), colour ('param_kolor') and origin ('param_kraj-pochodzenia') showed the relationship with the target variable and allowed for the follwoing conclusions:

1. The most expensive car has color white and the cheapest is green.
2. The most common color on the street are 'black' and 'silver', where silver is at the end of the line (together with green) and quite well explains its popularity among others
3. We dicovered a niche with the following colors: beige, yellow, purple and gold
4. The top 3 country of origin are: Germany, Poland and France
5. On average, we prefer to choose such brands as: Volkswagen, Ford, BMW, Mercedes-Benz, Toyota, Skoda. 
6. Five cabin car is a common standard with 1.9 engine power

ad.2 day_3_update
There are 155 features. Our goal is to determine the most important ones. We’ll start from the basics - dummy model, to get a baseline for further improvements. Success metric is MAE(mean absolute error starting with 39 465 zl.)
The price_currency column has PLN (99%) and EUR(1.9%) values. The minority, EUR should not impact our dataset significantly, so we deleted them. The majority of features are categorical, therefore we proceeded to pd.factorize(). The final score shrinked to 19566 zl. 

Thanks to eli5 library we could easily present the most valuable features. Top 4 are:
1.	param_faktura-vat__cat
2.	param_naped__cat
3.	param_stan__cat
4.	param_rok-produkcji__cat
The next  natural step  is to explore at least some of them and advance on feature engineering

ad.day_4__update
Run XGB model with MSE: 18718. The top most important features were selected and used to tune model again. The best score was : 13 371 zl.

ad.day5__update
There are around 12 parameters in XGBoost. Each of which should be carefully selected to receive the best score. We will use hyperopt library (Bayesian optimization) to optimize our model.

Hyperopt optimization is divided into three parts:
1.	Objective function :  takes parameters as an input and decides which ones are the best
2.	Space: parameters passed as input  to obj_funct. You decide about the ranges and structure (uniform, norm, hp.choice, hp.quniform)
3.	Best score: take all that you have and use fmin(minimum function) to combine it. You will use tpe.suggest here and publicly determine max_eval – no.of iterations that you want to train your model on.


