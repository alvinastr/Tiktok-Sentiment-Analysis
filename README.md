---

# Tiktok Review Sentiment Analysis

This project performs sentiment analysis on Tiktok reviews collected from the Google Play Store.

## Dataset

The dataset used in this project can be found on Kaggle: [Tiktok Google Play Store Review](https://www.kaggle.com/datasets/shivkumarganesh/tiktok-google-play-store-review).

## Installation

To run this project, you need to install the following libraries:

```bash
pip install pandas matplotlib wordcloud nltk plotly
```

## Usage

To use this project, follow these steps:

1. **Importing Libraries**

   The necessary libraries for data processing and visualization are imported:

    ```python
    import pandas as pd
    import matplotlib.pyplot as plt
    from wordcloud import WordCloud, STOPWORDS, ImageColorGenerator
    import nltk
    from nltk.sentiment.vader import SentimentIntensityAnalyzer
    from nltk.corpus import stopwords
    import string
    import re
    import plotly.express as px
    nltk.download('stopwords')
    ```

2. **Load the Dataset**

   Load the dataset into a pandas DataFrame:

    ```python
    data = pd.read_csv('/content/tiktok_google_play_reviews.csv')
    data.head()
    ```

3. **Data Cleaning**

   Clean the dataset by removing null values and unnecessary columns:

    ```python
    data = data[['content', 'score']]
    data = data.dropna()
    ```

4. **Text Preprocessing**

   Define a function to preprocess the text data:

    ```python
    stopword = set(stopwords.words('english'))

    def clean(text):
        text = str(text).lower()
        text = re.sub('\\[.*?\\]', '', text)
        text = re.sub('https?://\\S+|www\\.\\S+', '', text)
        text = re.sub('<.*?>+', '', text)
        text = re.sub('[%s]' % re.escape(string.punctuation), '', text)
        text = re.sub('\\n', '', text)
        text = re.sub('\\w*\\d\\w*', '', text)
        text = [word for word in text.split(' ') if word not in stopword]
        text = " ".join(text)
        text = [stemer.stem(word) for word in text.split(' ')]
        text = " ".join(text)
        return text
    ```



---
