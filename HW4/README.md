# Homework 4: Predictive Modeling

In this homework, you will develop various predictive models using housing price data and evaluate their performance through different statistical analyses and visualization techniques.

## Dataset Description

You will be working with two datasets containing housing price data from [realtor.com](https://www.realtor.com/) for foreclosure properties:

1. **IL_housing_price.csv**: This dataset includes housing data for properties sold in Illinois between 2017-01-01 and 2024-04-01. Foreclosure in this context refers to the process in which a homeowner's right to a property is terminated, usually due to default. It often involves the property being sold at a public auction where the proceeds are used to pay off the mortgage debt.

2. **WI_housing_price.csv**: This dataset contains data for 50 foreclosure properties sold in Wisconsin during the same period.

Each dataset includes the following columns:
| Column Name     | Description                                 |
|-----------------|---------------------------------------------|
| `property_url`  | URL of the property listing on realtor.com  |
| `style`         | Style of the house (e.g., condo, single house, mobile home) |
| `beds`          | Number of bedrooms                          |
| `full_baths`    | Number of full bathrooms                    |
| `half_baths`    | Number of half bathrooms                    |
| `sqft`          | Total square footage of the house           |
| `year_built`    | Year when the house was built               |
| `sold_price`    | Sale price of the house in USD (target variable)              |
| `lot_sqft`      | Square footage of the lot                   |
| `latitude`      | Latitude coordinate of the property         |
| `longitude`     | Longitude coordinate of the property        |
| `county`        | County where the property is located        |
| `stories`       | Number of stories in the house              |
| `parking_garage`| Number of parking garages                   |


Additionally, an **illinois-counties.geojson** file is provided, which contains geographical boundaries data for each county in Illinois. This file will be used in the later parts of the homework for creating Choropleth maps.

## Analysis Instructions

### Linear Models
Starting with `IL_housing_price.csv`, the target variable is the sale price. Be sure to set aside a validation set.

1. Train a linear model using appropriate columns from the dataset to predict housing prices. Create a histogram of the housing prices in the dataset. Compare this histogram with the predictions made by your linear model, e.g. by showing histograms of model predictions and historgrams of the true data. 
   
2. Make a histogram of the linear model errors. How are they distributed?
   
3. Tune your linear model with L1 and L2 regularization. Does this improve the MSE at all? It might not.

### Decision Tree

4. Train a Decision Tree model using the same dataset. Use this model to predict housing prices. Report the MSE or RMSE.
   
5. Visualize the decision tree to see how decisions are being made. Tools like `graphviz` can be used to create a visual representation of the tree.

### Random Forest
6. Train a random forest model on the same dataset. Report the MSE or RMSE.
   
7. Make a histogram of the forest outputs versus the true data distribution. How do they compare? You can also consider making overlapping density plots instead of histograms, if you prefer.
   
8. Tune your random forest. Can you improve it? Are any parameters important?

### Neural Networks
9. Implement a 3-layer neural network with sigmoid activations using PyTorch to predict housing prices. Consult [this PyTorch tutorial](https://github.com/yunjey/pytorch-tutorial/blob/master/tutorials/01-basics/feedforward_neural_network/main.py) for guidance. Report the MSE.
   
10. Look at the distribution of outputs of your neural network. Compare it to the true distribution. Neural networks are well known to converge to the mean output. Is this happening to you? If it does happen, try to retrain your net from scratch. Is it a consistent problem? Does it depend on the seed?
   
11. Tune your net by adjusting the optimizer, the number of layers in the net, and the activation functions you use. If you want, you can also try adding dropout and regularization, although this might not help much. Are you able to make any improvements?

### Visualization
12. Create a Choropleth map of Illinois counties, colored by the average sale price of foreclosure properties. An example code snippet can be found in `make-il-map.py`. 
    
13. Develop a second Choropleth map showing predictive errors by county using one of your models. Discuss which counties were easier or more difficult to predict accurately.


## Final Section 
Please select one of the two final sections for the HW. You do not need to do both. Please only complete one of the sections. Section A is on transfer learning. Section B is on TabPFN. Only complete one section. 


## Section A: 


### Transfer Learning
We now turn our attention to `WI_housing_price.csv`. 

14. Train models using `WI_housing_price.csv` and compare performance with those trained on the Illinois dataset.
   
15. Try your best to achieve some transfer learning. Take a linear model and train it on the data from `IL_housing_price.csv`. Then, take that trained linear model and try to make predictions on the data from `WI_housing_price.csv`. Does your trained linear model transfer?
 
16. Let's try to achieve some transfer via training. First, train a neural network on `IL_housing_price.csv`. Then, once this first training is done, fine-tune the network by training on the data from `WI_housing_price.csv`. Note, you might want to only train on `WI_housing_price.csv` for a few iterations, since it is small and you risk overfitting if you train for a long time. How do your results compare to the results from 12? Does transfer help at all?

## Section B: 

### TabPFN: 

TabPFN is a model that uses transformers to do tabular predictions. This section will let you practice using TabPFN. 

14. Train a tabPFN model on the data to predict housing prices. You might need to subset the data and train on individual subsets, since tabPFN has a data limit. [here is the repo](https://github.com/PriorLabs/TabPFN) How does the tabPFN model compare to the random forest and linear model? How does the run time compare? The error rate?

15. Discretize your outcome variable into bins and run tabPFN again. How does the error rate compare in the continuous vs discrete prediction case?

16. Find some data points where TabPFN and other models disagree on the final prediction. Which model is more accurate? Do you have a hypothesis why that model is doing better? 

