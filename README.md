# Disertation Project
## Machine Learning Techniques Applied in Tourism
### Airbnb Vienna

#### Short description and data sources
The project's aim is to extract relevant insights about Airbnb Vienna as to help potential landlords increase their competitive advantage.  

The data used within this project was web-scraped by [Inside Airbnb](http://insideairbnb.com/get-the-data.html) on 17 March 2020. Due to the large size of the folder (aprox. 1GB), the data I have used, along with additional spreadsheets) can be found and dowloaded using [this link](https://drive.google.com/drive/folders/1wZ5kNz-eCJ24Qcs_QpyFSr98THjJRjvG?usp=sharing). 

The thesis' aim was to extract relevant insights about Airbnb Vienna as to help potential landlords increase their competitive advantage. The property prices were predicted using XGBRegressor and a slight enhancement of the results was achieved by hyperparameter optimization. This choice of modelling gave insights on the most important features regarding the price of the properties listed.
Furthermore, Airbnb Vienna reviews were assigned a sentiment polarity score, using VADER (NLTK package), as to see which are the most frequently used words in reviews having a negative score, compared to those with a general positive sentiment, through word clouds.


This project has three main topics, based on three different datasets.

1. The *listings_17_03_2020.csv* dataset, contains the characteristics of all listings that were live at the scraping date. Each row belongs to a listing (13,224 liostings), and the columns provide information about the characteristics of each listing (106 features);

The *1.1.Vienna_Listings_17_03_2020_PreModelling* notebook contains data cleaning/processing, EDA (Explanatory Data Analysis) and feature engineering steps. The resulting dataset, before dummy transformations, contains 52 features and 11996 listings. The dataset resulted after the dummy transformations was exported as *transformed_listings.csv*.
The *1.2.Vienna_Listings_17_03_2020_XGBRegressor_HPM* takes as input the *transformed_listings.csv* dataset. This notebook contains the multicollinearity assessment, the standardization and normalization of features and the application fo the models.

The Multivariate Regression ( and the Ridge regularisation) was used as a weak baseline comparion prediction for XGBoost, as the dataset used isn't compatible with the multivariate regression hypotesis ( there are multiple highly correlated features, many features overall etc.). 

The property prices were predicted using XGBRegressor and a slight enhancement of the results (mainly reducing the overfitting of the model) was achieved by hyperparameter optimization. The parasmeters chosen were: max_depth, min_child_weight, eta, subsample, colsample.
This choice of modelling gave insights on the most important features that have an impact on the price of the properties listed.

2. The *reviews_17_03_2020.csv* contains all the user reviews for every listing that was live at the scraping date, in total, 470.279 reviews.

The *2.1.NLTK_positive_negative_scores* notebook contains the following steps:
 - data imports and preprocessing (removing unwanted columns);
 - some light data cleaning (unescaping html tags) as VADER takes into account punctuation and emojis when calculating polarity scores;
 - the application fo the VADER model and appending the Positive, Negative, Neutral, Compound metrics to the datatset. As the dataset contains reviews in multiple languages, the metrics are reliable only for the english reviews. Removing non-ebnglish reviews will be done in another notebook.
 
 The *2.2.1.Data processing for word clouds* notebook is used for removing automated postings from the dataset. 
 The *2.2.2.Subset english reviews*  does exactly just that. Taking into account that the data will be used for word-clouds, there was no need for a 100% accurate method. The way of action chosen was to: tokenize and lower-case the reviews, removing the punctuation signs, POS-tag and lemmatize the words(step wich only works with english) and using the *nltk.corpus.words.words()* corpus to count the (majority) of the words in english, and a simple counter to count all the words per review. 
 
 Reviews with more than 70% words in english were kept, almost 66% of the initial dataset, meaning 309.110 reviews. 
 In the *2.3.Word_clouds* notebook, the english reviews were split into positive, negative and neutral reviews, based on the compound metric. The resulting wordclouds are: 
 
![Positive Reviews Wordcloud](https://github.com/anazavoiu/disertation/blob/master/WordCloud300-positive.png)
 






3. The  *calendar_17_03_2020.csv* contains the Airbnb calendar of each ad for the period March 17, 2020 - March 17, 2021 (13,224 properties with daily prices, 4,826,810 records); this calendar contains the periods in which a property is or is not booked, the minimum and maximum number of nights and the price displayed for that period. This notebook was processed for data vizualization purposes.
