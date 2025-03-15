---
layout: page
title: Hypothesis Testing
---

<p class="message">
    This section is dedicated to the Hypothesis Testing
</p>

Question: Do tanks/bruiser have higher damage mitigated per minute compared to tanky supports?

Null Hypothesis: Tanks/bruisers have a higher damage mitigated than tanky supports.

Alternate Hypothesis: Tanks/bruisers have a lower damage mitigated than tanky supports.

Test Statistic: Difference in Means

Alpha Level: .05

Explanation:

    Null Hypothesis: Tanks/bruisers should have higher damage mitigated
     per minute due to being a solo laner ( Top Lane )

    Alternate Hypothesis: Opposite to the null hypothesis. Tanky supports
     should be protecting their ADC, and shielding the damage

    Test Statistic: We should be able to see a mean difference if true,
     since damage mitigated per minute is a numerical value

    Alpha Level: We set an alpha level of .05, because this is common
     and is enough to showcase if our p-value is true



```py
filtered_df.groupby('class_actual')['damagemitigatedperminute'].agg(['mean','count'])
```
<iframe src="{{ site.url }}{{ site.baseurl }}/assets/groupby.html" width=800 height=200 frameBorder=0></iframe>

We now need to observe the mean difference between both tank/bruiser and tanky supports. Here's
an interactable graph for damage mitgated per minute for each class

<iframe src="{{ site.url }}{{ site.baseurl }}/assets/damagemitigatedperminute_for_class.html" width=800 height=600 frameBorder=0></iframe>

In order to test our data, we need to shuffle the values around.
```py
with_shuffled = filtered_df.assign(Shuffled_Weights=np.random.permutation(filtered_df['damagemitigatedperminute']))
with_shuffled.head()
```

<iframe src="{{ site.url }}{{ site.baseurl }}/assets/shuffled_df.html" width=800 height=400 frameBorder=0></iframe>

```py
group_means = with_shuffled.groupby('class_actual').mean()
group_means
```

<iframe src="{{ site.url }}{{ site.baseurl }}/assets/group_means.html" width=800 height=200 frameBorder=0></iframe>

We can now compare the original graph, and the shuffled columns graph.
<iframe src="{{ site.url }}{{ site.baseurl }}/assets/shuffled_graph1.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="{{ site.url }}{{ site.baseurl }}/assets/shuffled_graph2.html" width=800 height=600 frameBorder=0></iframe>

Using the difference in means, we have found that the observed difference is -330, and our p-value is 0.
This suggests that tanks/bruiser have a higher damage mitigated overall compared to tanky support.

```py
n = 500

differences = []
for _ in range(n):

    with_shuffled = filtered_df.assign(Shuffled_Weights=np.random.permutation(filtered_df['damagemitigatedperminute']))

    group_means = (
        with_shuffled
        .groupby('class_actual')
        .mean()
        .loc[:, 'Shuffled_Weights']
    )
    difference = group_means.loc['tanky support'] - group_means.loc['tank/bruiser']

    differences.append(difference)
    
mean_weights = filtered_df.groupby('class_actual')['damagemitigatedperminute'].mean()
observed_difference = mean_weights['tanky support'] - mean_weights['tank/bruiser']
print(observed_difference)

p_value = (np.array(differences) <= observed_difference).mean()
print(p_value)
```

```py
-330.57659934042726
0.0
```

Conclusion:
    P-value = 0.0
    Since our P-value (0.0) is less than our significance level (alpha = .05), this suggests that tanks/bruiser
    have a higher damage mitigated per minute than tanky supports.


We will now focus on Framing a prediction problem:

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
