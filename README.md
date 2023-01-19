# HnM Recommender Sstem
## [Kaggle competition](https://www.kaggle.com/competitions/h-and-m-personalized-fashion-recommendations)

- This project is related to the kaggle competition, and the goal is to recommend products to customers using the data from H&M, a fast fashion brand.
- The given data is: 
  > ```articles.csv```: Information on fashion items (article means each product)  
  ```customers.csv```: Information on customers    
  ```transactions_train.csv```: Purchase log of customers  
  ```images folder```: Photos for each article  
  
  However, ```articles.csv``` contains detailed metadata, such as shape, material, and color information for each article. This project assumes that the information gathered from ```article.csv``` is enough, so data from the ```images folder``` will not be used to train the model.
- ```transactions_train.csv``` has purchase information for about 2 years from September 20, 2018 to September 22, 2020. The final task is to recommend up to 12 products for customers to purchase during the week since September 22, 2020, the last log date of the data. ```transactions_train.csv``` 12 articles must be recommended to all customers presented in the data, and performance evaluation is conducted with **MAP@12**.([MAP: Mean Average Precision](https://www.kaggle.com/code/debarshichanda/understanding-mean-average-precision) to put it simply, MAP is an application metric of precision, and it is a performance evaluation index that reflects product recommendation accuracy and priority when recommending.)

## Notebook
- This project plans to proceed with technology across a total of three notebooks.
> - 1st notebook: [````EDA(Exploratory Data Analysis)````](https://github.com/milkyme/HnM-Personalized-Fashion-Recommendations/blob/master/1.EDA.ipynb)
>   - Examine missing values ​​and outliers for given data, and proceed with EDA to analyze data from various directions through various visualizations and statistical analysis.
> - 2nd notebook: [````Candidate Generate```](https://github.com/milkyme/HnM-Personalized-Fashion-Recommendations/blob/master/2.Candidates%20Generate.ipynb)
>   - Using the given data, we proceed with the task of creating a candidate group consisting of hundreds of articles for each customer.
>   - Recommendation of candidates using Graph Neural Network is quite long [```2-1.Graph embedding```](https://github.com/milkyme/HnM-Personalized-Fashion-Recommendations/ blob/master/2_1.Graph%20Embedding.ipynb) is described in a separate notebook.
> - 3rd notebook: [````Ranking Model````](https://github.com/milkyme/HnM-Personalized-Fashion-Recommendations/blob/master/3.Ranking%20Model.ipynb)
>   - The final recommendation is made for each customer by calculating the ranking for the article candidate group created in the second notebook.

## Result
- 1. EDA focused on understanding and familiarizing with the contents of the features while examining the data. The explanations are detailed so that there is no difficulty in looking at ```2.Candidate Generate``` or ```3.Ranking Model``, which contain explanations of models related to recommendations, even if you do not necessarily look at the notebook.
- 2. Candidate Generate
		- Description: This is the process of selecting products to recommend to customers in various ways.
 		1) 'Best item' that selects products that have been sold a lot recently and products that have been sold a lot by age group
 		2) 'Same product code item' to select a product with the same product code as the recently purchased product
 		3) 'Contents based filtering' that recommends products similar to recently purchased products using product metadata
 		4) 'Graph Embedding (User-based collaborative filtering)', which makes recommendations by reflecting the purchases of other products by customers who have purchased the same product based on their purchase history
		A total of four methods were used to select candidates for each customer, and as a result of verification through validation data, the average recall for each customer was about 0.0945.
		- Performance: An average recall of 0.0945 means that when a customer purchases a product, there is an average probability of about 9.45% that the product is included in the candidate list. Of course, how much this is is relative, so to add an explanation, the MAP@12 for the test data of the model submitted by the final winner of the Kaggle competition was about 0.037.
			- Things to consider about performance are: 1) MAP@12 is a figure calculated by recommending only 12 articles, and there are hundreds of article candidates in candidate. And 2) MAP is Mean Average Precision, and since the basic calculation method is precision, direct comparison with the recall I used for verification is impossible.
		- However, there is ample room for 1) 12 and hundreds of gaps to overcome as the ranking model will proceed with one more sophisticated recommendation. 2) Precision and recall are obviously different, but when the metric is applied, the elements included in the numerator are the same even though the elements included in the denominator are different. Therefore, the average recall value used during verification also has a sufficient correlation with MAP, the metric to be used in the final evaluation.
		- ***In conclusion, it is difficult to compare directly how well candiate candidates are selected, but based on my indirect guess, meaningful results can be expected if the ranking model is well trained.***
- 3. Ranking Model
		- Description: This is the process of selecting and recommending 12 candidates that are most likely to be purchased for the candidates selected by each customer above. Since more than 1.3 million customers were given as training data, and there are hundreds of product candidates accordingly, it is necessary to learn quite large data. Metadata is also given as tabular data. Considering the above two points, we used the LightGBM model, which is efficient, fast, and can be used without worrying about preprocessing tabular data.
		- Performance: As mentioned before, MAP@12 for the test data of the model submitted by the final winner of the Kaggle competition was about 0.037. However, in my model applied to the validation data, MAP@12 is about 0.060. There will definitely be a difference between Test data and Validation data, so I cannot (of course) simply say that my model is 0.060/0.037 = 1.62 times better than the competition winner's model.
		- ***However, when configuring the valdation data, I was very careful not to cause data leakage, and I set the validation data to be as similar as the test data as much as possible (same 1-week period, only 1-week difference, etc.) , application to the test data will not result in very large performance degradation. Therefore, I think that the results of applying the ranking model following the candidate model showed significant performance compared to the winner solution of the competition.***
