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
* [notebook](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/dq_feedback.ipynb) - the projects notebook (this is where the magic happens)
* [feedback](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/feedback.md) - generic feedback post I've written (that's how it all started)
* [html file](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/projects.html) - main thread of all the published projects on DQs forum
* [dataset](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/dq.csv) - csv file containing all the feedback posts I've scraped 


![plot](https://user-images.githubusercontent.com/87883118/144156872-8d664c4f-abea-4a9e-930e-95e00bc335ec.png)
