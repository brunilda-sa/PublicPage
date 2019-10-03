---
layout: default
title: Multi-label classification for Satellite Images
description: This page provides details about the Multi-Label Classifier for satellite images project
---
# Multi-label classification for Satellite Images

## Introduction
In this project we are going to build a `multi-label classification model`, where given a specific satellite image the model will associate all labels belonging to it. The labels associated to the satellite images describe differents atmospheric conditions and various classes of land cover/land use. 

There are `17 possible labels`: agriculture, artisinal_mine, bare_ground, blooming, blow_down, clear, cloudy, conventional_mine, cultivation, habitation, haze, partly_cloudy, primary, road, selective_logging, slash_burn, water.

Several challenges should be considered in the process of building this classifier, below a few of them:
- Multi-Label classification task
- Large dataset, the training data has over one million rows 
- Imbalanced dataset

## Data source and description
The dataset contains the list of labels and satellite images. Each image have four bands of data: red, green, blue, and near infrared.

The data comes from [Planet](https://www.planet.com/) and its Brazilian partner [SCCON](https://www.sccon.com.br/) and the list and description of available files is below:
-  train.csv             : contains the training file names and their labels
-  sample_submission.csv : contains the test set names and their labels
-  train-jpg.zip         : contains the set of Train images
-  test-jpg.zip          : contains the set of Test images

## Concepts Overview
### What is a Multi-Label Classification
Multi-Label classification means a classification task with more than one classe can be associated to the target;  the model assigns to each sample a set of target labels. This can be thought as predicting properties of a data-point that are not mutually exclusive.

### Metrics description
-  **F2 Score**: The most commonly use metrics to be use for imbalanced data is the F2 score. The F2 score, measures accuracy using the precision and recall. The F2 score is given by (1+β2)(pr/(β2p+r))  where  p=tptp+fp,  r=tptp+fn, β=2. Note that the F2 score weights recall higher than precision.
-  **Precision**: is the ratio of true positives (tp) to all predicted positives (tp + fp)
-  **Recall**   :is the ratio of true positives to all actual positives (tp + fn)

## Methodology 
-  Define several strategies. Refer to section [Strategies overview](#Strategies-overview) to have more details about this
-  Select the best metric for a multi-label classification task
-  Load a subset of data with at least 10000 samples and have a first overview of the labels distribution
-  EDA, Preprocess and Clean Data
-  Feature Engineer
-  Scale
-  Deal with Classe imbalance
-  Hyperparameter optimization using the cross-validation approach
-  Select the best model
-  Final score using the set of test data
-  Analyse reesults and select the best model

## Strategies overview
To find the best model in terms of scoring, time consuming and computational requirements, below the strategies that will be implemented:
* `Baseline Approach`: For this approach a preselected `scikit-learn classifiers` will be used to build our model
* `Second Approach`  : For this approach a `CNN neural network` will be used to build our model
* `Third Approach`   : For this approach the `Transfer Learning concept for neural network` will be used to build our model

### Baseline approach
The Baseline approach consists in implement a multi-label classification model using the `scikit-learn classifiers` listed below:
  - KNN Classifier
  - MLKNN Classifier
  - RandomForestClassifier
  - OneVsRestClassifier with LogisticRegression
  - OneVsRestClassifier with LinearSVC
  
The best classifier will be selected based on the F2 score, the execution timing and the computational requirements and then compare with others aproaches.

For more information about the models above, please refer to the [scikit Learn web page](https://scikit-learn.org/stable/modules/multiclass.html).
  
### Second approach
The Second approach consists in implement a multi-label classification model using a `CNN Convolutional neural network` :

The model will be evaluated based on the F2 score, the execution timing and the computational requirements and then compare with others aproaches.

### Third approach
The Third approach consists in implement a multi-label classification model using a the pre-trained neural network below:
- MobileNet
- VGG16

The best neural network will be selected based on the F2 score, the execution timing and the computational requirements and then compare with others aproaches.

## Results Summary
In this section we are going to present a summary of results. For more the details about the results and visualization, please refer to the [previous page](https://brunildacity01.github.io/MyProjects/#my-upcoming-project), under the section `Notebooks`.

**Baseline Approach** 

`Average Score`
- KNN                                   : 0.709413
- MLKNN                                 : 0.747590
- RandomForestClassifier                : 0.697395
- OnevsRestClassifier_LogisticRegression: 0.639626
- OnevsRestClassifier_LinearSVC         : 0.672187

`Score per class`

As shown below, classifiers were not able to predict labels having under-sampled data, in our case as shown in the i.e. conventional_mine, selective_logging, blow_down, blooming, artisinal_mine

![ALT_Text]("https://raw.githubusercontent.com/brunildacity01/MyProjects/master/Images/Results_PerLabelBaseline.png")

**Second Approach**

`Average Score`
- CNN                                   : 0.732413
- MobileNet                             : 0.702046
- VGG16                                 : work in progress

**Third Approach**

`Classifiers`
Average Score
- KNN                                   : 0.774087
- MLKNN                                 : 0.816947
- RandomForestClassifier                : 0.781214
- OnevsRestClassifier_LogisticRegression: 0.762463
- OnevsRestClassifier_LinearSVC         : 0.701709

Score per class

As shown below, when analysing the results per label, all Classifiers were able to predict all labels

![ALT_Text]("https://raw.githubusercontent.com/brunildacity01/MyProjects/master/Images/Results_PerLabelThird.png")

`Neural Networks`

- CNN                                   : 0.866102
- MobileNet                             : 0.772362
- VGG16                                 : work in progress

## Conclusion
**Baseline Approach** 
- In average the F2 score for all Classifiers is 0.6932422, which is a good score taking into account the complexity of the task
- The MLKNN Classifier has obtained the best average F2 score, but the second place when predicting each label  
- OneVsRestClassifier with LogisticRegression has obtained the lowest average F2 score, but the first in predicting each label. Setting the class_weight to 'balanced' has certendly improved the performances

- `Selection`: With an average F2 score of 0.639626 and a classification of 15 labels over 17, the OneVsRestClassifier with LogisticRegression is the best model overall

**Second Approach**
- In average the F2 score for all neural networks is 0.7172295, which is a good score and 3.3444386 % better than the Baseline approach. We can say that neural network perform slightly better than scikit-learn Classifiers

- `Selection`: Among all the neural networks CNN performed the better with an average F2 score of 0.732413 

**Third Approach**
- In average the F2 score for all Classifiers is 0.767284, which is a good score and 9.649855855% better than the Baseline approach and 6.523594914% better than the second approach
- The MLKNN Classifier has obtained the best average F2 score and was able to predict all labels  
- OneVsRestClassifier with LinearSVC has obtained the lowest average F2 score, but was able to predict all labels

- `Selection`: With an average F2 score of 0.816947 the OneVsRestClassifier with LinearSVC is the best model overall

To conclude on what approach/model is the best, more analysis will be required. The next steps will be:
- Build a model based on the pretrained VGG16 neural network
- Resampling the dataset
- Improve the hyperparameter optimization, on neural networks


[back](./)

