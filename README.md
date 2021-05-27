# Topic-Modeling-and-Sentiment-Analysis-on-News-Headlines

## Background 
This a public dataset found on [Kaggle](https://www.kaggle.com/therohk/million-headlines). It contains data of news headlines published over a period of eighteen years. 

Below is the data description: 
- publish_date: Date of publishing for the article in yyyyMMdd format
- headline_text: Text of the headline in Ascii , English , lowercase
- Start Date: 2003-02-19 ; End Date: 2020-12-31

Sourced from the reputable Australian news source [Australian Broadcasting Corporation](http://www.abc.net.au)

## Goal 
For this dataset, I aim to perform 
- topic modeling to see what are some natural topics these headlines fall into
- sentiment analysis to detect tone expression as well as changes in sentiment across time 

## Process 

### Topic Modeling using NLTK and Gensim(gensim.models.LdaMulticore)
- Step 1: Preprocess the data 
  - Tokenization: Split the headline text into words. Lowercase the words and remove punctuation
  - Remove stopwords as well as words that have less than 3 characters 
  - Lemmatize (nltk.stem.WordNetLemmatizer): words in third person are changed to first person and verbs in past and future tenses are changed into present
  - Stemming (nltk.stem.SnowballStemmer): words are reduced to their root form (plural to single)

- Step 2: Create bag of words 
  - Create a word dictionary and use indexes to represent unique words (gensim.corpora.Dictionary)
  - Filter down the word word dictionary to remove words that are either too frequent or too rare
  - Keep the top 100000 most frequent words only 
  
