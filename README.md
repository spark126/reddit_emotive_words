# Using Classification Modeling and Reddit to Find Emotive Words

## Problem Statement

As complex platforms provide online communities for many individuals and societies manipulation and propaganda has become an ever increasing problem. This project aims to begin the process of better understanding the meaning of words and their effectiveness in conveying emotion. We focus on emotion as the current consensus on human decision making is that emotions is more persuasive than logic. This does not mean that logic is worthless or unnecessary but that it is more effective to use emotional persuasion which is supported by logic. [source 1](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4050437/) [source 2](https://customerthink.com/neuroscience-confirms-we-buy-on-emotion-justify-with-logic-yet-we-sell-to-mr-rational-ignore-mr-intuitive/)

In order to begin understanding emotions in words our first step is to create a list of words that convey emotion. To attempt to do this we will use classification models and natural language processing to find words that help separate bodies of text from two very distinct subreddits, [/r/AskPhysics](https://www.reddit.com/r/AskPhysics/) and [/r/Poetry](https://www.reddit.com/r/Poetry/). Most submissions on the /r/AskPhysics subreddit are purely related to understanding concepts in physics and therefore are, for the most part, devoid of emotions. Poetry on the other hand often requires the use of a few words to convey complex feelings. Additionally, /r/Poetry includes tagging on submissions that allow us to only select submissions that have been tagged poems.

Using Classification Modeling we will try to create a high scoring model, accuracy, that we can then pull feature names (words) and feature importance. Then using feature importance we will select words that most influence the classification model and check if these words convey emotion. Then for lack of a better method, we will see if the results are intuitive.

## Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**selftext**|*object*|reddit|Body of the submission, text, which will be vectorized into many columns.| 
|**subreddit**|*object*|reddit|Name of subreddit where submission was posted.| 

## Analysis

As we wanted to create a list of emotive words through the use of the models feature importance, it was decided to only use the vectorized text as the features. This would allow the words to be the main focus of the model. Overall three separate models were used, the Decision Tree Classifier, the Random Forest Classifier, and the Voting Classifier, which included the Ada Boost Classifier, the Gradient Boosting Classifier, and the Random Forest Classifier. Each model or ensemble was then independently gridsearched for the best score, prioritizing the reduction of indicators of the model being overfit, cross val score vs training score. Additionally, the Decision Tree Classifier and Random Forest Classifier were fit to both a stemmed text dataset and a lemmatized text dataset.

After hyper-parameter optimization the highest scoring model with minimal overfit was select, which was the ensemble Voting Classifier. Then the feature names and feature importance were pulled from each of the classification models within the ensemble and then graphed separately.

## Conclusion & Recommendations

The Voting Classifier ensemble model best predicted the subreddit of the submission based on the words within the body of the submission, scoring ~0.06 better on mean accuracy than the closest model, random forest classifier. The model did not overfit, as the test score was greater than the cross validation score.

Overall the score was much better than the ~0.50 mean accuracy of the baseline and implies that there is a clear separation between the wording in submissions in /r/poetry and /r/AskPhysics, as expected. However, even with a well scoring model compiling a list of meaningful words is still difficult. Using feature importance we are still very limited in the amount of words that we can select as more features do not mean a better model. Additionally, the model performed better on unigrams and therefore means getting a phrase of words is difficult.

If we were to continue with classification models. Next steps could include expanding our base dataset to include many more subreddits such as /r/history, /r/mathematics, /r/askscience, and other science subreddits which contain largely text submissions. Another step would be to build the classification models while rotating features and selecting the high scoring models to pull features from, however, it may be best to search for other modeling solutions due to the contradictory need to reduce model features and the desire to create a large and robust library of emotive words.
