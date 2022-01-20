# Capstone Report

Data Science and Machine Learning Capstone Project Report

## Abstract

The aim of my project was to understand the way in which various factors in a student's life could impact their academic performance. Solving this problem would be of interest to schools, as it would allow them to identify which students may need extra support. I attempted to solve this problem by building a linear regression model on data collected from student school reports and questionnaires. The model was not very good at predicting the student's numerical score, with an explained variance of only 0.17 on testing data and 0.31 on training data. However, it achieved an accuracy of 84% when trying to classify the students into pass/fail. Lastly, the regression coefficients did give insight into which factors are the most influential when it comes to predicting a student's academic success.

## Introduction

Understanding which factors influence a student's academic performance is important to the education industry. A model which takes in school report and questionnaire data to output a prediction of the student's success will allow academic institutions to identify which students are at risk of failing their course so they can provide additional assistance.

I built a linear regression model to solve this problem. It was trained on data obtained from two Portuguese secondary schools, with a target variable of the student's final score, G3 - an integer between 0 and 20, where 20 is a perfect score. The explained variance score was low, suggesting that the given data did not contain enough infomation to accurately predict a student's G3 score. But given the simpler task of evaluating which students passed and which failed, the model was far more successful. In this context, a pass mark was any G3 score greater than 9, and the regression model had an 84% accuracy of prediction.

Linear regression means finding a hyperplane in n-dimensional space which best estimates a given collection of data points. In other words, it is a generalisation of the 'line of best fit', $y = mx + c$. These coefficients (e.g. m and c before) detail how the model interprets the input data. Negative values mean that the feature negatively correlates with G3 score, while positive values imply positive correlation. Finding these values allows me to understand which features the model deems to be most important when predicting academic attainment.

## Related Work

