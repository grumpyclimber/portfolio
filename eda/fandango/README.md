In this project we'll analyze movie ratings data from 2015 and 2016 to determine whether there has been any change in Fandango's rating 
system after [Hickey's analysis](https://fivethirtyeight.com/features/fandango-movies-ratings/). **This is an extended version of analysis:
I've followed a hunch, that money is a very important factor in ratings.** I've gathered additional budget data and analysed its corelation 
with movie ratings.

**Part 1**

The first part doesn't differ much from other notebooks on the matter you can find on the internet. It's a brief and simple attempt at answering the question: Does Fandango still inflate the ratings? It is a good entry point to our analysis in part 2.

**Part 2**

Having done the basic analysis on part 1, I came to conclusion that we need more data! My theory is not groundbreaking but I'will prove it: money is a very important factor in Fandango ratings, not only the amout of money involved in the movie but also where is it coming from. To perform the analysis in part 2, we'll need to aquire more data:
* scrape Wikipedia pages of each movie for budget data and for distribution company data (more on that topic here: [how I found the link to every movie from Fandango dataset](https://github.com/grumpyclimber/portfolio/tree/main/other/wiki_scrape))
* analyze the ratings based on the new data
![sum_budgets](https://user-images.githubusercontent.com/87883118/144156554-16fb6774-b951-4ab5-aaee-f0733f525030.png)
