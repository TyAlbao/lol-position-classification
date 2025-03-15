---
layout: page
title: Fairness Analysis
---

### Two groups:
We decided to analyze the fairness in accuracies between the two different types of champions:
* Tanky Support
* Tank/Bruiser

Keep in mind that these classifications were made by ourselves and were not given in the dataset

### Hypotheses
Test statistic:
* difference in accuracy scores

Significance level:
* .01

Null:
* There is no difference in accuracy scores for Tanky Support and Tank/Bruiser classes
Alternative:
* Tanky Support class types have higher accuracy scores compared to Tank/Bruiser Class types

### Conclusion
After performing a permutation test of 1000 iterations, our p-value was 0.0

This means we reject the null and say that there is statistcal evidence that Tanky Supports have a higher accuracy score than Tank/Bruisers