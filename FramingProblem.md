---
layout: page
title: Framing Prediction Problem
---

### Prediction Problem
We will trying to predict the position used for players given their pre-game and in-game data. Since there are more than 2 positions, this will be a multiclass classification

We chose to predict position because different champions can play different positions and we wanted to see if there was a pattern of position usage and if a well-tuned model could pick up on those patterns.

Because the consequence of an incorrect prediction is the same for all positions, we will be using **accuracy** as our main evaluation metric, as opposed to precision, recall, or F1 score

We know that all of our data at the "time of prediction" is relevant because there is no post-game data that would give away the classification.