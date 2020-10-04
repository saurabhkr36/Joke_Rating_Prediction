# Joke_Rating_Prediction
Ranked 50th with RMSE score of 4.424 on Joke rating prediction hackathon in Analytics vidhya.
Link to Competition -> https://datahack.analyticsvidhya.com/contest/jester-practice-problem/#LeaderBoard

## Introduction
Many online businesses rely on customer reviews and ratings. Explicit feedback is especially important in the entertainment and ecommerce industry where all customer engagements are impacted by these ratings. Netflix relies on such rating data to power its recommendation engine to provide best movie and TV series recommendations that are personalized and most relevant to the user.
The dataset contains anonymous ratings(-10 to 10) provided by a total of 41,000 users. Train file contains 1.1 million ratings and in the test file the user needs to predict the ratings provided by the same set of users on a diffrent set of jokes. The complete text for all 139 jokes is also provided in a separate csv. Given the combination of user and joke, the task is to predict the rating given by that user to the joke in the test set.
The evaluation metric for this challenge is root mean squared error (RMSE).
## Objective
Predict the ratings for jokes given by the users provided the ratings provided by the same users for another set of jokes. 
## Step-wise Approach
### Text Preprocessing
I've created a function to convert a raw sentence to a string of meaningful words. 
#### Removing HTML tags
Often, unstructured text contains a lot of noise, especially if you use techniques like web or screen scraping. HTML tags are typically one of these components which don’t add much value towards understanding and analysing text so they should be removed. I've used BeautifulSoup library for HTML tag clean-up.
#### Removing special characters
Special characters, as you know, are non-alphanumeric characters. These characters are most often found in comments, references, currency numbers etc. These characters add no value to text-understanding and induce noise into algorithms. In order to remove these, regular-expressions (regex) can be used and I've used it in this dataset of jokes to get rid of these characters and numbers.
#### Removing stopwords
Stopwords are often added to sentences to make them grammatically correct, for example, words such as a, is, an, the, and etc. These stopwords carry minimal to no importance and are available plenty on open texts, articles, comments etc. These should be removed so machine learning algorithms can better focus on words which define the meaning/idea of the text. I've used set of words from nltk.corpus in the dataset.
#### Visualization and Vectorization
I've used WordCloud library to vizualize the wordcloud of jokes dataset. Wordcloud is a novelty visual representation of text data, typically used to depict keyword metadata (tags) on websites, or to visualize free form text. Tags are usually single words, and the importance of each tag is shown with font size or color. 
I've used CountVectorizer to vectorize the words extracted from jokes dataset for further use.
### Model Training
I've used LightGBM model to train the words corpus.
#### LightGBM
Light GBM is a gradient boosting framework that uses tree based learning algorithm. It can handle the large size of data and takes lower memory to run along with focus on accuracy of results.
#### Parameters in LightGBM
I've used the following parameters in LightGBM:
         'num_leaves': 45
         'min_data_in_leaf': 30
         'objective':'regression'
         'max_depth': -1
         'learning_rate': 0.075
         "boosting": "gbdt"
         "feature_fraction": 0.9
         "bagging_freq": 1
         "bagging_fraction": 0.9
         "bagging_seed": 11
         "metric": 'rmse'
         "lambda_l1": 0.1
         "verbosity": -1
         "nthread": 4
         "random_state": 4950
### Model Validation
The Predicted results of ratings are compared to the existing actual results in the competition site and its RMSE calculated as 4.42
## End Notes
The text preprocessing part is an important part and needed logical interpretation and visual inspection of jokes dataset.
The Jokes rating are predicted using LightGBM model with given parameters tuned and found to be optimal as RMSE of 4.42.


