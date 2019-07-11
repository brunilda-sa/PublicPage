---
layout: default
title: Multi-label classification for Satellite Images
description: This section provides details about the Multi-Label Classifier build in the context of this project
---

# Multi-label classification for Satellite Images

## Introduction
In this notebook we are going to build a multi-label classification model, where given a specific satellite image the model will associate all labels belonging to it. The labels associated to the satellite images describe differents atmospheric conditions and various classes of land cover/land use. 
There are 17 possible labels: agriculture, artisinal_mine, bare_ground, blooming, blow_down, clear, cloudy, conventional_mine, cultivation, habitation, haze, partly_cloudy, primary, road, selective_logging, slash_burn, water.

### Data source and description
The dataset contains the list of labels and satellite images. Images have four bands of data: red, green, blue, and near infrared
The data comes from Planet (https://www.planet.com/) and its Brazilian partner SCCON (https://www.sccon.com.br/)
Data list:
-  train.csv - contains the training file names and their labels, the labels are space-delimited
-  sample_submission.csv - contains all file names and their labels in the test set
-  train-jpg.zip - images for the train set
-  test-jpg.zip - images for the test set

### What is a Multi-Label Classification
Multi-label classification is task of finding multiple key features from one specific satellite image. In others words one image can be associated to several classes/labels.

## Challenges
- Multi-Label classification. Normally classification are bynary or multi-classes.
- Large dataset, the training data has over one million rows 
- Imbalanced Dataset

### Methodology 
-  Apply several approaches
  - Baseline Approach: Use scikit-learn Classifiers to build a multi-label model 
  - Second Approach: Use CNN and Transfer Learning neural networks to build a multi-label model 
  - Third Approach: Feature Engineer the predefined classes
-  Load a subset of data with 10000 samples and have a first overview of the labels distribution
-  Preprocess Data, e.g. preformat images for scikit-learn Classifiers, vectorize the labels, etc.
-  Select scikit-learn Classfiers that handle multi-label classification
-  Select the best metric for the project
-  Hyperparameter optimization and select the best paramter for each classifier 
-  Use the selected parameters and score each classfier
-  Select the classifier obtaining the best score
-  Score selected classifier using the test data set

### Metric to be used
**F2 Score**: When plotting the labels distribution, we could observed that we have very imbalanced data
. In this case one the most commonly use metrics is  the F2 score. The Fβ score, measures accuracy using the precision and recall. Precision is the ratio of true positives (tp) to all predicted positives (tp + fp). Recall is the ratio of true positives to all actual positives (tp + fn). The F2 score is given by (1+β2)prβ2p+r  where  p=tptp+fp,  r=tptp+fn, β=2. Note that the F2 score weights recall higher than precision.

**Confusion Matrix**: A breakdown of predictions into a table showing correct predictions (the diagonal) and the types of incorrect predictions made (what classes incorrect predictions were assigned).

## Overview of differents strategies
## Baseline approach
For the Baseline approach, we are going to proceed to a comparison analysis, based on the F2 score, among the following classifiers:
  - KNN Classifier
  - MLKNN Classifier
  - RandomForestClassifier
  - OneVsRestClassifier
  
## Second approach
For the second approach, we are going to proceed to a comparison analysis, based on the F2 score, among the following neural networks:
- CNN
- MobileNet
- VGG16

## Third approach
For the Third approach, we are going to proceed to a comparison analysis, based on the F2 score, among the all classifiers and all neural network, after been feature engineering our labels.

## Results
**Baseline Approach** 
Overall results
- KNN                   : 0.712568
- MLKNN                 : 0.747465
- RandomForestClassifier: 0.698658
- OnevsRestClassifier   : 0.681306

Results per Classes
Even if we obtained reasonables scores when analysing the results per label, without surprise all Classifiers missed to predict labels having under-sampled data, i.e. conventional_mine, selective_logging, blow_down, blooming, artisinal_mine

**Second Approach**
- CNN                   : 0.732413
- MobileNet             : 0.702046
- VGG16                 : 

**Third Approach**
Classifiers
- KNN                   : 0.774087
- MLKNN                 : 0.816947
- RandomForestClassifier: 0.814515
- OnevsRestClassifier   : 0.778788

Results per Classes
When analysing the results per label, all Classifiers were able to predict all labels

Neural Networks
- CNN                   : 
- MobileNet             : 
- VGG16                 : 

## Conclusion
From this decrease in F2 score we can assume our models are not generalizing well to the unseen validation data. We definitely have a lot of room for improvement!

_yay_

[back](./)
