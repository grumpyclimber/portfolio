# NLP on guided projects feedback

Do you share your projects in the Dataquest community? I do!  I have benefited a lot from various people sharing their insights on my work. As I've progressed, I've started giving back and showing other people what I would have done differently in their notebooks. I've even started writing a [generic post](https://github.com/grumpyclimber/portfolio/blob/main/ml/nlp_feedback/feedback.md) about the most important comments on our projects. To include more interesting content in my post, I've started looking at other users feedback to guided projects. **Wait a second... What if we combine all of the feedback data to every guided project in one dataset?**

This article is the first post in a series of posts describing my project. To really benefit from this article you should have a good understanding of pandas library and be aware of regex usage in cleaning data. We'll focus on web scraping, so elementary HTML (language used for creating websites) is very helpful, but you should survive without it.

### Structure
I have divided this project into three stages, all of them are not that complicated on their own, but combining them together may feel a bit overwhelming. Every stage will be covered in a separate article:

* Part 1: Gather the data - We'll use the BeautifulSoup library to scrape all the necessary string values from the website and store them in a pandas dataframe. This is the part we'll discuss in the below article.
* Part 2: Clean and analyse the data - Web scraping very often delivers 'dirty' text values. It is normal for the scraper to pick up a few extra signs or lines of HTML during the process. We'll use regular expression techniques to transform that data into a more useful format and analyze it.
* Part 3: Use machine learning models on the data. Why perform the analysis yourself, when you can send the machine to do that work for you? Expanding on our work from part 2, we'll test different machine learning approaches to analyse text data. 

