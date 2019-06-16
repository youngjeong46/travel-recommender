# Vacation Destination Recommender!


## Overview

This project took TripAdvisor's Hotel reviews in 9 different trave locations and applied NLP (Natural Language Processing) to create a recommender for travelers on where to travel and which hotel to stay in.

**Blog post on the topic can be found [here](https://datatostories.com/posts/2019/06/09/travel-recommender/). The Flask app is live and can be accessed [here](http://travel-recommender-app.herokuapp.com/).**

## Project Design


Scraping close to 130000 hotel reviews on Tripadvisor scattered around 8 different destinations, I took a closer look at 86000 positives reviews and performed Natural Language Processing on them. General NLP workflow took the following steps:

1. Preprocessing the documents:
Clean the documents: Remove punctuations, special characters, and either stem or lemmatize certain words (I chose to lemmatize).
Tokenize the documents: Using NLTK's tokenizer, I tokenized the documents, removing stopwords.
2. Vectorizing the tokens: Of the two more common ways to vectorize the tokens, I decided on using TF-IDF (Term Frequency-Inverse document frequency) instead of a simpler CountVectorizer, as it accounts for the importance of a word in a document in a collection or corpus.
3. Topic Modeling: Using the TF-IDF matrix, I applied some of the topic modeling algorithms (NMF, LSA, and LDA).
4. Create a recommender system: Using the model, I calculated cosine similarity to find a document that was most similar to build a recommender system.

To test how the model behaved (since in unsupervised learning we are not clear with model performance metric), I used several stages:
1. Collect another collection of document - in my case, I used Scott's Drink document collection, and run the model to see if topic spaces were obvious. Doing so and running topic modeling with 2 spaces, it was apparent that one topic space had words that related to alcohol and drink mixture, and other with traveling
and weather.
2. Run the recommender system with documents from my training set to see if the recommender returned
itself as the topic choice. This worked correctly for all three models as well.
3. Slightly change some words from Step 2 or remove a sentence and see if the recommender system
remained working. It made the right recommendation most of the times, although make a few word changes started returning different reviews as recommendations. I was confident that the model behaved well up to this point.
4. Input custom documents (i.e. User's ideal vacation description) to see if the recommender returns what was expected. The model did not perform very well here. For example:

"I want to go ski on the mountain" returned Whistler as the top recommendation, which is to be expected. However, "I want to go ski" returned Boracay as the top recommendation, which is to be NOT expected. Looking closely, we can see two things in action: 1. Word Frequency on Whistler shows "ski" barely mentioned. This is alarming but expected at the same time because hotel reviews should mostly talk about the state of the hotel, not of the city or the ski resorts. 2. Ski could mean "jet ski", which is a summer and beach-related activity.

Doing these case studies showed me that the model has some holes that need to be improved.

## Tools

- Web Scraping: Scrapy
- Data Storage: MongoDB, pandas
- Natural Language Processing: SpaCy, gensim, nltk, scikit-learn
- Web Application: Javascript, Flask
- Presentation: Google Slides

## Project Organization

The structure of the project organization is adapted from Cliff Clive's [DataScienceMVP](https://github.com/cliffclive/datasciencemvp), which itself is adapted from the famous Data Science project structure from Cookiecutters that you can access [here](https://github.com/drivendata/cookiecutter-data-science/).

```
    ├── LICENSE
    ├── README.md          <- The top-level README for developers using this project.
    ├── main.py            <- The top-level src code for this project.
    ├── data
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── results            <- Trained and serialized models, model predictions, or model summaries
    │   ├── models         <- Generated model records stored in pickle files
    │
    ├── notebooks          <- Jupyter notebook. Naming convention is a number (for ordering),
    │   └── MVP.ipynb      <- General overview of the projectin Jupyter notebook.
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   ├── proposal.docs  <- Proposal of the project
    │   └── slides.pptx    <- Slide deck for a short presentation.
    │   
    ├── environment.yml    <- Conda environment file

```

## Data

The data was obtained by scraping the following websites:

1. TripAdvisor.com: Using Scrapy
2. Reddit.com: Via API

The data were accumulated and then combined to create a single dataset of over 86000 reviews.
