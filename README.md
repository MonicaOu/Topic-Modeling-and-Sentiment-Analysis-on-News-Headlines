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

## Tasks (Topic Modeling, WordCloud and 2 types of Sentiment Analysis) 

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
  
- Step 3: Apply TF-IDF on bag of words
  - We could directly run LDA on bag of words and use word counts as weights. However, for words that show up frequently across many headlines, they aren't quite as strong as words that are unique to only a few headlines in terms of classifying topics. Hence, we would want to apply TF-IDF (gensim.models.TfidfModel) and put less weights on words that frequenly show up in headlines
 
- Step 4: Run LDA 
- Classify all headlines into 10 topics and extract words and associated probabilities that define the topics
- A potential topic looks like this 
  - Topic: 1 Word: 0.021*"man" + 0.018*"polic" + 0.015*"charg" + 0.013*"murder" + 0.012*"woman" + 0.011*"crash" + 0.010*"court" + 0.009*"alleg" + 0.009*"death" + 0.009*"car"
  - This topic might be related to accident and murder 

### Detect Common words in News Headlines using WordCloud 
- I am curious what are some common words in ABC news headlines, hence I generate a wordcloud with the preprocessed data from topic modeling and the result is as follows
![image](https://user-images.githubusercontent.com/76879882/119908544-764fe580-bf18-11eb-93a6-2eadefc729e1.png)
- Common buzz words include "Plan", "New", "Australia", "Say", "Report" and "Claim" etc


### Sentiment Analysis using NLTK VADER Package
- Sentiment labels: Postive, Negative and Neutral

- Lemmatisation and Removing stopwords are not necessary here because it might harm the analysis performance
  - According to this [article](https://medium.com/data-science-blogs/stopwords-and-lexicon-normalization-for-sentiment-analysis-f9f10f0d4108#:~:text=VADER%20tends%20to%20outperform%20TextBlob,for%20pattern%20based%20sentiment%20analysis.), removing StopWords and Lemmatization actually made identifying negative reviews more difficult. Intuitively, it makes perfect sense. StopWords such as “not”, “very”, and “but” can be quite helpful when it comes to identifying negative emotions. Words with the same base roots such as “worse” and “bad” or “better” and “good” exhibit different emotional intensities but will be ignored after Lemmatization

  - Also, according to [Schumacher](https://opendatagroup.github.io/data%20science/2019/03/21/preprocessing-text.html#:~:text=The%20general%20rule%20for%20whether,improve%20performance%2C%20do%20not%20lemmatize.&text=For%20example%2C%20a%20popular%20sentiment,not%20be%20stemmed%20or%20lemmatized), "VADER, has different ratings depending on the form of the word and therefore the input should not be stemmed or lemmatized."

- Classification threshold
  -Based on "About the Scoring" section on this [github page](https://github.com/cjhutto/vaderSentiment), if compound score is larger than 0.05, the headline will be classified as positive; if compound score is smaller than -0.05 it will be negative and in between will be neutral

- Result 
  - Nearly half of the news headlines are neutral. While in the other half, there are more negative headlines identified than positive ones 
  - Changes in sentiment over time: There are two peaks (in 2012 and 2015) and two troughs (in 2010 and 2020). There might be some major events happening during that time and drive sentiment scores up and down. For example in 2020, sentiment score went down potentially because of COVID.
   - ![image](https://user-images.githubusercontent.com/76879882/119909226-017dab00-bf1a-11eb-9ea2-631c59e630b6.png)
 
 
### Sentiment Analysis using [NRCLex Package](https://pypi.org/project/NRCLex/) (more granular) 
- Sentiment labels: Fear, Anger, Sadness, Disgust, Negative, Positive, Surprise, Joy, Trust and Anticipation

- Lemmatisation and removing stopwords are not necessary as mentioned above 

- Result 
  - ABC news headlines consists mostly of "negative emotion", where more than 60% of headlines express a sense of fear and negativity. This makes sense because headlines might be reserved for large-scale disasterous events. However, almost one-thrid of them have a more postive tone, and show a sense of postivity and trust
  - ![image](https://user-images.githubusercontent.com/76879882/119910848-ae0d5c00-bf1d-11eb-84b2-8842993befb1.png)

  
