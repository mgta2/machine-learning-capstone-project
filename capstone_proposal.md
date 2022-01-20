# Capstone Proposal

Data Science and Machine Learning Capstone Project Proposal.

## Domain Background

My project will concern the academic performance of secondary school pupils in Portugal. In particular, I will be looking at student attainment in Portuguese language. This attainment is measured in the form of three scores between 0 and 20 - G1, G2 and G3. The most important grade is G3, as this is the student's score in their final year at school.

## Problem Statement

The aim of my project will be to try to understand how various factors influence a student's academic performance. My goal will be to build a regression model which takes in information about a given student and tries to predict their final score, G3. Depending on the model's performance, I could then use it to understand which factors in a student's life have the greatest impact on their academic attainment. This information could be very helpful for teachers to understand which of their pupils are most likely to struggle at school, based on their respective environments and family backgrounds. These pupils could then be given more teacher attention and help.

## Datasets and Inputs

I will be using the dataset obtained from: https://archive.ics.uci.edu/ml/datasets/student+performance

This data was collected from two Portuguese secondary schools and was used in the academic paper: P. Cortez and A. Silva. Using Data Mining to Predict Secondary School Student Performance. In A. Brito and J. Teixeira Eds., Proceedings of 5th FUture BUsiness TEChnology Conference (FUBUTEC 2008) pp. 5-12, Porto, Portugal, April, 2008, EUROSIS, ISBN 978-9077381-39-7

The dataset is split in two: Mathematics and Portuguese language. I will only be using the Portuguese language data. There are a total of 649 instances with 33 attributes/features and no missing values. The dataset includes information such as the student's age, family size and alcohol consumption. It was collected from school reports and questionnaires.

The website housing the dataset has more than 1 million web hits, and the data has been used in a research paper written by academics at respected universities. Coming from these trustworthy sources, the data should be error free. That said, some of the data came from questionnaries, where students would have to judge their own alcohol consumption and time spent studying. This self-reported data is less reliable and can be rather arbitrary (such as rating the quality of one's family relationships from 1 to 5).

## Solution Statement

I intend to use the Gradient Descent algorithm to build a regression model for the Portuguese language data, with the target variable being the student's G3 score between 0 and 20. I will split my data up into training data and testing data, before building my model using the training data. A Cross Validation algorithm will build the model on different subsets of the training data. I can use this to see how much variance there is between different runs and whether or not my model is overfitting. I will then evaluate my model's performance on the testing data, and extract the model coefficients to see which features are considered to be of the most importance in estimating G3.

## Benchmark Model

The 'weekly study time' feature is measured from 1 to 4. As a benchmark model, I could take G3 to be this feature multiplied by 5. One would expect study time to be positvely correlated with academic success. This gives a very crude way to compare results with my regression model.

## Evaluation Metrics

The 'explained variance score' will give the fraction of the variance of G3 which cannot be explained by the given features. It will give insight as to how well the model can predict the student's final score using these statistics. A score of 1 would mean than the student's grade is completely determined by these environemntal factors, while a score of 0 would suggest that academic performance is totally independent of them.

The difference in MSE between the model's performance on the training data versus on the testing data will provide an insight into whether the model is overfitting. If the scores are close, then this suggests a low level of overfitting and that our model is reliable.

Lastly, I could consider the model's accuracy with respect to classifying the student into G3>9 or G3<10. It may be the case that the model finds it very difficult to predict the student's numerical score, but classification into pass/fail is reliable.

## Project Design

1. Look through the data and see if there is anything noteworthy.
2. Clean/preprocess the data. Several features will need to be encoded. It may be sensible to drop some features to prevent the dimension from getting too large. It will be necessary to split the data into train/test.
3. Build my model. Use Cross Validation to see how well it is working.
4. Evaluate the model's performance on testing data using the above evaluation metrics.
5. Analyse results.