# stock_prediction_g24_p3
     This  project tries to predict stock prices from news articles 
     and viral based tweets

## data preprocessing
    we pre_process data in data_preprocess folder using stock price charts of
    amazon and apple recorded at different intervals of time. The various news 
    articles about apple and amazon are used as well. News data is not present 
    in this project repository as it enourmous and cannot be pushed to github.
    the data_preprcoess folder contains charts_pre_processing.ipynb,
    news_processing.ipynb and combine_news_and_cahrts.ipynb. The following are
    the descriptions about each file:
    
**data_preprocess/news_processing.ipynb** - we process news by sanitizing the news articles 
    content and converting them into pure english vocabulary word tokens by
    getting rid of numeric, alphanumeric and words with special characters or
    non-english characters. We also consider published_time timestamp(in utcTimezone) 
    to properly associate with stock trends.We do this for both apple and amazon. we store 
    the newly processed data in data_preprocess/pkls/news/ folder. We get a pandas data frame 
    with the following headers:
    **['published_time','time_frame','article_content','word_tokens']**.

**data_preprocess/charts_pre_processing.ipynb** - we process stock charts to fit our training.
    The charts in OHLC format with various time intervals and we can find the trend of stock for 
    a given row by finding the  difference between the closing and opening cost, if difference 
    is positive it means stock goes up  and if difference is negative it means stock goes down. 
    We do this for both amazon and apple separately for each interval and will be stored in pkl files
    in the  folder  data_preprocess/pkls/charts/. We get a pandas data frame with the following headers:
    **['published_time','time_frame','trend']**.

**data_preprocess/combine_news_and_charts.ipynb** - we combine news article with stock chart data with this file.
    All articles will be associated with immediate stock data trend for each interval of time data. we do this for 
    amazon and apple. we store this data in  data_preprocess/pkls/full_data this is the final data used for feature 
    extraction. We get a pandas data frame with the following headers:
    **['published_time','time_frame','article_content','word_tokens','trend']**.

## Feature Extraction
    Features extraction is handled in folder feature_extraction/. It contains all feature 
    extraction algrithms used and sub-folder to store relevant feature-extraction data. It
    contains features n-gram, glove and tf-idf.

## Models
    Machine-Learning models are handled in models/ folder. It contains all models logistic, svm,
    naive-bayes and xgboost fo each feature in their own sseperate folders. In each sub folder there are
    pkl files for each feature to save that particulaar models progress to use it again.

## configure.json
    Fill the fields with appropriate folder paths to run the project in your machine.

# How to use this project for prediction
    1) run all the files in data_preprocess first.
    2) for each feature_extraction run the designated .ipynb files in feature_extraction/ folder to
        get the features.
    3) for each model run the designated .ipynb files in the subfolder named after the model in model/
        folder to save the model state for both the apple and amazon for all time intervals seperately
        in pkl files in their designated pkls subfolder.
    4) use the pkl files in models/{model name}/pkls/{feature name}/ to predict the stock trand for given
        text.


