## The attached jupyter notebook shows how *rating, sentiment and length of user reviews* affect deveoper response to user reviews
[![Supported Python version](http://dswami.freevar.com/git_icons/pyversions.svg)]()

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
  - Read data of all android apps (Data Structure: list of pandas DataFrame where each dataframe contains all reviews from a single android app)
  - Filter apps containing at least one developer response (i.e. % devResponse >0.00) and append data of all such apps into single dataframe with columns ["appName", "date","rating","reviewText", "dev-reply-time", "dev-reply-text"]

**2. Feature Extraction:** <br>
  - Length of reviews: transformed into categorical variable by binning into 5 classes based on percentiles (20,40,60,80,100).
  - **Sentiment Analysis:** To classify sentiment of reviews, `SentiStrength` java code is used which takes input as either single review or txt file containing one review in each line. Thus, the reviewText column is exported as a txt file which then passes on to SentiStrength to classify all reviews (process approx 8-10 lakhs reviews/ minute). The output file is then read into pandas for further processing. (Note: delete the output file named reviews0_out.txt before running the sentiment classfication again). Please find below brief explanation for parameters supplied to SentiStrength process:
    - ***explain:*** include explanation column illustrating how a given reviews gets a particular sentiment class. 
    - ***paragraphCombineAv:*** takes average of positive and negative sentiment of each sentence to determine overall sentiment. Other options are to take max or total, however there are problems with both as max doesn't capture variability and total reaches to saturation of value 5/-5 quickly.
    - ***trinary:*** output sentiment as [-1,0,+1] (more details in SentiStrength Java Manual as how to calculate it)
    - ***capitalsBoostTermSentiment:*** gives boost to the sentiment of a term whose all letters are capital (like WRONG, AWESOME)
  - Refer to SentiStrength Java Manual for more options that can be included while running sentiment analysis. Please refer to paper <a href = "https://www.researchgate.net/publication/266657943_Sentiment_analysis_of_commit_comments_in_GitHub_An_empirical_study"> sentiment_analysis of commit comments.pdf</a> to know more about sentiment classification process.

**3. Analysis & Results:** <br>

- Various exploratory graphs are then plotted at both app level and play store level and conclusions are added about what inferences can be drawn from those graphs. <br>
<a href="http://dswami.freevar.com/git_icons/usr_results_1.png"><img src="http://dswami.freevar.com/git_icons/usr_results_1.png" style="width:82px; height:86px" alt=" "></a>



If you have further questions, feel free to contact dswami@usc.edu
