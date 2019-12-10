# Project 3 - NLP Classification with Reddit Posts

## Problem Statement
- Using Reddit API to collect posts from two subreddits (r/Rockets and r/NBA).
- Use NLP to train a classifier on where each reddit post come from. 
## Gathering the Subreddit Posts
- Dataframes were taking from r/Rockets and r/NBA on reddit.
- Using pushshift multiple items were requesting from each subreddit.
- 20 requests were made with a maximum of 500 posts from each request. A delay of 1 day was put between each request. 
- Requests were made to get a substantial amount of posts while gathering posts from the same timeframe. 
  -911 posts were taken from r/Rockets. 8,207 posts were taken from r/NBA
  -7,885 posts were taken from r/Rockets. 10,000 posts were taken from r/nba
  -After cleaning 16,549 comments were left and were used in modeling.
  -91,000 words were used in these comments.
- Comments were chosen for anylization due to the balanced ratio. Titles were avioided because of the similarity of the title posts and most posts were of pictures/videos. 
## Cleaning the Data and EDA
- A function was used to clean the data: Changing the text to lowercase. Removing HTMLS and emojis. Removing non-letters. Removing hyperlinks. Removing words with 2 or fewer letters. Removing whitespaces.  
- The text was lemmatized to shorten words
- Count Vectorizer was used to find the 35 most common words from each post. A union was set between these 35 most used words and then the union was appended to the english stopwords. 
## Modeling
- A baseline score between the two subreddit comments were 59% r/NBA and 42% r/Rockets.
- A target variable was set to be r/Rockets
- The data was split using test train split with the test size of 0.33%
- 3 models were used: Logistic Regression. Random Forest. Multinomial Naive Bayes. 
- Each of the models were ran with CountVectorizer and TFIDVectorizer. Each with the new stopwrods which were created. 
- Gridsearch was used on each of the models to find the best parameters that were used. 

| Data/Model|Train Score|Test Score|
|---|---|---|
|LogisticRegression With Cvec| .95% | .70% |
|LogisticRegression with TFID| .81% | .70% |
|Random Forest with Cvec| .98% | .68% |
|Random Forest with TFID| .95% | .68% |
|MNB with Cvec| .84% | .70% |
|MNB with TFID| .84% | .70% |

## Conclusions/Recomendations. 
- Each of the models were overfit to the testing data. Reasoning: 
   -This was may have been the large amount of words that were being anaylized.
   -These two subreddits are similar in nature both speaking about basketball. 
   -These two subreddits have alot of overlap with each cases of authors posting on each subreddit.

- Which model works best?
  -Random Forest with Cvec scored the highest accuracy on the training data.
    -This could caused by the unbalanced data in the baseline score. The random forest model has a tendancy to choose the         majority in the classification process.  
    -This model was the most overfit out of the 3 models used.
  -The LogisticRegression model with Cvec would be the recommended model 
    -This model was the least overfit out of the 3 models. 
    -The accuracy score on the Train and Test score were above the baseline score. 
    -This model would do the best on new data. 
    
- Recomedations:
  - More work on feature engineering to find features that will improve accuracy.
  - Adding more words to the stop words to create larger differences between the subreddits. 
  - Using more types of models.
  - Gridsearching to find better parameters.   
