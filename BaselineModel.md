---
layout: page
title: Baseline Model
---

## Model used:
* Random Forest Classifier
* feature to be predicted: **position**

### Quantitative Features
* kills	
* deaths	
* assists	
* damageshare	
* wardsplaced	
* earnedgoldshare
* **total: 6**

### Nominal Features
* year
* patch
* **total: 2**

### Ordinal Features
* no ordinal features were used
* **total: 0**

### Encodings
* RFC don't need numerical data to be scaled or altered, so all quantitative features remained as is
* We used One Hot Encoding on the year and patch features
  * although year and patch are stored as numbers, they have no order or weight

<br>

## Model Performance
The five different positions are model can predict are:
* bot	
* jng	
* mid	
* sup	
* top

Because the consequence of an incorrect prediction is the same for all positions, we will be using **accuracy** as our main evaluation metric, as opposed to precision, recall, or F1 score

### Model hyperparameters:
These were arbitrarily chosen, just to give us a reference of how good the model would be without any tuning
* max_depth: None
  * None because we were curious to see how far down a decision tree would go without limiting it
* n_estimators: 300
  * 300 was set because it is a decently high number for the size of our dataset

### Training Data
* accuracy score: **100%**
* this means there is a very good chance the model took advantage of having no limit for max_depth and the random forest has many deep trees
* very good change this model overfit to the data

### Testing Data
* accuracy score: **62.76%**
* comparing this to the training data score, it is clear our baseline model was overfitting
* difference in training and testing scores: **37.24%**

## Conclusion
We need to tune our model's hyperparameters so that it does not overfit