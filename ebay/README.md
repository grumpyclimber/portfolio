# Ebay car sales data analysis

This is the first project I've decided to publish. Apart from doing the usual data cleaning as requested by Dataquest for this project, I have chalanged myself to do a few additional tasks:
* extracted engine size from 'name' column where it was easily achieveble (in about 14500 rows) - this opened up a lot of new possibilities in analyzing the dataset:
![engine_ef](https://user-images.githubusercontent.com/87883118/144156016-0f4d7dd8-7303-40c0-9929-59964dd6b229.png)

* filled 4000 cells of power column with average power value for each brand respectively (instead of filling it with an average power value for the whole database)
* inspected rows with 'sontiage_autos' brand and reassigned 80% of these entries to their correct brand
* came across faulty data in post-2015 entries and removed it (see below)
![cars2015](https://user-images.githubusercontent.com/87883118/144155742-c2ddfffc-58f8-4fa4-92c7-ceaef31d874a.png)

* plotted average price data on the map of Germany
![map](https://user-images.githubusercontent.com/87883118/144156126-921fc51b-ae25-4c26-bae2-c7fc56ccc356.png)


libraries: Pandas, Numpy, Matplotlib, Geopandas

