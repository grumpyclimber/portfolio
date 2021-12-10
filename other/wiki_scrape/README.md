**TL;DR: I wrote a function to scrape Wikipedia for movie budgets:**

While doing my [Star Wars project](https://github.com/grumpyclimber/portfolio/tree/main/eda/star_wars), I did a basic scrape of movie data using Wikipedia library. That gave me an idea how to expand on the [fandango project](https://github.com/grumpyclimber/portfolio/tree/main/eda/fandango) - scrape movie budget data and analyse rating shift based on the budget... and other factors I can scrape from the page.

But for now I need to scrape the budget data first, Wikipedia library can't deliver that, I imagine that Wikipedia API would be a good way to do it 
(haven't touched that topic yet it's on the list of things to do) but I've wanted to try scraping the data from a webpage (because I've never done it) - I suspected that it won't be easy - Somehow I had to find the links to those movies wikipedia websites! 
here's how I've done it:

[notebook](https://github.com/grumpyclimber/portfolio/blob/main/wiki_scrape/scrape_wiki.ipynb)

After a while I've started using the above function for scraping distribution company data as well. Repeating the whole process, just to scrape 1 more value seemed,
very inefficient. Combine that with the fact that sometimes the first result is not a movie page, led me to a second improved version of the scraping function:

[notebook](https://github.com/grumpyclimber/portfolio/blob/main/wiki_scrape/scrape_wiki_vol2.ipynb)
