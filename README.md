<img src="http://imgur.com/1ZcRyrc.png" style="float: left; margin: 20px; height: 55px">

# Project 3: Web APIs & NLP
---

## Executive Summary
---

<b>Contents:</b>
1. Executive Summary
2. Problem Statement
3. Data Dictionary
4. Data Cleaning & EDA
5. Preprocessing and Modeling
6. Conclusion and Recommendations

## Problem Statement
---

Reddit is a massive collection of forums where people can share social news and content. Essentially, posts are organised according to subject into user-created ‘subreddits’. Members submit content (such as images, texts, and links) to subreddits, which can then be voted up (‘upvote’) or down (‘downvote’) by other members.<br>

We want to help you to identify:
1. Topics of interest/needs of these new dog and cat owners
2. Provide relevant suggestions on creating new services for dog and cat owners and;
3. Suggest a viable business model for pet lovers to venture into the pet industry

Our team aims to engineer selective supervised classification models namely:
1. Random Forest Classifier
2. Multinomial Naive Bayes
3. Logistics Regression Classifier

And select one model that best predicts the classification of the subreddit for current and future posts submitted by either dog or cat owners. Our team will select the best model based on the test score (which tells us its predictive power) of the models and look at the most important word features for that particular model to draw.

## Data Dictionary
---

For Pushshift.io API, the data dictionary is as follows:

|           Feature                          |    Datatype  |   Description                 |
|:------------------------------------------:|:------------:|:-----------------------------:|
|<p align='left'>subreddit                   |     object   |   post subreddit location     |
|<p align='left'>title                       |     object   |   post title                  |

## Data Collection
---

The dataset is scraped from r/cats and r/dogs subreddit. The reasons for selecting these two subreddits are:<br>
1. They are generic subreddits which encompasses all topics related to cats and dogs - not discriminating against any breeds. Hence, it would be interesting to know the prominent keywords in each subreddit, which will influence the business decisions for CatDog.
2. As of writing this README, there are 3,277,095 members in the r/cats subreddit and 2,303,326 members in the r/dogs subreddit. This forms a large enough database for our model to develop.

Utilising APIs, we scraped around 10,000 posts from each subreddit. There are many different components within each document in the entire corpus. Specifically, we would target the post titles because there was a significant amount of empty body text for posts within the r/cats subreddit.

## Data Cleaning and EDA
---

Upon analyzing the top 2000 posts, i will clean the data as follows:

1. remove html characters
2. remove http links / URLs
3. remove punctuations
4. consider only alphabets and numerics (as there are foreign languages and emojis)
5. replace newline with space
6. convert text to lower case
7. remove duplicates
8. remove stop words which i will do it later in the preprocessing

### Findings

I have created new columns for title length and title word count to check on the distribution. As expected, both are positively skew as members usually will write shorter words / characters for title and is easier to gain attention. <br>
By ploting boxplot, many outliers are found but i decide not to remove any as all are very important features to distinguish cats and dogs subreddit.

## Preprocessing and Modeling
---

Steps are taken for preprocessing:
1. Tokenizing
2. Removing Stopwords
3. Lemmatizing

### Model Evaluation

I use CountVectorizer for all models 


|           Model                                       | Train_Accuracy  | Test_Accuracy  |
|:-----------------------------------------------------:|:---------------:|:--------------:|
|<p align='left'>Baseline                               |     0.5039      |     0.5039     |
|<p align='left'>Random Forest                          |     0.9964      |     0.9118     |
|<p align='left'>Multinomial Naive Bayes                |     0.9526      |     0.9192     |
|<p align='left'>Logistic Regression                    |     0.9617      |     0.9197     |

Based on test accuracy score, Multinomial Naive Bayes and Logistic Regression outperformed Random Forest. Hence, i will further optimize the model with GridSearchCV to achieve better score.

|           Model                                       |  Train_Accuracy | Test_Accuracy  |
|:-----------------------------------------------------:|:---------------:|:--------------:|
|<p align='left'>Multinomial Naive Bayes                |     0.9526      |     0.9192     |
|<p align='left'>Multinomial Naive Bayes (GridSearchCV) |     0.9486      |     0.9194     |
|<p align='left'>Logistic Regression                    |     0.9617      |     0.9197     |
|<p align='left'>Logistic Regression (GridSearchCV)     |     0.9725      |     0.9199     |

The best model is Logistic Regression (GridSearchCV)

Further, Confusion Matrix is plotted and base on the high Accuracy score, I can conclude Logistic Regression is the best model to be used here.

## Conclusion and Recommendations
---

<b>Improvements to the Model</b>
<li> For modeling rigor, literal subreddit name references should have been removed as individual words (e.g. "dog", "cat") were left in earlier on.
<li> Additional stopwords 'ing' should be removed.
<li>Having posts with more unique words helps to distinguish between spam and ham but;
<li>Not all posts with unique words are relevant, so we have to focus more on the coefficient of frequently appearing words
<li> Perhaps this project could be improved by performing a form of sentiment analysis on the data in future studies. Lastly, though this model scored only around ~ 90% accuracy on testing data, this model still predicts much better than the baseline (~ 50%) and might be helpful in differentiating between dogs and cats.
<li> To consider using TifdVectorizer and compare the scores.
<li> Further analysis can be done on the emojis within the titles.

<br><b>Business recommendations</b>

<li>Explore other forums that are more local e.g. Hardwarezone as Reddit posts are more global and may not attune well to local context. Starting small within the local context would be a better way to 'test' the market first.
<li>r/dogs - more practical and ‘discussion’ driven (e.g. how to train your dogs not to bark too often).
<li>Create consultancy and onboarding services for new dog owners.
<li>If interested to bring in breeds, the top words can signify the popular ones among dog lovers and you may even mate two different breeds together to get a crossbreed.
<li>r/cats - sharing of digital media.
<li>Grooming services, venture into F&B (e.g. cat café) or even match making company.



---
### References

1. https://www.reddit.com/r/cats/
2. https://www.reddit.com/r/dogs/
