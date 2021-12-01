This is my second attempt at ML, this time I'm learning a linear regression model. Using this model we're trying to predict house prices based on various property features.

Some of the concepts we'll touch upon in this project:

* Linear regression - we'll use a linear regression model to forecast the house prices. 
* Outliers removal - removing extreme values from the dataset, those values create a noise that's not digested very well by our model.
* Feature engineering - some of the columns containt duplicated or very similar data. We'll try to reduce the number of columns by merging some of them. During that process, we'll try to amplify the features that have a higher impact on the price.
* Overfitting - we'll create a validation set to test our model at the very end of the project.
* We'll also start conducting more and more data processing inside functions - to preserve memory, it's a good start before working on a [large data project](https://github.com/grumpyclimber/portfolio/tree/main/taxis_big_ML)

Here's an example plot of the results:

![price_prediction](https://user-images.githubusercontent.com/87883118/141601800-fefaa74a-0318-48d8-9d0b-1157d02f1b68.jpg)

**Links:**
* [Dataset](https://github.com/grumpyclimber/portfolio/blob/main/ML_house_prices/AmesHousing.tsv) 
* [Notebook](https://github.com/grumpyclimber/portfolio/blob/main/ML_house_prices/houses_final.ipynb)

**Articles and posts that were helpful:** 
* [Feature engineering](https://www.kaggle.com/c/home-data-for-ml-course/discussion/100526#652503)
* [Outliers removal](https://towardsdatascience.com/ways-to-detect-and-remove-the-outliers-404d16608dba) 
* [Overfitting](https://machinelearningmastery.com/overfitting-and-underfitting-with-machine-learning-algorithms/)
* [Memory usage](https://www.kaggle.com/pavansanagapati/14-simple-tips-to-save-ram-memory-for-1-gb-dataset#Technique-10:-Memory-leaks)




