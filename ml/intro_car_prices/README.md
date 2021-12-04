My first attempt at ML model, I've followed most of Dataquests quidance on the project, but added a bit of extra work from my side. It was a long battle, started with a simple trick to shine among many:
* check performance of 3 different versions of the dataset on different models

That led me to experimenting with random seeds and it was opening up a pandora box:
* I've ran all models on 100 random seed numbers to check how the model performs in 100 different cases, not in a single case (I'd really be grateful for feedback on that matter) instead of looking for the lowest result in those 100 runs . I was looking for a model that performed the best on average on 100 runs.
* I've checked plenty more column combinations (selecting just the top columns from single column model results is not the best solution)


![k_value](https://user-images.githubusercontent.com/87883118/144155457-4160caac-95c9-4ce8-adc7-33c235042f22.png)


[Dataset](https://archive.ics.uci.edu/ml/datasets/automobile) 

[Notebook](https://github.com/grumpyclimber/portfolio/blob/main/ml/intro_car_prices/cars_ml_small.ipynb) 
