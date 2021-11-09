This is an ongoing multiple notebooks project. Currently I am at the first stage: importing.


**The idea behind it all:**

A while ago I've asked a higher power (btw thanks higher power) to have a look at my portfolio and to my surprise I was flourished with glory, 
apparently the data battles I fought were bold and I was getting closer to being worthy, BUT:
* there were a few remarks and one of them was lack of merging with other datasets
* but the most interesting remark was data scalability  
  * my projects lacked the idea that memory is a limited resource
* we're going to assume that there were no other remarks


Having that knowledge I've started plotting a devious scheme in my head:
* import 2 or 3 years of NYC Taxi trips dataset into Kaggle
* merge with at least 1 more dataset (at this stage it's weather)
* analyze, build ML models
* do all of the above on Kaggle platform, where each notebook has 'only' 16gb of RAM
  * depends how you look at it it's a lot or not much at all, for an example: basic pandas data importing for May 2018 used 2.8 Gb of RAM. One month 2.8 Gb - We want to have at least 24 months!  We're going to have to get creative


ATM I'm focusing on importing large dataset:
* setting up a pipeline for importing and merging data, learning basic memory-saving tricks to fit under 16 Gb of RAM
  * I've prepared a [pandas-based solution](https://github.com/grumpyclimber/portfolio/blob/main/taxis_big_ML/taxis_imports_pd.ipynb) - to even make it possible with Pandas I had to introduce several techniques, that were new to me:
    * I've started using chunksize atribute 
    * Deleting the old dataframes when no longer needed and using gc.collect() to clean memory
    * Performing dataframe merging and other operations inside functions to save on memory
<!--   * so far I haven't been able to create a Dask-only based solution, but I've made big improvements to the speed of importing data from the source using Dask library (then changing it to pandas), unfortunatelly it came with a price: 70% more RAM usage, here's the [notebook](https://github.com/grumpyclimber/portfolio/blob/main/taxis_big_ML/taxis_imports_dask_pd.ipynb)
 
 **Importing 5% sample for every month of years: 2017 and 2018:**
 |libraries|pandas|dask then pandas|
 |---|---|---|
 |time|27 mins|20 mins|
 |RAM usage|3.1 GB|5.3 GB| -->
