---
layout: page
title: Framing Prediction Problem
---

### Prediction Problem

Our goal is to build a multiclass classification model that predicts the role or position (bot, jng, mid, sup, or top) of a player in a game. The response variable we are predicting is position, which is categorical with five distinct classes.

This problem is a multiclass classification because:

* The target variable (position) has more than two possible values.
* Each instance belongs to one of these five mutually exclusive classes.

Choice of Response Variable
We chose position as the response variable because:

* A player’s role is critical for team strategy and game performance.
* Understanding how features like kills, assists, earned gold share, and damageshare correlate with a player's role can provide insights into gameplay patterns.

Evaluation Metric Choice
Since we are dealing with a multiclass classification problem, our choice of evaluation metric is accuracy.
Accuracy is appropriate in this case because:

* All classes are equally important – misclassifying a bot as a jng is just as bad as misclassifying a top as a sup.
* We don’t have an imbalanced dataset – If one role had significantly fewer instances, then F1-score would be more appropriate.
* Interpretability – Accuracy is an intuitive and widely understood metric for classification problems

Features Used for Prediction
We ensured that all features used in training would be available at the time of prediction

* Kills, deaths, assists, earned gold share, damageshare are all in-game statistics that are known at any moment during the match.
* We did not include features that depend on the game’s final outcome (such as win/loss or final gold amount).