You can access all the projects files on MY [GitHub](https://github.com/grumpyclimber/portfolio/tree/main/ml/nlp_feedback). I'll be adding more files and fine-tuning the existing ones as I publish the next articles.

Ready? Let's get to work:
# Part 1 -  Web scraping for Natural Language Processing project
If you haven't used BeautifulSoup yet, then I encourage you to check my [introduction notebook](https://github.com/grumpyclimber/portfolio/tree/main/other/wiki_scrape). It follows a similar path that we're going to take: scraping not one, but many websites. Also, here's a bit more [in depth article](https://www.dataquest.io/blog/web-scraping-python-using-beautiful-soup/) on Dataquest introducing us to web scraping.

Let's have a look at how the actual guided project post category looks, so we can have a better idea of what we want to achieve:

<img width="942" alt="main" src="https://user-images.githubusercontent.com/87883118/144956101-27b15dc3-4ad2-473f-870a-faa241819d02.png">

This is the main thread of Guided Projects. It contains all of our Guided Projects, that we've decided to publish. Most of them received a reply with some comments - we're interested in the contents of that reply, here's an example post:

<img width="918" alt="feedback" src="https://user-images.githubusercontent.com/87883118/144956671-3c8dc0bc-1922-4a12-9c73-5e4b549d93af.png">


In this post, Michael published his project and Elena replied with some remarks to his work. We're interested in scraping only the content of Elena's remarks. It is not going to be as easy as scraping one website. We want to scrape a specific part of many websites, to which we don't have the links...yet. Here's the plan of attack:
1. We don't have the links to all of the guided project posts - we need to extract them, which means we'll have to scrape the main thread of guided projects
2. After scraping the main thread we'll create a dataframe containing posts, titles, links, views and the number of replies
  * We'll filter out posts with no replies
3. The remaining dataset should contain only the posts that received feedback and the links to those posts - we can commence scraping the actual individual posts

## Very basic HTML introduction:

Before we start, I have to ask: have you ever seen a HTML code? It differs from Python. If you've never experienced HTML code, here's a **very** basic example of a table in HTML:
```html
<html>
<body>
<table border=1>
  <tr>
    <td>Emil</td>
    <td>Tobias</td>
   <td><a href="https://www.dataquest.io/">dataquest</a></td>
  </tr>
</table>
 </body>
 </html>
```
<html>
<body>
<table border=1>
  <tr>
    <td>Emil</td>
    <td>Tobias</td>
    <td><a href="https://www.dataquest.io/">dataquest</a></td>
  </tr>
</table>
</body>
</html>
 
In HTML we use tags to define elements. Many elements have an opening tag and a closing tag — for example ```<table>``` opens up the building of a table and at the very end of coding the table, we write ```</table>``` to close it. This table has 1 row (have you guessed it's ```<tr>``` for a row?) and 3 cells in that row. In the third cell we've spiced up the atmosphere a little - we used a link (```<a href=...>```). HTML tags can have attributes (we've used 'border' attribute in 'table' tag and 'href' attribute in 'a' tag).   

The whole concept of webscraping is to extract (scrape) specific elements of a website.

## Step 1: web scraping the main thread of guided projects 

### Inspecting the website:

We'll begin with inspecting the contents of the whole website: https://community.dataquest.io/c/share/guided-project/55
We can use our browser for that, I use Chrome. Just hover your mouse above the title of the post right-click it and choose Inspect, (BUT pay attention! 
I've chosen a post that's a few posts below the top - just in case the first post has a different class). 

Now we can look at the code of the website, when you hover your mouse cursor above certain elements of the code in the right window, the browser will highlight that element in the left window, in the below example my cursor is hovering above the ```<tr data-topic-id=...>``` and on the left side we can observe a big chunk of the website being highlighted:

<img width="1092" alt="inspect" src="https://user-images.githubusercontent.com/87883118/145134328-abb52874-0bc5-4bc9-a952-662d44fe00d6.png">

### First attempts at web scraping:

For our first attempt we'll try to obtain only the links of every post. You can notice that the actual link has a class 'title raw-link raw-topic-link', it's in the second line of the code below:

```html
<a href="/t/predicting-bike-rentals-with-machine-learning-optimization-of-the-linear-model/558618/3" role="heading"
   level="2" class="title raw-link raw-topic-link" data-topic-id="558618"><span dir="ltr">Predicting Bike Rentals 
  With Machine Learning, Optimization of the Linear Model</span></a>
```
We'll use the below code to scrape all the links with that class into one list and see how many we've managed to extract:

```python
# imports:
from bs4 import BeautifulSoup
from urllib.request import urlopen, Request

# step 1 lets scrape the guided project website with all the posts:
url = "https://community.dataquest.io/c/share/guided-project/55"
html = urlopen(url)
soup = BeautifulSoup(html, 'html.parser')

# look for every 'a' tag with 'class' title raw-link raw-topic-link:
list_all = soup.find_all("a", class_="title raw-link raw-topic-link")

# check how many elements we've extracted:
len(list_all)
```
\[Output]: 30

Our list has only 30 elements! We were expecting a bigger number, what happened? Unfortunately, we're trying to scrape a dynamic website. (a more [in depth article](https://www.zesty.io/mindshare/marketing-technology/dynamic-vs-static-websites/) on the matter). Dataquest loads only the first 30 posts when our browser opens the forums page, if we want to see more we have to scroll down. But how do we program our scraper to scroll down? [Selenium](https://selenium-python.readthedocs.io/) is a go-to solution for that issue but we're going to use something much simpler: 
* scroll down to the bottom of the website
* when we reach the end save the website as a file
* instead of processing a link with BeautifulSoup, we'll process that file

Let's get to scrolling down:

![20211207_132125](https://user-images.githubusercontent.com/87883118/145162982-e907978a-5ff0-49ca-8830-f377618ddb52.jpg)

Yes, that is an actual fork pushing down the 'down arrow' on the keyboard, weighted down with an empty coffee cup (the author of this post does not encourage any unordinary use of cutlery or dishware around your electronic equipment). Having scrolled down to the very bottom, we can save the website using > File > Save Page As... Now we can load that file into our notebook and commence scraping, this time we'll target every new row ```tr```. Because ultimately we're not interested in scraping just the links, we want to extract as much data as possible. As you remember when we hovered the mouse cursor over ```<tr ...>``` tag a lot has been highlighted. Not only the title, with a link, but also the number of replies, views etc.

```python
import codecs
# this is the file of the website, after scrolling all the way down:
file = codecs.open("../input/dq-projects/projects.html", "r", "utf-8")
# parse the file:
parser = BeautifulSoup(file, 'html.parser')

# look for every 'tr' tag, scrape its contents and create a pandas series from the list:
list_all = parser.find_all('tr')
series_4_df = pd.Series(list_all)

# create a dataframe from pandas series:
df = pd.DataFrame(series_4_df, columns=['content'])
df['content'] = df['content'].astype(str)
df.head()
```
||content|
|----|----|
|0|```<tr><th class="default" data-sort-order="defau...```|
|1|```<tr class="topic-list-item category-share-guid...```|
|2|```<tr class="topic-list-item category-share-guid...```|
|3|```<tr class="topic-list-item category-share-guid...```|
|4|```<tr class="topic-list-item category-share-guid...```|

## We've arrived at step 2
We have created a dataframe filled with a lot of HTML code. Let's inspect the content of one cell:
```python
df.loc[2,'content'] 
```
```html
<tr class="topic-list-item category-share-guided-project tag-257 tag-sql-fundamentals tag-257-8 has-excerpt 
unseen-topic ember-view" data-topic-id="558357" id="ember71">\n<td class="main-link clearfix" colspan="">\n
<div class="topic-details">\n<div class="topic-title">\n<span class="link-top-line">\n<a class="title raw-link
raw-topic-link" data-topic-id="558357" href="https://community.dataquest.io/t/analyzing-cia-factbook-with-sql-full-project/558357"
level="2" role="heading"><span dir="ltr">Analyzing CIA Factbook with SQL - Full Project</span></a>\n<span 
class="topic-post-badges">\xa0<a class="badge badge-notification new-topic" 
href="https://community.dataquest.io/t/analyzing-cia-factbook-with-sql-full-project/558357" 
title="new topic"></a></span>\n</span>\n</div>\n<div class="discourse-tags"><a class="discourse-tag bullet"
data-tag-name="257" href="https://community.dataquest.io/tag/257">257</a> <a class="discourse-tag bullet" 
data-tag-name="sql-fundamentals" href="https://community.dataquest.io/tag/sql-fundamentals">sql-fundamentals</a>
 <a class="discourse-tag bullet" data-tag-name="257-8" href="https://community.dataquest.io/tag/257-8">257-8</a>
 </div>\n<div class="actions-and-meta-data">\n</div>\n</div></td>\n<td class="posters">\n<a class="latest single"
data-user-card="noah.gampe" href="https://community.dataquest.io/u/noah.gampe"><img alt="" 
aria-label="noah.gampe - Original Poster, Most Recent Poster" class="avatar latest single" height="25" 
src="./Latest Share_Guided Project topics - Dataquest Community_files/12175_2.png" 
title="noah.gampe - Original Poster, Most Recent Poster" width="25"/></a>\n</td>\n<td class="num posts-map posts" 
title="This topic has 0 replies">\n<button class="btn-link posts-map badge-posts">\n<span 
aria-label="This topic has 0 replies" class="number">0</span>\n</button>\n</td>\n<td class="num 
likes">\n</td>\n<td class="num views"><span class="number" title="this topic has been viewed 9 times">9</span>
 </td>\n<td class="num age activity" title="First post: Nov 20, 2021 9:25 am\nPosted: Nov 20, 2021 9:27 am">\n
 <a class="post-activity" href="https://community.dataquest.io/t/analyzing-cia-factbook-with-sql-full-project/558357/1">
  <span class="relative-date" data-format="tiny" data-time="1637360860367">1d</span></a>\n</td>\n</tr>
```
### Extracting the data from HTML:

How to find order in this madness? We only need 2 elements from the above code (but we'll try to extract more).
The title in the above block of code is "Analyzing CIA Factbook with SQL - Full Project", we can find the title inside the span element:
```html
<span dir="ltr">Analyzing CIA Factbook with SQL - Full Project</span>
 ```
The previous element is the link we're after:
```html
<a class="title raw-link
raw-topic-link" data-topic-id="558357" href="https://community.dataquest.io/t/analyzing-cia-factbook-with-sql-full-project/558357"
level="2" role="heading">
 ```
Number of views should be a usefull:
```html
><span class="number" title="this topic has been viewed 9 times">9</span>
```
 
The last bit of information we're after is the number of replies for each post:
```html
<span aria-label="This topic has 0 replies" class="number">0</span>
```
We could use BeautifulSoup to target those specific elements and extract their content, but this dataset is not that big and extracting the information
we need directly from the cell in the same row seems like a bit safer option. We'll follow the below plan:
* Remove the first row (which is not a post element)
* Proceed with regex techniques to extract the title, link, number of replies and number of views (forgot regex tricks? [here's a cheatsheet](https://www.dataquest.io/blog/regex-cheatsheet/))
* Remove the rows with 0 replies

```python
# remove 1st row:
df = df.iloc[1:,:]

# extract title, link and number of replies:
df['title'] = df['content'].str.extract('<span dir="ltr">(.*?)</span>')
df['link'] = df['content'].str.extract('href=(.*?)level="2"')
df['replies'] = df['content'].str.extract("This topic has (.*?) re").astype(int)
df['views'] = df['content'].str.extract("this topic has been viewed (.*?) times")
df['views'] = df['views'].str.replace(',','').astype(int)

# remove 1 generic post and posts with 0 replies:
df = df[df['replies']>0]
df = df[df['replies']<100]
df.head()
```

| |	content |title |link	|replies|views|
| -----|	------------------------------------------------- |--------------------------------------------------------------------- |-----	|-----|-----|
|4	|<tr class="topic-list-item category-share-guid...	|Predicting house prices	|https://community.dataquest.io/t/predicting-ho...	|1|26|
|5|	<tr class="topic-list-item category-share-guid...	|[Re-upload]Project Feedback - Popular Data Sci...	|https://community.dataquest.io/t/re-upload-pro...	|3|47|
|7|	<tr class="topic-list-item category-share-guid...	|GP: Clean and Analyze Employee Exit Surveys ++	|https://community.dataquest.io/t/gp-clean-and-...	|2|53|
|10|<tr class="topic-list-item category-share-guid...	|Project Feedback - Popular Data Science Questions	|https://community.dataquest.io/t/project-feedb...	|5|71|
|12|	<tr class="topic-list-item category-share-guid...	|Guided Project: Answer to Albums vs. Singles w...	|https://community.dataquest.io/t/guided-projec...|5|370|

        

## Step 3: scraping the individual posts
This last step is not going to be much different than step 1 of scraping, we have to inspect one individual post and deduct which element of the page is responsible for the content of the first reply to the post. We're assuming that the most valuable content is going to be stored in the first reply to the published project. We'll ignore all the other replies.
        
To process this amount of text data we'll create a function. All the heavy data processing is being done inside the function and we don't have to worry about some variables occupying the memory after we're done working with them.   
        
```python
# create a function for scraping the actual posts website:
def get_reply(one_link):
    response = requests.get(one_link)
    content = response.content
    parser = BeautifulSoup(content, 'html.parser')
    tag_numbers = parser.find_all("div", class_="post")
    # we're only going to scrape the content of the first reply (that's usually the feedback)
    feedback = tag_numbers[1].text
    return feedback
```
### Testing the scraper
Here's a very important rule I follow whenever performing web-scraping:
START SMALL!

You don't want to scrape a few thousand websites just to learn that your last line of code didn't work and you have to redo everything and wait again. That is why we'll start with a very small dataset, check if everything is clicking, then move on to deeper waters.

```python
# create a test dataframe to test scraping on 5 rows:
df_test = df[:5].copy()

# we'll use a loop on all the elements of pd.Series (faster than using 'apply')
feedback_list = []
for el in df_test['link2']:
    feedback_list.append(get_reply(el))
df_test['feedback'] = feedback_list
df_test
 ```
<!-- |index|feedback|
|---|---|
|4|     \nprocessing data inside a function saves memo...|
|5|     \nHi,\nI’ve been going through your project an...|
|7|     \n\n\nnoticed that you’re deleting objects, af...|
|10|            \nthink you forgot to attach your file…\n|
|12|    \n@gdelaserre: recategorized your topic. The E...| -->

Looks promising, let's check the whole cell:
```python
df_test['feedback'][4]
```
'\nprocessing data inside a function saves memory (the variables you create stay inside the function and are not stored in memory, when you’re done with the function) it’s important when you’re working with larger datasets - if you’re interested with experimenting:\nhttps://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page\nTry cleaning 1 month of this dataset on kaggle notebook (and look at your RAM usage) outside the function and inside the function, compare the RAM usage in both examples\n'

Whole reply, ready for cleaning. 

### Scraping all of the feedback

Now let's move on to a bigger boat (this will take a while):
```python
# this lets scrape all the posts, not just 5 of them:
def scrape_replies(df):
    feedback_list = []
    for el in df['link']:
        feedback_list.append(get_reply(el))
    df['feedback'] = feedback_list
    return df
    
df = scrape_replies(df)
```

That's it, we've extracted all the raw data we wanted from Dataquest's websites. In the next post, we'll focus on cleaning and analyzing this data using natural language processing techniques. We'll try to find the most common patterns in the content of projects feedback. But before you go, here are a few things to think about:

## Things to consider:
**Scraping tool**

BeautifulSoup is a great library to start with, but you've probably noticed that we came across its limitations, to perform web scraping on complex dynamic websites we should use a more advanced tool (We'll try to cover Selenium library in the future)

**Consider the server**

If you're constantly requesting a LOT of content from a website, most of the servers will pick up on it and very often cut you off. Remember to start small. In our specific example, we asked for a chunk of data and received it without any problems.  But it's common to run into some problems, most common one: 
```python
ConnectionError: HTTPSConnectionPool(host='en.wikipedia.orghttps', port=443): Max retries exceeded with url:[...]
```
The important part is: **Max retries exceeded**. It means we've been requesting data too many times. It's a good habit to stop web scraping every now and then to mimic natural human behaviour, how do we do that? We need to smuggle this 1 line of code: 
```python
time.sleep(np.random.randint(1,20)) 
``` 
This will pause our algorithm for a random number (1-20) of seconds, naturally, that extends the amount of time it takes to extract the data, but makes it possible on the other hand. Remember that we need to put this one-liner in an adequate spot in our code:

```python
# this lets scrape all the posts, not just 5 of them:
def scrape_replies(df):
    feedback_list = []
    for el in df['link']:
        # go to sleep first, then do your work:
        time.sleep(np.random.randint(1,20)) 
        feedback_list.append(get_reply(el))
    df['feedback'] = feedback_list
    return df
    
df = scrape_replies(df)
```
If you're interested in other tricks in web scraping, [read this article](https://www.danielherediamejias.com/6-basic-tips-to-perform-web-scraping-with-python/).

**Internet connection**

Assuming that the server will let us extract all of that data, can your service provider handle it? The size of our dataframes is fairly small, but imagine performing this task on much bigger datasets. Hotspotting wifi from an iphone may not be an ideal solution. Maybe that data has already been extracted and the dataset is available online? I encourage you to post the dataset after you've scraped it, some people may not have such a good connection as you do. Alternatively, you could use an environment with a better connection. While working on this project I've used Kaggle. I didn't have to worry about my slow connection, it was fast enough to connect to and work on Kaggle. All the web scraping was done through their servers.

**Memory usage**

Ok, so your connection can handle it, but can your laptop handle it? Our dataframe is small, but always be prepared! If the size of the dataframe is close to your RAM size, then you have to start considering doing it in stages. Check your disk space, make sure that you need all that data.

**Is it legal?**

There are several of articles relating to this topic. You should read at least one or two and be aware of what you're doing. It is very important, especially when web scraping is being conducted for business activities. 

## Any questions?

Feel free to reach out and ask me anything:
[Dataquest](https://community.dataquest.io/u/adam.kubalica/summary), [LinkedIn](https://www.linkedin.com/in/kubalica/), [GitHub](https://github.com/grumpyclimber/portfolio)
