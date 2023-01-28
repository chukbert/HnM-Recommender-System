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
<img src="https://www.kaggleusercontent.com/kf/104384600/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..KHrZgHXMegv1TRRavtX7ZQ.COLJHOTd8pWIOY9oEnEX-tW6BShzf0g8WH_CGxYehupVedEXut7-Zuh-8cSWKF-B7yIwQ2EEB_sgBaApXslXloAIPrhS50gY2bsTFtQolpIqe64xzE35J7V_6O1IwpH00akPYBKiLFvGFZlb4BOYiFnQxaEP8FMUgWEE6KhGW171tUyLb0RySJUsQ_XSjCcYwSBaq5d9UiP6PUm-bKHBfMJL1tSm96PzFSopdMDno90pxbZqTBrN7jk3ScoK6axMQC9AO3QoCZc_GrT26IXMHu2mcGYEGL59FPuMR_LZsM6kwfl6AnKK0uo7kj1iFvy6aljthEv979Qq64dmt9UgBRZ2vWnOe5l8fxkQkNn8CKBpEbBbrmh07UyvakX3kzuuVXP_V_8bU6qbk_7MzuiLXdx6_hV0uvo3Q3tJyACFUq6lmV1Roj4IEl2fr_JTnPIWWO7Mpc2EHE9N0KTSFHMmoOQiuSZ56orxYPK1-bT4gJGFtQpRCIy25mVr96jDjyfTZyhglFGpIcpJFAvFwOf6hvHtUubLFshBwDbfJiHtxiHStWO3znHE7SViijWsVP_sGABdfKLNn0gckLpjoABP20VvwTMJyVpcgj8Wakznbp_TjAn0Z5cuDEXClZn0zuYiuA26Y12T9SvUuwMEEoxWdA5gFAo44-UlOKRZY4p2ycA.T-f_AMpTynOLWk7PLxuc8A/__results___files/__results___10_0.png"  width="60%" height="30%">
