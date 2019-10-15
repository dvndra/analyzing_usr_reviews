## The attached jupyter notebook shows how <emp> rating, sentiment and length of user reviews </emp> affect developer response and response time

To run this code, please make sure you have the following:
- the original dataset named Top100Android,
- SentiStrength files (provided in SentiStrength Folder). Refer to SentiStrength Java Manual for more options that can be included while running sentiment analysis.

### Overview of code:
- Read data of all android apps (Data Structure: list of pandas DataFrame where each dataframe contains all reviews from a single android app)

- Filter apps containing at least one developer response (i.e. % devResponse >0.00) and append data of all such apps into single dataframe with columns ["appName", "date","rating","reviewText", "dev-reply-time", "dev-reply-text"]

- To classify sentiment of reviews, SentiStrength java code run as a process (which either takes single review or txt file containing one review in each line). Thus, the reviewText column is exported as a txt file which then passes on to SentiStrength to classify all reviews (process approx 8-10 lakhs reviews/ minute). The output file is then read into pandas for further processing. (Note: delete the output file named reviews0_out.txt before running the sentiment classfication again)

- parameters supplied to SentiStrength process:
    explain: include explanation column illustrating how a given reviews gets a particular sentiment class. 
    paragraphCombineAv: takes average of positive and negative sentiment of each sentence to determine overall sentiment. Other options are to take max or total, however there are problems with both as max doesn't capture variability and total reaches to saturation of value 5/-5 quickly.
    trinary: output sentiment as [-1,0,+1] (more details in SentiStrength Java Manual as how to calculate it)
    capitalsBoostTermSentiment: gives boost to the sentiment of a term whose all letters are capital (like WRONG, AWESOME)
    Refer to SentiStrength Java Manual for more options that can be included while running sentiment analysis.
#### Note also refer to paper "sentiment_analysis of commit comments.pdf" to know more about sentiment classification process.

- Though rating and sentiment is discrete, however reviewLength is continuous and hence we have binned the variable into 5 classes based on percentiles (20,40,60,80,100).

- Various exploratory graphs are then plotted at both app level and play store level and conclusions are added about what inferences can be drawn from those graphs.

If you have further questions, feel free to contact dswami@usc.edu
