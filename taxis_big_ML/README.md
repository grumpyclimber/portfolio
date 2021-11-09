This is an ongoing multiple notebooks project. Currently I am at the starting stage: 
* setting up a pipeline for importing and merging data, learning basic memory-saving tricks to fit under 16 Gb of RAM


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
