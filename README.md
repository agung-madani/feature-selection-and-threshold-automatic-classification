# Analysis of Feature Selection and Automatic Threshold in Classification Modeling

## Introduction

This repository contains the code and analysis for a project that aims to analyze and optimize classification modeling using automatic feature selection and threshold techniques. The project addresses the challenge of selecting relevant features and determining the optimal automatic threshold to improve the performance of a classification model.

### Problem Statement

The primary problem addressed in this project is how to select the most relevant and significant features in a given dataset and determine the optimal automatic threshold to enhance the performance of a classification model.

### Goal

The project's goal is to present a comprehensive approach to feature selection and automatic threshold determination in classification modeling. The approach involves using two different feature selection methods, MRMR (Minimum Redundancy Maximum Relevance) and ReliefF, to obtain an informative subset of features from the dataset. Additionally, it demonstrates the use of the Maximum Fisher's Discriminant Ratio (F1) method to determine the optimal automatic threshold.

## Dataset

The dataset used in this project is the "Body Performance Data" obtained from Kaggle, which contains information about a person's performance level (Grade)/fitness with various features, including age and sports performance data. The dataset has 11 features and 1 target variable with four classes (A, B, C, D).

### Data Preprocessing

- Duplicate rows were removed from the dataset.
- Labels 'A', 'B', 'C', 'D' were mapped to numeric values 0, 1, 2, 3.
- Gender labels 'M' and 'F' were mapped to numeric values 1 and 2.
- The dataset was split into features (X) and the target variable (y).
- Standard scaling was applied to normalize the features.

## Feature Selection Methods

### MRMR (Minimum Redundancy Maximum Relevance)

MRMR is a feature selection method that aims to select a subset of features with maximum relevance to the target variable and minimum redundancy among the selected features. It combines relevance and redundancy concepts to find informative and distinct features.

#### Key Steps in MRMR:

1. Compute F-statistics and initialize the correlation matrix.
2. Select features iteratively by maximizing relevance and minimizing redundancy.
3. Repeat for a specified number of features (k).

### ReliefF

ReliefF is another feature selection method that ranks features based on their ability to distinguish between instances close to each other. It considers the impact of each feature on class separation.

#### Key Steps in ReliefF:

1. Randomly select an instance and find its k-nearest neighbors from the same class (hits) and different classes (misses).
2. Update feature weights based on the differences between the selected instance's feature values and hits/misses.
3. Repeat for all instances and features.

## Results of Feature Selection

The feature selection methods were applied with different values of k. Here are the selected features for each method:

### MRMR Selection (k=3):
- Features: 'sit and bend forward_cm', 'sit-ups counts', 'broad jump_cm'

### MRMR Selection (k=6):
- Features: 'weight_kg', 'body fat_%', 'diastolic', 'sit and bend forward_cm', 'sit-ups counts', 'broad jump_cm'

### ReliefF Selection (k=3):
- Features: 'gender', 'sit and bend forward_cm', 'broad jump_cm'

### ReliefF Selection (k=6):
- Features: 'gender', 'weight_kg', 'diastolic', 'systolic', 'sit and bend forward_cm', 'broad jump_cm'

### ReliefF Selection with F1 Threshold:
- Features: All features except 'age'

## Automatic Threshold with F1

Automatic thresholding with F1 is a method for automatically selecting thresholds in classification modeling based on the Maximum Fisher's Discriminant Ratio (F1). F1 measures significant differences between class groups.

#### Key Steps in F1 Threshold Calculation:

1. Calculate the mean, variance, and class proportions for each class.
2. Calculate F1 value based on means, variances, and proportions.
3. The F1 score indicates the quality of the threshold.

The calculated F1 score is 0.009551998997520652, which is used to threshold the ReliefF-selected features.

## Training and Model Evaluation

The dataset was split into a training set (70%) and a testing set (30%). The Random Forest Classifier algorithm was used for training, and the models were evaluated using accuracy. Additionally, training times were measured to assess efficiency.

### Model Accuracy and Training Time:

- Using all features resulted in an accuracy of 0.7337 with the longest training time.
- MRMR selection with k=3 achieved an accuracy of 0.5567 with faster training time.
- MRMR selection with k=6 had a slightly improved accuracy of 0.6199 with longer training time.
- ReliefF selection with k=3 yielded an accuracy of 0.4858 with the fastest training time.
- ReliefF selection with k=6 improved accuracy to 0.5669 with still faster training time.
- ReliefF selection with F1 threshold achieved the highest accuracy of 0.6518 but required the longest training time.

## Conclusion

In conclusion, this project explored feature selection and automatic threshold techniques in classification modeling. MRMR and ReliefF were used for feature selection, and F1 thresholding was applied. The findings suggest that combining ReliefF with F1 thresholding can lead to optimal feature subsets and improved model performance. However, it comes at the cost of longer training times. The choice of feature selection method should consider the trade-off between accuracy and training efficiency. Automatic thresholding with F1 provides a convenient way to determine thresholds in classification tasks.