The authors who produced the relevant dataset applied it in their paper (http://www3.dsi.uminho.pt/pcortez/student.pdf) to both classification and regression tasks. They used decision trees to classify the results into both pass/fail as well as five tiers (excellent, good, satisfactory, sufficient, fail). Notably, the authors used the R programming language with the RMiner package, while I used Python with the numpy, pandas and sklearn packages.

## Methodology

All the data manipulation and relevant code is contained in capstone_notebook.ipynb. The first step was to preprocess the data. I choose to drop several of the features. Some contained information that was unneccessary for my project. Others, such as 'reason', gave the student many ways to respond - 'home', 'reputation', 'course', 'other'. I would need to one-hot encode this feature, adding 4-1 = 3 more dimensions. I decided to drop them instead of blowing up my dimension. Then I encoded the remaining binary features (e.g. 'male' becomes 1 and 'female' becomes 0) so that the regression model could work with this data. Last, I split my data into test and train.

It was neccessary to transform the data using MinMaxScaler. Otherwise, the features are not weighted correctly. For example, the number of absences ranged from 0 to 93, which is on a different scale to binary 0s and 1s. This would mess up the distance metrics. I choose to transform with respect to only the training data. This way, no infomation about the testing data could get into the model.

Next, I trained my model and employed 5-fold Cross Validation to see how well it handled the training data. The model was then ready to be applied to the testing data. I looked at the Mean Squared Error, Explained Variance Score, and pass/fail classification accuracy, as well as the model's linear regression coefficients.

### Dataset

I used the dataset obtained from: https://archive.ics.uci.edu/ml/datasets/student+performance

This data was collected from two Portuguese secondary schools and was used in the academic paper: P. Cortez and A. Silva. Using Data Mining to Predict Secondary School Student Performance. In A. Brito and J. Teixeira Eds., Proceedings of 5th FUture BUsiness TEChnology Conference (FUBUTEC 2008) pp. 5-12, Porto, Portugal, April, 2008, EUROSIS, ISBN 978-9077381-39-7

The dataset is split in two: Mathematics and Portuguese language. I only used the Portuguese language data. There are a total of 649 instances with 33 attributes/features and no missing values. The dataset includes information such as the student's age, family size and alcohol consumption. It was collected from school reports and questionnaires.

### Baseline Model

I took a baseline model of 'weekly study time' multiplied by 5. The studytime feature is measured from 1 to 4, so this scales it up to 20. This seemed like a sensible yet unsophisticated model. One would expect study time to correlate with academic performance, and it is a way of measuring how well the model does against crude estimates.

### Algorithms

(1) SGD Regression:

I used the Stochastic Gradient Descent algorithm to build my model. This algorithm finds the hyperplane (linear model) which best fits the given data points, with respect to the Mean Squared Error (see below). It does this in a computationally efficient manner by estimating each sample and updating the hyperplane coefficients with a decreasing learning rate. This way, a sequence is built which converges to the optimal answer.

(2) MinMaxScaler:

This algorithm transforms the data features onto the same scale. The smallest value is sent to 0, while the largest value goes to 1. This way, all features are weighted equally with respect to the distance metric.

(3) 5-fold Cross Validation:

This algorithm splits the given data into 5 parts. Five models are trained on a different 4/5 of the data each time. Each model is then tested on the remaining 1/5 of the data. Then the score associated to each model is printed.

### Metrics

(1) Mean Squared Error (MSE):

This metric is used in the linear regression algorithm as a way of measuring the distance between data points and the model's prediction. The aim of the SGD algorithm is to minimise this value.

(2) Explained Variance Score:

The 'explained variance score' will give the fraction of the variance of G3 which cannot be explained by the given features. It will give insight as to how well the model can predict the student's final score using these statistics. A score of 1 would mean than the student's grade is completely determined by these environemntal factors, while a score of 0 would suggest that academic performance is totally independent of them.

(3) Accuracy Score:

This returns a value between 0 and 1 which denotes how often the model predicted the correct result from two options. This metric was used for the pass/fail classification.

### Experiments

Before applying my model to the testing data, I used 5-fold Cross Validation to ensure that the model was behaving as expected. There was fairly little variation between different runs, suggesting that the model was behaving consistently and that hyper-parameter tuning was not necessary.

## Results and Analysis

The model had low overfitting, achieving an MSE of 8.65 on testing data and 7.20 on training data. The small difference between these numbers suggests that the model will generalise reliably as its performance on testing data was very similar to the data it learned from. These MSE values were significantly lower than the benchmark model's 65.37 and 64.20 on training and testing data respectively. This means that the model beat the crude benchmark model by a large margin.

However, the model struggled to predict the students' G3 scores, achieving an explained variance of 0.17 on testing data and 0.31 on training data. This means that the given data features are not enough to reliably say what numerial grade a student will achieve. This is completely expected as one would imagine that many other factors play a role in a student's success. For example, intelligence is not measured, and we have no way of knowing how different students will respond to exam pressure.

When using the model to classify the students into pass/fail, an accuracy of 84% was achieved. This is signifcantly better than predicting the G3 score, and this infomation is also very useful. Teachers and schools could use this model to predict which students are at risk of failing by looking at easy-to-obtain school reports and questionnaires.

Lastly, analysis of the model coefficients revealed which factors are the most influential. The most impactful negatively correlated statistics were number of previous class failures and weekday alcohol consumption. For positive correlation, the desire to pursue higher education, good familial relations, and more hours spent studying were the strongest predictors, followed closely by education level of the student's parents.

## Conclusion

Overall, the project was a success. My model was able to predict pass/fail with a reasonable accuracy, and the coefficient analysis answered the fundamental question of which features had the most impact on a student's academic success.

Further work on this topic could involve building a classification model with more labels than just pass/fail. A decision tree could be hyper-parameter tuned to give the best prediction of a student's grade. This would likely perform better than my regression model's prediction of G3. However, it seems unlikely that this model could reliably predict correctly. My explained variance results suggest that the features of the data do not encode enough information to truly know how students will fair in exam conditions.

