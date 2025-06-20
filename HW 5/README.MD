# Homework 5: Explainability
In this homework, we will consider several methods for explaining the outputs of predictive models. We will focus on attribution methods, which try to weight the relitive importance of inputs with respect to making a prediction. It is important to note there are many methods for considering the interactions between variables. This assignment will not consider those methods, because they get complicated quickly. Instead, we will focus on attribution methods such as LIME, Shapley Values, and SmoothGrad. 




## Dataset

For this assignment, we will be working with two datasets.

**1. Pima Indians Diabetes Database:** This tabular database has several health diagnostic measures such as blood pressure, and the goal is to predict if a patient has diabetes. 

**2. Animal-10N Image Classification Dataset:** The ANIMAL-10N dataset consists of ten classes of animals, comprising 50,000 training images and 5,000 testing images. Your task is to develop a model capable of accurately classifying the animal depicted in a given image. 

## Analysis Instructions

### Tabular Data

Starting with the Pima Indians Diabetes Database. This dataset can be downloaded [here](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database)

1. Investigate the balance of the dataset with respect to the outcome variable. Is the outcome variable of the patient being diabetic undersampled? More specifically, what percentage of the total outcomes have the patient as diabetic? You always want to check this with medical data. 

2. Run a linear or logistic model on this dataset with an L1 penalty. What features does the model select on? 

3. Run a random forest on the dataset using SciKitLearn. After training, this classifier will have a field named `feature_importances_' that you can access. For example, if your trained random forest is called 'rfc' then you can call 'rfc.feature_importances_' to access feature importance. You can also call 'rfc.feature_names_in_' to get feature names. Doing this, what features does the random forest select on? 

4. Use LIME on this dataset to explain the importance of each feature. You may wish to reference this [starter code](https://www.kaggle.com/code/prashant111/explain-your-model-predictions-with-lime). Note -- LIME explains one datapoint at a time! So you will need to give LIME a particular datapoint and LIME will explain that datapoint only. You can report results for this question on only one datapoint. 

5. Is LIME stable across different datapoints? If you ask for explainability across two different datapoints, does LIME select on different features? 

6. Use SHAP (SHapley Additive exPlanations) to analyze feature importance on this dataset. Install the SHAP library (`pip install shap`) and use it to generate both global and local explanations:
   - Generate a summary plot showing the global feature importance across the entire dataset
   - For the same datapoint you used with LIME, generate a SHAP force plot to explain that individual prediction

7. How do LIME, SHAP, Forest importance, and linear model weighting compare? Do they select similar features? For this problem, you may consider LIME and SHAP feature selection on a single example datapoint.

### Predictive Modeling on Animal Images

We now turn our attention to the animal classification dataset. 

8. First, let's start by loading the data. Here's some [starter code](https://github.com/bstadie/STAT_415_Spring_2025/blob/main/HW%205/data_loader.py) for data loading is provided. You need to fill in the missing parts of the code to correctly load the data. Then, visualize an example image from each class in the training dataset.

9. Train a linear model on the animal clasification dataset. Note that you will need to use PyTorch to train this model, since there is no way you'll be able to do the matrix inversion required to run OLS. Here is some [starter code](https://github.com/yunjey/pytorch-tutorial/blob/master/tutorials/01-basics/linear_regression/main.py). A linear model corresponds to a single linear layer from the input to the output.

10. Train a vanilla deep convolutional network on the animal classifcaiton dataset. You should reference the starter code [here](https://github.com/bstadie/STAT_415_Spring_2025/blob/main/HW%205/nn_models.py#L50). 

11. Tune your neural network by adding batchnorm, more layers, better activations, improved learning rates, etc. Compare the accuracy of the linear model, the simple conv net, and the tuned conv net. Do this by making learning curves, which show the training epoch on the X-axis and the cross entropy loss on the Y-axis. Note that your overall graph will have 3 total curves: the linear model cross entropy loss vs epoch, the vanialla conv net cross entropy loss vs epoch, and the tuned convolutional model cross entropy loss vs epoch. Make a similar curve that shows the training epoch on the X-axis and the model test accuracy on the Y-axis for all three models. What hyper-parameters are important for learning?

12. Implement image augmentation. That is, flip all the images horizontally 180 degrees. Then train your CNN on a new dataset consisting of both augmented data and your original data. Does image augmentation improve performance? 


### Feature Atribution on Animal Images

13. Using the starter code [here](https://github.com/bstadie/STAT_415_Spring_2025/blob/main/HW%205/smooth_grad.py), run SmoothGrad on one your convolutional model from step 10. Produce a graphic similar to those in Lecture 10, which shows a heatmap of the gradient on the image demonstrating what pixels SmoothGrad is selecting on. See for example [here](https://www.semanticscholar.org/paper/SmoothGrad%3A-removing-noise-by-adding-noise-Smilkov-Thorat/f538dca4def5167a32fbc12107b69a05f0c9d832/figure/2).

14. Similarly, use LIME on images to generate an explanation of what features your convolutional net from step 10 is selecting on. See for example [here](https://raw.githubusercontent.com/marcotcr/lime/master/doc/images/images.png). Starter code is [here](https://github.com/bstadie/STAT_415_Spring_2025/blob/main/HW%205/LIME.py). Compare the features selected on by LIME and SmoothGrad. Are there any common features for certain animals? 

That's it! You're done with the HW for this class.
