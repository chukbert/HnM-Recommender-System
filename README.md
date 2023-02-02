# HnM Fashion Recommender System
## Description

This project is related to the [kaggle competition](https://www.kaggle.com/competitions/h-and-m-personalized-fashion-recommendations). The goal is to develop product recommendations based on data from previous transactions as well as from customer and product meta data. The available meta data spans from simple data, such as garment type and customer age, to text data from product descriptions and image data from garment images.

**The final task** is to recommend up to 12 products for customers to purchase during the 7-day period immediately after the training data ends. Performance is evaluated according to the Mean Average Precision @ 12 **([MAP@12](https://www.kaggle.com/code/debarshichanda/understanding-mean-average-precision))**.

## Dataset

The dataset can be downloaded [here](https://www.kaggle.com/competitions/h-and-m-personalized-fashion-recommendations/data).

  >  ```articles.csv``` : detailed metadata for each ```article_id``` available for purchase  
  ```customers.csv``` :  metadata for each ```customer_id``` in dataset  
  ```transactions_train.csv``` : the training data, consisting purchase log of customers  
  ```images folder``` : a folder of images corresponding to each ```article_id```  
  
  However, ```articles.csv``` contains detailed metadata, such as shape, material, and color information for each article. This project assumes that the information gathered from ```article.csv``` is enough, so images from the ```images folder``` will not be used to train the model.

## Notebook
- This project performed in the two notebooks.
> - 1st notebook: [````EDA(Exploratory Data Analysis)````](https://github.com)
>   - This Exploratory Data Analysis Notebook will look the data, analyze the content, check for missing data, understand the data distribution, see what are the relations between data in various files, and do some various visualizations and statistical analysis.
> - 2nd notebook: [````Candidate generation and Model````](https://github.com)
>   - This notebook prepares the data, reducing the amount of data train needed from **```4.5GB + 512MB + 117MB```** to **```788MB + 17MB + 11MB```**. Achieve **6x memory reduction!**.
>   - Generates candidates as negative examples for training the model and for evaluation. For each customer, candidate products generated are 12 best seller last week, the most recent product purchased by the customer, and the best seller product for the week in which the customer purchased.
>   - Feed data training and candidates to LGBMRanker and use the ranker to output predictions. Get **0.2045 score** and 1798/2952 place ~ **40% better** than other competitors. 

## Result
| | |
|:-------------------------:|:-------------------------:|
|<img src="https://res.cloudinary.com/dxf1c5iwj/image/upload/v1675324658/hnm/age_dist_grouped_w7weab.png"  width="100%" height="100%">|<img src="https://res.cloudinary.com/dxf1c5iwj/image/upload/v1675325222/hnm/club_member_ig13yw.png"  width="100%" height="80%">|
|<img src="https://res.cloudinary.com/dxf1c5iwj/image/upload/v1675325223/hnm/pop_item_wshcqk.png"  width="100%" height="80%">|<img src="https://res.cloudinary.com/dxf1c5iwj/image/upload/v1675325223/hnm/pop_prod_name_mvd3bg.png"  width="100%" height="90%">|
|<img src="https://res.cloudinary.com/dxf1c5iwj/image/upload/v1675325223/hnm/pop_type_f8gvzv.png"  width="100%" height="100%">|<img src="https://res.cloudinary.com/dxf1c5iwj/image/upload/v1675325223/hnm/pop_section_ds5y8h.png"  width="100%" height="100%">|
|<img src="https://res.cloudinary.com/dxf1c5iwj/image/upload/v1675325223/hnm/prod_group_ijbm4t.png"  width="100%" height="100%">|


