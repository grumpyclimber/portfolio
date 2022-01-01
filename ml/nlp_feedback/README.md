Dataquest offers online, project-based data science courses focused on data analysis using R and Python. Part of every course is a hands on project to practice your skills. After finishing your project, the platform encourages you to publish it on their forum to gather feedback. 

A while ago I've started writing a [generic feedback post](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/feedback.md). I wanted to compile all my usual project feedback remarks into 1 list. So that everyone can have a read before/ after they publish their project and check if they still can do some work. 

That made me thinking: why don't include other peoples feedback as well? I've started wondering how many published projects received at least 1 reply on Dataquest's forum? Currently (November 2021) that number sits at 1102 posts. At this stage this stopped looking like writing a post, and started looking like a data analysis project...

Step 1:
Scrape all the necessary data (project posts)

Step 2:
Clean data - we only want to analyze the posts with at least 1 reply, we also have to do some text cleaning

Step 3:
Analyze data

Step 4:
ML

Techniques/ topics I've touched upon in this project: 
NLP, web scraping, n-grams, stemming, tokenization, TF-IDF, Wordcloud, Supervised ML, Kmeans clustering

Files in this folder:
1. [notebook](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/dq_feedback.ipynb) - the projects notebook (this is where the magic happens), all of the steps briefly presented in one notebook, if you're after a deeper analysis and coding experience - check out the individual notebooks for each step:
    * [scraping notebook](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/dq-scraping.ipynb) - web scraping notebook, presenting how to extract all the data from the website
    * [nlp_analysis notebook](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/eda-on-feedback-v1.ipynb) - notebook with basic EDA on numerical data and expanded NLP analysis of the text data
2. [feedback](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/feedback.md) - generic feedback post I've written (that's how it all started)
3. [html file](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/projects.html) - html file of the main thread of all the published projects on DQs forum
4. [dataset](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/dq.csv) - csv file containing all the feedback posts I've scraped for the first (brief) notebook
5. [second dataset](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/dq_v2.csv) - csv file containing all the feedback posts I've scraped for the second notebook

![plot](https://user-images.githubusercontent.com/87883118/144156872-8d664c4f-abea-4a9e-930e-95e00bc335ec.png)
