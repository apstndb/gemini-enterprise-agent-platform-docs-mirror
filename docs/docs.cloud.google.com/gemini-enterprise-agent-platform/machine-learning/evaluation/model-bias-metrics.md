---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/model-bias-metrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/model-bias-metrics
title: Model bias metrics for Agent Platform
description: Learn about evaluation metrics that Gemini Enterprise Agent Platform provides to help you detect model bias.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page describes model evaluation metrics you can use to detect *model bias* , which can appear in the model prediction output after you train the model. For the examples and notation on this page, we use a hypothetical college application dataset that we describe in detail in [Introduction to model evaluation for fairness](https://docs.cloud.google.com/gemini-enterprise-agent-platform/evaluation/intro-evaluation-fairness) .

For descriptions of metrics that are generated from pre-training data, see [Data bias metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/evaluation/data-bias-metrics) .

## Overview

In our example college application dataset, we have 200 applicants from California in slice 1, and 100 Florida applicants in slice 2. After training the model, we have the following confusion matrices:

| California applicants      | Acceptances (predicted) | Rejections (predicted) |
| -------------------------- | ----------------------- | ---------------------- |
| Acceptances (ground truth) | 50 (true positive)      | 10 (false negative)    |
| Rejections (ground truth)  | 20 (false positive)     | 120 (true negative)    |

| Florida applicants         | Acceptances (predicted) | Rejections (predicted) |
| -------------------------- | ----------------------- | ---------------------- |
| Acceptances (ground truth) | 20 (true positive)      | 0 (false negative)     |
| Rejections (ground truth)  | 30 (false positive)     | 50 (true negative)     |

You can generally interpret the sign for most metrics as follows:

  - Positive value: indicates a potential bias favoring slice 1 over slice 2.

  - Zero value: indicates no bias in between slice 1 and slice 2.

  - Negative value: indicates a potential bias in favoring slice 2 over slice 1.

We make a note where this doesn't apply to a metric.

## Accuracy Difference

Accuracy Difference measures the difference in accuracy between slice 1 and slice 2:

$$ \\frac{tp\_1 + tn\_1}{n\_1} - \\frac{tp\_2 + tn\_2}{n\_2} $$

((True positives for slice 1 + True negatives for slice 1)/Total number of instances for slice 1) - ((True positives for slice 2 + True negatives for slice 2)/Total number of instances for slice 2)

**In our example dataset** :

((50 correctly predicted California acceptances + 120 correctly predicted California rejections)/ 200 California applicants) - ((20 correctly predicted Florida acceptances + 50 correctly predicted Florida rejections)/ 100 Florida applicants) = 170/200 - 70/100 = 0.15

The positive value of the Accuracy Difference indicates that the model is more accurate for California applicants versus Florida applicants. This could indicate a potential bias favoring California applicants.

## Difference in Positive Proportions in Predicted Labels (DPPPL)

Difference in Positive Proportions in Predicted Labels (DPPPL) measures whether the model has a tendency to make disproportionately more positive predictions for one slice over the other. DPPPL calculates the difference in Positive Proportions in Predicted Labels, where Positive Proportions in Predicted Labels is (Predicted positive outcomes/Total number of instances) for a slice:

> **Note:** This metric is analogous to the [data bias metric](https://docs.cloud.google.com/gemini-enterprise-agent-platform/evaluation/data-bias-metrics) of *Difference in Positive Proportions in True Labels* , which focuses on labeled positive outcomes instead of predicted positive outcomes.

$$ \\frac{tp\_1 + fp\_1}{n\_1} - \\frac{tp\_2 + fp\_2}{n\_2} $$

((True positives for slice 1 + False positives for slice 1)/Total number of instances for slice 1) - ((True positives for slice 2 + False positives for slice 2)/Total number of instances for slice 2)

**For our example dataset** :

((50 correctly predicted California acceptances + 20 incorrectly predicted California acceptances)/ 200 California applicants) - ((20 correctly predicted Florida acceptances + 30 incorrectly predicted Florida acceptances)/ 100 Florida applicants) = 70/200 - 50/100 = -0.15

The negative value of the DPPPL indicates that the model disproportionately accepts more Florida applicants compared to California applicants.

## Recall Difference

Recall Difference measures the difference in recall between slice 1 and slice 2, looking only at labeled positive outcomes. Recall difference may also be called [*Equal Opportunity*](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/model-bias-metrics#whats-next) .

$$ \\frac{tp\_1}{l^1\_1} - \\frac{tp\_2}{l^1\_2} $$

(True positives for slice 1/(True positives for slice 1 + False negatives for slice 1)) - (True positives for slice 2/(True positives for slice 2 + False negatives for slice 2))

**In our example dataset** :

(50 correctly predicted California acceptances/(50 correctly predicted California acceptances + 10 incorrectly predicted California rejections)) - (20 correctly predicted Florida acceptances/(20 correctly predicted Florida acceptances + 0 incorrectly predicted Florida rejections)) = 50/60 - 20/20 = -0.17

The negative value indicates that the model is better at recalling Florida applicants than California applicants. In other words, the model tends to be more accurate in its acceptance decisions for Florida versus California applicants.

## Specificity Difference

Specificity Difference measures the difference in specificity, also known as the *true negative rate* , between slice 1 and slice 2. We can think of it as the recall difference but for labeled negative outcomes:

$$ \\frac{tn\_1}{l^0\_1} - \\frac{tn\_2}{l^0\_2} $$

(True negatives for slice 1/(True negatives for slice 1 + False positives for slice 1)) - (True negatives for slice 2/(True negatives for slice 2 + False positives for slice 2))

**In our example dataset** :

(120 correctly predicted California rejections/(120 correctly predicted California rejections + 20 incorrectly predicted California acceptances)) - (50 correctly predicted Florida rejections/(50 correctly predicted Florida rejections + 30 incorrectly predicted Florida acceptances)) = 120/140- 50/80 = 0.23

The positive value indicates that for application rejections, the model has better recall for California applicants compared to Florida applicants. In other words, the model tends to be more correct in its rejection decisions for applicants from California versus those from Florida.

## Difference in Ratio of Error Types

Difference in Ratio of Error Types measures the difference in how the errors (false negatives and false positives) are distributed between slice 1 and 2. The Ratio of Error Type is calculated as (False negatives (Type I error)/False positive (Type II error)). Difference in Ratio of Error Types may also be called [*Treatment Equality*](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/model-bias-metrics#whats-next) .

$$ \\frac{fn\_1}{fp\_1} - \\frac{fn\_2}{fp\_2} $$

(False negatives for slice 1/False positives for slice 1) - (False negatives for slice 2/False positives for slice 2)

**In our example dataset** :

(10 incorrectly predicted California rejections/20 incorrectly predicted California acceptances) - (0 incorrectly predicted Florida rejections/30 incorrectly predicted Florida acceptances) = (10/20 - 0/30) = 0.5

Although the model makes 30 errors for both the California and Florida applicants, the positive value for Difference in Ratio of Error Types indicates that the model tends to over-predict positive outcomes (higher false positive) and therefore under-predict negative outcomes (lower false negative errors) for California applicants, in comparison to the Florida applicants.

The sign of the Difference in Ratio of Error Types can be generally interpreted as:

  - Positive value: indicates that the model makes disproportionately more false positive errors than false negative errors for slice 1.

  - Zero value: indicates that the model makes the same amount of false positive errors for both slices.

  - Negative value: indicates that the model makes disproportionately more false positive errors than false negative errors for slice 2.

The sign for this metric doesn't necessarily indicate bias in the model, because the harmfulness of false negatives or false positives depends on the application of your model.

## What's next

  - Read the [model evaluation pipeline component reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/model-evaluation-component#fairness) .

  - Read more about fairness metrics in [A Survey on Bias and Fairness in Machine Learning](https://www.cs.purdue.edu/homes/bb/2020-fall-cs590bb/docs/Survery_of_Bias_and_Fairness_in_ML.pdf) .
