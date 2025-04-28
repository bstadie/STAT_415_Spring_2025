# Homework 3: Recommender Systems 2, Collaborative Filtering and Linear Models
Continuing on Homework 2, this repository provides the materials and guidelines for Homework 3, where you will continue to work with the Evanston, IL, restaurant reviews dataset. In this homework, we will keep going with our exploration of recommender systems, turning our focus to collaborative filtering and predictive modeling techniques. In particular, we will work with Linear Modeling. 

## Dataset
For this assignment, we will continue using the same ``'RestaurantReviews.xlsx'`` data as introduced in Homework 2.

## Analysis Instructions
Your analysis should be presented in a clear, visually appealing PDF document, with appropriate visualizations that are properly labeled and annotated to aid interpretation. You may use any Python libraries or tools that you find helpful, but your document should not include any code. Focus on presenting your findings in a clear, concise, and understandable way.

Please note that the questions provided in the homework assignment are meant to guide your analysis. Many of these questions are intended to be open-ended.

In addition to the PDF document, please also submit a code file that includes all the code you used in your analysis.

The questions for this second part of the recommender systems homework are divided into two categories: Collaborative Filtering and Predictive Modeling.

### Collaborative Filtering

1. Use the demographic data in ``'Reviews.csv'`` to create a unique user feature vector for each reviewer, including numeric representations of all demographic attributes in the data, including but not limited to ``'Has Children?'``, ``'Weight (lb)'``, ``'Preferred Mode of Transport'``, etc. Apply one-hot encoding for categorical variables. Ensure each vector is unique to an individual reviewer, by avoiding double counting. Many reviewers have submitted reviews for multiple restaurants, so you do not want to count these people twice when making these vectors. Report the total number of unique user vectors created and the dimensionality of each vector.

Another way of asking this question: Create a user feature matrix where row $i$ is a unique user and column $j$ is that user's feature vector. 

2. Using the vectors created in the previous question, write a function that computes the distance from one user to all others. With this function, build a recommendation algorithm that takes a user and outputs a recommendation made by the most similar user (i.e. the most similar users favorite restaurant). Demonstrate this algorithm by selecting ``'Timothy Mace'`` as your user, and in your report, include his most similar user and the recommendations provided. Based on this example, explain how this algorithm works. Does this algorithm always suggest more than one recommendation for every user in the dataset? If not, propose a possible solution.
   
3. Rather than finding users that are similar in terms of demographics, we want to find users that gave similar reviews. To find users that have given similar reviews, for each user $j$ you will want to form a 63-dimensional vector where entry $i$ is the user $j$'s review score (rating) of restaurant $i$. This vector will have many blank entries. What should you use to fill in these blanks? *Hint: probably not 0.*


Note, another way of forming question 3 is this: Make a matrix where $a_{ij}$ is user $j$'s review of restaurant $i$. Fill in the blank entries of this matrix. 

4. Similar to step 2, write a function that computes the distance from one user to all others based on the vectors created in step 3. Demonstrate this algorithm by selecting ``'Sarah Belle'`` as your user, and in your report, include Sarah's most similar user and the recommendations provided. 
   
### Predictive Modeling

5. Develop a linear regression model that integrates demographic data and the cuisine type of restaurants to accurately predict a restaurant's rating for a given restaurant.

6. Repeat question 5. However, this time do a logistic regression rather than a linear regression. To do a logistic regression, bin the reviews into `postive` and `negative` bins. Then predict the bin of the review. 

7. Compare the performance of linear and logistic regression by creating a train/test split on your model? What is the error of your models? How should you compare them? Select a review from the test set and use your model to predict the restaurant score based on his user demographics and the restaurant's cuisine type. Compare the model's prediction with the actual score to assess its accuracy.

8. Pick your favorite model from step 7, either logistic regression of linear regression. Add an L1 penalty (Lasso regularization) into your regression model to observe its impact on the model's performance and feature selection. Compare the test-set results with the standard regression model developed in step 5 or 6. What features are selected by this L1 model? In other words, when are the weights of the linear model large? When are they small or negative? Are certain demographics more predictive of review score?

9. We want to know what demographic features are useful for predicting coffee scores. There are 3 coffee shops in the dataset. For these three restaurants only, write a linear model that takes demographic data and predicts the score.
    
10. Examine the weights produced by the linear model developed in in step 9. Identify the demographic features that are most influential. In other words, when are the weights of the linear model large? When are they small or negative? Based on these weights, can we infer if certain demographic groups have a preference for or against coffee?

### Text Embedding

11. Consider the column ``'Review Text'``. Embed the review texts into vectors using Sentence Transformers. Use these embeddings as features to train a logistic regression model to predict the review sentiment: positive or negative. Note, this repo contains reference code for embedding with sentence transformers. Compare the MSE of this model to the MSEs of the models in steps 5 and 7. 



### Final
12. Find at least 1 interesting thing in the dataset and write about it. For example, find a single user that hates every restaurant they review, or a trend among Northwestern students. When I did this exercise, I found 18 interesting trends in the data with minimial effort. So there should be plenty of things to find.
