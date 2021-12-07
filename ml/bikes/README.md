In this notebook we'll build various machine learning models to predict the amount of rented bikes each day.

The dataset has multiple columns containing information about 
* time of the day
* month
* year 
* type of the day (holiday / working)
* multiple weather columns

We can quickly establish that time of the day is the most important feature for our predictive model:

![cns_hr](https://user-images.githubusercontent.com/87883118/145117816-a53385a2-fbc8-49c2-81cb-5716a7179480.png)

Second most important feature is the temperature data. This dataset contains only 2 years worth of entries, and we can notice a significant rise of rentals in the second year - thus year column also plays an important role in a Random Forest model:

![cols_importance](https://user-images.githubusercontent.com/87883118/145118116-6dc0bebb-22a4-4279-9ecd-a1065d35a165.png)

Before moving on to test other models, we'll use meteostat library to import more weather data:
* precipitation
* atmospheric pressure
* unfortunately meteostats weather station for Washington D.C. doesn't have sunshine time data 

After importing and filling in the missing weather data, we can move on to test a few different regression models:

![models](https://user-images.githubusercontent.com/87883118/145119051-1e65b65a-fe88-4e81-9039-805c14e974d3.png)

Having tested quite a few models we'll move on to stacking them together.

![final](https://user-images.githubusercontent.com/87883118/145120407-a9cb7a10-c43b-4388-a56c-a2cc92220999.png)
![final2](https://user-images.githubusercontent.com/87883118/145120412-7f706fd9-7d7d-4cc6-a117-74dd707e6f3b.png)

Our final models results:
* RMSE of test set: 37.34252077152997
* R2 score of training set: 0.9803606913767285
* R2 score of test set: 0.9582019271312862

**It's worth mentioning that to beat the results of single Random Forest or Gradient Boosting model, by a small margin. We had to use multiple model stacking methods that come at a big computational cost.**


**Links:**
* [Dataset](https://www.kaggle.com/marklvl/bike-sharing-dataset) 
* [Notebook](https://github.com/grumpyclimber/portfolio/blob/main/ml/bikes/bike_share.ipynb)
