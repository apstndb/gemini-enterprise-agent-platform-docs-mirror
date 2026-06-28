---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/intro-evaluation-fairness
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/intro-evaluation-fairness
title: Introduction to model evaluation for fairness
description: Learn about metrics that Gemini Enterprise Agent Platform provides to help you evaluate your model for bias.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

A machine learning workflow can include evaluating your model for fairness. An unfair model displays systemic bias that can cause harm, especially to traditionally underrepresented groups. An unfair model may perform worse for certain subsets, or *slices* , of the dataset.

You can detect bias during the data collection or post-training evaluation process. Gemini Enterprise Agent Platform provides the following model evaluation metrics to help you evaluate your model for bias:

  - [**Data bias metrics**](https://docs.cloud.google.com/vertex-ai/docs/evaluation/data-bias-metrics) : Before you train and build your model, these metrics detect whether your raw data includes biases. For example, a smile-detection dataset may contain far fewer elderly people than younger ones. Several of these metrics are based on quantifying the distance between label distribution for different groups of data:
    
      - Difference in Population Size.
    
      - Difference in Positive Proportions in True Labels.

  - [**Model bias metrics**](https://docs.cloud.google.com/vertex-ai/docs/evaluation/model-bias-metrics) : After you train your model, these metrics detect whether your model's predictions include biases. For example, a model may be more accurate for one subset of the data than the rest of the data:
    
      - Accuracy Difference.
    
      - Difference in Positive Proportions in Predicted Labels.
    
      - Recall Difference.
    
      - Specificity Difference.
    
      - Difference in Ratio of Error Types.

To learn how to include the model evaluation bias pipeline components in your pipeline run, see [Model evaluation component](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/model-evaluation-component#fairness) .

## Example dataset overview

For all examples related to fairness metrics, we use a hypothetical college admission dataset with features such as an applicant's high school grades, state, and gender identity. We want to measure whether the college is biased towards California or Florida applicants.

The target labels, or all possible outcomes, are:

  - Accept the applicant with scholarship ( `p` ).

  - Accept the applicant without a scholarship ( `q` )

  - Reject the applicant ( `r` ).

We can assume that admission experts provided these labels as the ground truth. Note that it's possible for even these expert labels to be biased, since they were assigned by humans.

To create a binary classification example, we can group labels together to create two possible outcomes:

  - Positive outcome, notated as `1` . We can group `p` and `q` into the positive outcome of "accepted `{p,q}` ."

  - Negative outcome, notated as `0` . This can be a collection of every other outcome aside from the positive outcome. In our college application example, the negative outcome is "rejected `{r}` ."

To measure bias between California and Florida applicants, we separate out two slices from the rest of the dataset:

  - Slice 1 of the dataset for which the bias is being measured. In the college application example, we're measuring bias for applicants from California.

  - Slice 2 of the dataset against which the bias is being measured. Slice 2 can include "everything not in slice 1" by default, but for the college application example, we are assigning slice 2 as Florida applicants.

In our example college application dataset, we have 200 applicants from California in slice 1, and 100 Florida applicants in slice 2. After training the model, we have the following confusion matrices:

| California applicants      | Acceptances (predicted) | Rejections (predicted) |
| -------------------------- | ----------------------- | ---------------------- |
| Acceptances (ground truth) | 50 (true positives)     | 10 (false negatives)   |
| Rejections (ground truth)  | 20 (false positives)    | 120 (true negatives)   |

| Florida applicants         | Acceptances (predicted) | Rejections (predicted) |
| -------------------------- | ----------------------- | ---------------------- |
| Acceptances (ground truth) | 20 (true positives)     | 0 (false negatives)    |
| Rejections (ground truth)  | 30 (false positives)    | 50 (true negatives)    |

By comparing metrics between the two confusion matrices, we can measure biases by answering questions such as "does the model have better recall for one slice than the other?"

We also use the following shorthand to represent labeled ground truth data, where `i` represents the slice number (1 or 2):

\\( l^0\_i = tn\_i + fp\_i \\)

For slice i, number of labeled negative outcomes = true negatives + false positives.

\\( l^1\_i = fn\_i + tp\_i \\)

For slice `i` , number of labeled positive outcomes = false negatives + true positives.

Note the following about the college application dataset example:

  - Some fairness metrics can be generalized for multiple outcomes as well, but we use binary classification for simplicity.

  - The example focuses on the classification task, but some fairness metrics generalize to other problems like regression.

  - For this example, we assume that the training data and test data are the same.

## What's next

  - Learn about the [data bias metrics](https://docs.cloud.google.com/vertex-ai/docs/evaluation/data-bias-metrics) supported by Gemini Enterprise Agent Platform.

  - Learn about the [model bias metrics](https://docs.cloud.google.com/vertex-ai/docs/evaluation/model-bias-metrics) supported by Gemini Enterprise Agent Platform.

  - Read the [model evaluation pipeline component reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/model-evaluation-component#fairness) .
