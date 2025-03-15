---
layout: page
title: Final Model
---

## Features Added
* champion
* damagetochampions
* wardskilled
* killsshare
* deathsshare

### Reason
**champion**
* Most champions are used for a particular position. For example one champion's abilities are more optimized while playing top lane while another champion is best used as bottom lane. Some champions are useful in multiple positions, making this feature extremely helpful, but not a guarantee for success.

**damagetochampions**
* Since different positions have different roles, some positions are responsible for inflicting more damage on enemies. Knowing how much damage a player deals to enemy champions can help determine positions.

**wardskilled**
* jungle and support positions are known to kills more wards than other positions, so this stat is another feature that can help differenciate positions

**killsshare**
* This helps standardize the kills feature as it gives the number of kills relative to their teammates. This ensures that games where there were more or less kills than normal are not weighted differently. Since certain positions have higher kill rates than others, this can help classify positions

**deathsshare**
* Similar to the killsshare feature, deathsshare helps standardize the number of deaths to the number of deaths relative to their team. Doing this gives us a feature that doesn't skew the weights.

## Model Tuning Process
* Algorithm chosen: **Random Forest Classifier**
* Hyperparameters:
    * max_depth: **50**
    * n_estimators: **400**
    * min_samples_split: **20**

### Choosing Hyperparameters
* RandomSearchCV:
    * this generates a number of models with hyperparameters randomly chosen from a specified range
    * uses cross-validation method to test these parameters then gives best parameters
    * gave best params as:
        * max_depth: None
        * n_estimators: 400
        * min_samples_split: 2
    * training data accuracy:
        * 100%
    * testing data accuracy:
        * 94.32%
    * difference in training and testing data accuracies:
        * 5.68%
    * With 100% training accuracy and a difference in accuracies greater than 5%, this gave us motivation to tweak the model so it didn't overfit
* GridSearchCV:
    * this trains RFC models with every combination of hyperparameters listed
    * to avoid overfitting we limited the model to a max_depth of 50
    * this method gave best params as:
        * max_depth: 50
        * n_estimators: 400
        * min_samples_split: 20
    * training data accuracy:
        * 96.46%
    * testing data accuracy:
        * 93.47%
    * difference in training and testing data accuracies:
        * 2.99%
    * while these accuracy scores are lower than the previous parameters, we feel more comfortable with this model as the difference in accuracies is lower by more than 2%, giving us confidence that it won't overfit to more data in the future

### Comparing to Baseline Model
Baseline Model test data accuracy:
* 62.52%

Final Model test data accuracy:
* 93.47%

Final Model improvement:
* 30.95%

Our final model clearly had a major improvement from our baseline model