# Homework 2: Recommender Systems Part 1
This repository contains materials and instructions for Homework 2, in which you will be working with a dataset of restaurant reviews from Evanston, IL. You will be tasked with taking this data and using it to build a recommendation engine.

The primary goal of the assignment is to gain insight into different systems of recommendation. In particular, we will focus on popularity matching, content-based filtering, and collaborative filtering methods. All three of these methods are important problems in the technology and data science communities. Broadly speaking, the outcome variable of interest in this dataset will be the user review score. We will at times use direct predictive modeling methods to predict the user review score from the data. However, much of our analysis will also focus on how to find similar restaurants and similar users across the dataset. Recommendations can then be made by finding restaurants that are similar to other restaurants the user enjoyed.

## Dataset
To access the dataset for this assignment, go to **Files > Homework** Data on the Canvas course page. There is one Excel file, ``'RestaurantReviews.xlsx'``, that contains two sheets. First, the ``'Restaurants'`` sheet contains information describing each of the restaurants in the dataset, such as average cost and type of cuisine. There is also a natural language description of each restaurant. The second sheet, ``'Reviews'``, contains user review scores for the restaurants. These reviews include review text, dates of the review, and demographic data of the reviewer. This demographic data includes birth year, marital status, and vegetarian preferences. The outcome variable of interest for this assignment is the rating, which is a score from 1 to 5 for the restaurant.

## Analysis Instructions
Your analysis should be presented in a clear, visually appealing PDF document, with appropriate visualizations that are properly labeled and annotated to aid interpretation. You may use any Python libraries or tools that you find helpful, but your document should not include any code. Focus on presenting your findings in a clear, concise, and understandable way.

Please note that the questions provided in the homework assignment are meant to guide your analysis. Many of these questions are intended to be open-ended.

In addition to the PDF document, please also submit a code file that includes all the code you used in your analysis.

The questions we would like you to consider for this homework can be broken into 4 categories: Exploratory Data Analysis, Popularity Matching, Content-based Filtering, and Natural Language Analysis.

### Exploratory Data Analysis
1. Import the dataset and identify any missing values. Highlight significant findings regarding missing data, such as specific entries or columns with missing values, and discuss the impact on your analysis. Propose strategies for handling these missing values, considering the context of recommendation systems.

2. Create histograms to explore the data distribution for key variables like ``'Has Children?'``, ``'Vegetarian?'``, ``'Weight (lb)'``, ``'Preferred Mode of Transport'``, ``'Average Amount Spent'``, and ``'Cuisine'`` in Restaurants.csv. Determine whether the dataset is balanced and select which histograms offer meaningful insights for inclusion in your final report; you don't need to include all of them.

3. Perform clustering on one-hot encoded user demographic data to identify distinct user groups. Use algorithms such as K-Means, DBSCAN, and Agglomerative Clustering, adjusting their parameters to discover meaningful clusters. For each identified cluster, calculate the average review score and look for trends. Present your findings in a clear format, preferably using tables.
   
### Popularity Matching
4. Identify the restaurant with the highest average review score, report its average score, and compare it to the general dataset's average score. Additionally, find the restaurant that has received the highest number of reviews and compare this number to the dataset's median number of reviews in your report. 

5. Create a simple recommendation engine that offers restaurant suggestions based on a specific cuisine type entered by a user, based on a popularity score. Apply this engine to generate recommendations for Spanish, Chinese, Mexican food, and Coffee, and include these specific recommendations in your report.

6. Implement a shrinkage estimator that adjusts review scores towards the mean score, scaled by the number of reviews a restaurant has received. Please use the exact shrinkage estimator from page 17 of Lecture 4. Identify the restaurant that benefits the most from this adjustment and the one that is most negatively affected. Illustrate the impact of shrinkage on review scores. For example, you can plot the top positive and negative changes in a bar chart, but feel free to create an alternative plot if you prefer, or present your results in a table instead.

### Content-based Filtering

