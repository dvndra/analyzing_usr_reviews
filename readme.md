## The attached jupyter notebook shows how *rating, sentiment and length of user reviews* affect deveoper response to user reviews
[![Supported Python version](https://img.shields.io/pypi/pyversions/Lucid.svg)]()

Developer response behaviour comprises of two important aspects:
- whether developer provides a response to a review, and if applicable
- how much time developer takes to respond (aka response time)
The code template can be used to do similar analysis on custom dataset structured as one .csv file for every app in a folder.

### Pre-requisites:
To run this code, please make sure you have the following:
- the original dataset folder named Top100Android, or your custom dataset from any app store.
- SentiStrength files (provided in SentiStrength Folder). Refer to SentiStrength Java Manual for more options that can be included while running sentiment analysis.

### Overview of code:
**1. Data Ingestion:** <br>
  - Read data of all android apps (Data Structure: list of pandas DataFrame where each dataframe contains all reviews from a single android app) and filter apps containing at least one developer response (i.e. % devResponse >0.00) and append data of all such apps into single dataframe with columns ["appName", "date","rating","reviewText", "dev-reply-time", "dev-reply-text"]

**2. Feature Extraction:** <br>
  - Though rating and sentiment is discrete, however reviewLength is continuous and hence we have binned the variable into 5 classes based on percentiles (20,40,60,80,100).
⋅⋅⋅ To classify sentiment of reviews, SentiStrength java code run as a process (which either takes single review or txt file containing one review in each line). Thus, the reviewText column is exported as a txt file which then passes on to SentiStrength to classify all reviews (process approx 8-10 lakhs reviews/ minute). The output file is then read into pandas for further processing. (Note: delete the output file named reviews0_out.txt before running the sentiment classfication again)

- parameters supplied to SentiStrength process:
    explain: include explanation column illustrating how a given reviews gets a particular sentiment class. 
    paragraphCombineAv: takes average of positive and negative sentiment of each sentence to determine overall sentiment. Other options are to take max or total, however there are problems with both as max doesn't capture variability and total reaches to saturation of value 5/-5 quickly.
    trinary: output sentiment as [-1,0,+1] (more details in SentiStrength Java Manual as how to calculate it)
    capitalsBoostTermSentiment: gives boost to the sentiment of a term whose all letters are capital (like WRONG, AWESOME)
    Refer to SentiStrength Java Manual for more options that can be included while running sentiment analysis.

Note: please refer to paper <a href = "https://www.researchgate.net/publication/266657943_Sentiment_analysis_of_commit_comments_in_GitHub_An_empirical_study"> sentiment_analysis of commit comments.pdf</a> to know more about sentiment classification process.

-

- **Step 3 - Analysis & Results:**

- Various exploratory graphs are then plotted at both app level and play store level and conclusions are added about what inferences can be drawn from those graphs.

If you have further questions, feel free to contact dswami@usc.edu
