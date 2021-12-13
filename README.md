# Portfolio
Hello world, here are my humble beginnings of a portfolio! Most of the below projects are based on well known datasets, but in each and every one of them I've pushed myself to outshine the standard scope of the project.  If I couldn't find anything new in the data, and my project would look the same as every other notebook, I've collected new data (like in [Fandango project](https://github.com/grumpyclimber/portfolio/tree/main/eda/fandango)). No idea or room for new data? Then I've grabbed a brush and worked on the visualizations. (eg. [Star Wars](https://github.com/grumpyclimber/portfolio/tree/main/eda/star_wars)). At this stage I'm focusing on machine learning projects. My newest addition is a [project feedback](https://github.com/grumpyclimber/portfolio/tree/main/ml/nlp_feedback) notebook, where I've used a web scraper to extract all the comments to students guided projects and analyzed that data. 

The portfolio is divided into 3 parts:

🔍 1. [Exploratory Data Analysis](https://github.com/grumpyclimber/portfolio#exploratory-data-analysis)  

🎰 2. [Machine Learning](#ml)

🪄 3. [Tricks and intros](#intros)

Get in touch: <td><a href="https://linkedin.com/in/kubalica" target="_blank" rel="noopener"><img src="https://icon.signature.email/social/linkedin-square-small-0077b5-FFFFFF.png" alt="LinkedIn icon" width="20" height="20" border="0" valign="bottom"/></a>&nbsp;&nbsp;<a href="https://stackoverflow.com/users/16519424/adam-kubalica" target="_blank" rel="noopener"><img src="https://icon.signature.email/social/stackoverflow-square-small-f48024-FFFFFF.png" alt="Stack icon" width="20" height="20" border="0"  valign="bottom" /></a>&nbsp;&nbsp;</td>

<a name="eda"></a>
# Exploratory Data Analysis

### :car: [Ebay cars](https://github.com/grumpyclimber/portfolio/tree/main/eda/ebay) - A deeper analysis of a well known car dataset. 
This dataset very often serves as an introduction to pandas. Students focused on surviving their first coding project forget to unleash their curiosity. Because of that the dataset has a lot of untapped potential: extracting engine size from the cars names, identyfing sontiage_autos, identyfying the issue with post-2015 entries to name a few. It's also a perfect dataset for a basic introduction to geopandas.

### 👾 [Star Wars](https://github.com/grumpyclimber/portfolio/tree/main/eda/star_wars) - This one is all about the style... 
Star Wars fans survey is a small dataset that doesn't give us a lot potential for analysis. To make it more interesting I've decided to work on the visuals of this notebook. Custom fonts, color palettes, and lots of plots. I've even plotted a death-star. The force is strong with this one.

###  :movie_camera: [Fandango](https://github.com/grumpyclimber/portfolio/tree/main/eda/fandango) - Extended version of Fandango ratings analysis. 
To dig deeper into Fandangos rating shift I've gathered more data, specifically distribution company and budget data for each movie. I've set up a BeautifulSoup scraper get the required information from Wikipedia. That gives us a better look how movie budgets and their distributors affect the ratings.   

### 🚑 [Road fatalities](https://github.com/grumpyclimber/portfolio/tree/main/straya_road_deaths) - A basic analysis of road fatalities on Australian roads
A bit of a break from recent ML projects - a quick EDA on a relatively simple dataset. Australian roads became much safer in the last 30 years. But that change doesn't affect everybody equally. Some social groups and locations are becoming more common in road fatalities.

---
<a name="ml"></a>
# Machine Learning

### 🚙 [ML car prices](https://github.com/grumpyclimber/portfolio/tree/main/ml/intro_car_prices) - Introduction to ML with k-nearest neighbors algorithm. 
I've extended the project with testing out multiple random seeds, checking many column combinations and different dataframe versions (based on cleaning techniques).

### 🏠 [ML house prices](https://github.com/grumpyclimber/portfolio/tree/main/ml/house_prices) - Building a linear regression model to predict house prices.
Multiple feature engineering layers to merge various numeric and categorical columns into 1. Using feature selection techniques and testing different outliers removal methods. 
### :taxi: [ML NYC taxi trips](https://github.com/grumpyclimber/portfolio/tree/main/ml/taxis_large) - An ongoing project with large datasets of NYC taxi trips.
The core idea of this project is to experience working with large data. Using pandas big data techniques or Dask library to manage importing and merging  datasets, all while trying to fit under strict memory limitations of a kaggle notebook.

### 📋 [Project feedback](https://github.com/grumpyclimber/portfolio/tree/main/ml/nlp_feedback) -  Scraping and analyzing projects feedback. 
Another BeautifulSoup scraping session gathered feedback to all of the published projects on Dataquest forum. Having gathered a lof of text data. I've tested different NLP techniques, applied supervised and unsupervised machine learning models to analyze text data.  

### 🚲 [Bike Sharing](https://github.com/grumpyclimber/portfolio/tree/main/ml/bikes) - Using multiple regression models to predict rental count
Random Forest hyperparameter optimization using GridSearch, gathering more weather data using meteostat, testing various regression models, small steps into stacking models: averaging predictions of multiple models and using neural network model as a meta model. 

---
<a name="intros"></a>
# Tricks and intros:
### 🔡 [Scraping data](https://github.com/grumpyclimber/portfolio/tree/main/other/wiki_scrape) - scraping data from Wikipedia pages.
Getting introduced to web-scraping with BeautifulSoup, we'll develop a function to extract budget data from the website. 

### :fishing_pole_and_fish: <a href="https://github.com/grumpyclimber/portfolio/tree/main/other/tricks">Tricks</a> - Mix of short and easy tricks, hacks and intros.
Giving back, improving on others work and explaining your work is an essential part of learning how to code. In this folder I'll try to include some of my notebook that can be helpful. 

### :globe_with_meridians: <a href="https://github.com/grumpyclimber/portfolio/tree/main/other/maps">Maps</a> - Quick and easy intro to geopandas.
Using the ebay dataset to conduct a quick tutorial to geospatial visualization with Geopandas.


---

languages: Python, HTML

libraries: 
* Pandas
* Numpy
* Matplotlib
* Geopandas
* Seaborn
* Scikit-learn
* Wikipedia
* Missingno
* BeautifulSoup
* Dask
* Textwrap
* Meteostat

Adam Kubalica
<td><a href="https://linkedin.com/in/kubalica" target="_blank" rel="noopener"><img src="https://icon.signature.email/social/linkedin-square-small-0077b5-FFFFFF.png" alt="LinkedIn icon" width="20" height="20" border="0" /></a>&nbsp;&nbsp;<a href="https://stackoverflow.com/users/16519424/adam-kubalica" target="_blank" rel="noopener"><img src="https://icon.signature.email/social/stackoverflow-square-small-f48024-FFFFFF.png" alt="Stack icon" width="20" height="20" border="0" /></a>&nbsp;&nbsp;</td>