7. Using the data in the ``"restaurants.csv"`` table, compute the Euclidean distance between every restaurant. Note that you will need to compute a numeric embedding of the categorical variables.

8. Repeat the previous step, using cosine distance this time. Then, for both the Euclidean distances and cosine similarities, report the results for the pairs (``'Peppercorns Kitchen', 'Epic Burger'``) and (``'Peppercorns Kitchen', 'Lao Sze Chuan'``). Discuss how these metrics reflect the relationships and similarities between the restaurants, considering their cuisine types and other features.

9. Write a script for a content-based filtering recommendation engine. This script should accept a user's name, identify the user's favorite restaurant, and then find the 10 most similar restaurants based on Euclidean distance. For the user ``'Willie Jacobsen'``, utilize the engine to identify his favorite restaurant and list the top 10 most similar restaurants. Display these recommendations through a plot, a table, or any other method that shows the system's output effectively.

10. Come up with a method of comparing the recommendations made by Euclidean distance and cosine distance. Explain why your method makes sense. What distance metric does the best under your proposed comparison method? Be sure to visualize your results or present a table as evidence.

### NOTE: 
For the following section, you only need to do one of version A or version B. You do not need to do both. If you do both, you will receive no extra credit. Please clearly mark which version you did in your assignment. There is no correct choice. Your choice will not impact your final grade. 

### Natural Language Analysis -- version A. 
11. Consider the ``'Brief Description'`` column of the Restaurants dataset. Augment this description by appending the restaurant's cuisine type to the end of the description. For example, with Tapas Barcelona, the description is: *'Festive, warm space known for Spanish small plates is adorned with colorful modern art & posters.'* The cuisine is *'Spanish.'* The augmented description would thus be: *'Festive, warm space known for Spanish small plates is adorned with colorful modern art & posters. Spanish.'* Name this variable ``'Augmented Description'``.

12. Compute the Jaccard matrix using the elements of ``'Augmented Description'``. In the Jaccard matrix, entry $d_{ij}$ should represent the Jaccard distance between restaurant $i$'s augmented description and restaurant $j$'s augmented description. In your report, please include the Jaccard distance between the following pairs of restaurants: 
(a) Burger King and Edzo’s Burger Shop
(b) Burger King and Oceanique
(c) Lao Sze Chuan and Kabul House

13. Note that Jaccard distance can make reccommendations by taking a restaurant the user likes and finding the restaurant that is closest to this liked restaurant, in terms of the jaccard distance. Using this method, please make reccommendations for the users ``'Calvin Smith'`` and ``'Solomon M'``


### Natural Language Analysis -- version B. 
11. Consider the ``'Brief Description'`` column of the Restaurants dataset. Augment this description by appending the restaurant's cuisine type to the end of the description. For example, with Tapas Barcelona, the description is: *'Festive, warm space known for Spanish small plates is adorned with colorful modern art & posters.'* The cuisine is *'Spanish.'* The augmented description would thus be: *'Festive, warm space known for Spanish small plates is adorned with colorful modern art & posters. Spanish.'* Name this variable ``'Augmented Description'``.

12. Develop a script that calculates the TF-IDF score for a specified input word across all ``'Augmented Descriptions'`` of the restaurants. Apply this script to determine which restaurant has the highest TF-IDF score for the term **'cozy'** and the term **'Chinese'**.

13. Make a list of the 100 most popular words in the ``'Augmented Description'`` column. Write two nested for loops. First, loop over each of the restaurant descriptions. For each restaurant description, also loop over every word in the 100 most popular words list. Compute the TF-IDF score for that word. The result should be 63 TF-IDF vectors of length 100, one for each restaurant. Next, compute the TF-IDF distance matrix. In this matrix, $d_{ij}$ is the distance between the TF-IDF vectors for restaurants $i$ and $j$. In your report, please include the TF-IDF distance between the following pairs of restaurants: 
(a) Burger King and Edzo’s Burger Shop
(b) Burger King and Oceanique
(c) Lao Sze Chuan and Kabul House

