---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/ml-use
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/ml-use
title: About data splits for AutoML models
description: Learn how Gemini Enterprise Agent Platform splits image data into training, validation, and test sets for training AutoML models, and how you can control this data splitting process.
data_source: docs.cloud.google.com
---

This page describes how Gemini Enterprise Agent Platform uses the training, validation, and test sets of your data to train an AutoML model and the ways you can control how your data is split among these three sets. AutoML uses data splits differently depending on the data type of the training data.

This page describes data splits for image data. For information about data splits for tabular data, see [Data splits for tabular data](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/data-splits) .

For image datasets, AutoML uses the training set to train the model, and the validation set to validate the results that the model returns during training. When training is complete, AutoML uses the test set to provide the final evaluation metrics.

You can let Gemini Enterprise Agent Platform divide your data automatically. Your data is randomly split into the three sets by percentage. This is the easiest way to split your data, and works well in most cases.

| Set        | Percentage |
| ---------- | ---------- |
| Training   | 80         |
| Validation | 10         |
| Test       | 10         |

To use the default data split, accept the default in the Google Cloud console, or leave the [split](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#inputdataconfig) field empty for the API.

If you want to control how your data is split into sets, you have the following options:

  - [Manual split](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/ml-use#ml-use-unstructured)
  - [Data filter split](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/ml-use#filter)
  - [Mathematical split](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/ml-use#percentages)

Choose only one of these options; make the choice when you train your model. Some of these options require changes to the training data (for example, the `ml_use` label). Including data or labels for data split options does not require you to use those options; you can still choose another option when you train your model.

## Manual split for unstructured data

The manual split is also known as "predefined split".

To use the `ml_use` label to control your data split, you must set the `ml_use` label on your data.

### Set a value for the ml\_use label

You can set the `ml_use` label for image data at data import time (per data item or for the entire import file), or after data import by using the Google Cloud console.

#### Setting ml\_use on individual data items at import time

Set the `ml_use` label on each data item by including a value for the `aiplatform.googleapis.com/ml_use` field in your [JSON Lines](https://jsonlines.org/) data, or setting the value of the first column of the CSV file. See the information about preparing data for your data type for more details.

If any of your data items repeat in your data (if the same image snippet appears multiple times in your import file), Agent Platform uses the `ml_use` value for the first data item it encounters, and ignores any subsequent `ml_use` values. The first encountered item is not necessarily the item that is nearer to the beginning of the upload file.

#### Setting ml\_use for entire upload files

If your data can be sorted into different upload files by `ml_use` value, you can set the `ml_use` value for the entire upload file by using the per-file drop-down menu when you upload files using the Google Cloud console, or by using the [`dataItemLabels`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/import#ImportDataConfig) map field in the [datasets.import](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/import) method.

If you set `ml_use` for an upload file, and the file also contains `ml_use` values, the `ml_use` values in the file take precedence over the file-wide value.

#### Setting ml\_use after import

After you upload your data, you can set or update the `ml_use` value for specific data items in the Google Cloud console by selecting one or more items in the list view and using the **Assign ML use** drop-down menu.

If you upload a data file again, even if the ml\_use values have changed, it doesn't update the `ml_use` value. You can't update `ml_use` values after import by using the Agent Platform API.

### Use the ml\_use label

When you train your model, specify **Manual (Advanced)** for the Data split in the Google Cloud console. If you train using the Agent Platform API, use the [FilterSplit](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#filtersplit) object, specifying `labels.aiplatform.googleapis.com/ml_use=training` for the training filter, `labels.aiplatform.googleapis.com/ml_use=validation` for the validation filter, and `labels.aiplatform.googleapis.com/ml_use=test` for the test filter. For example:

    model = job.run(
    dataset=dataset,
    model_display_name=_name,
    training_filter_split="labels.aiplatform.googleapis.com/ml_use=training",
    validation_filter_split="labels.aiplatform.googleapis.com/ml_use=validation",
    test_filter_split="labels.aiplatform.googleapis.com/ml_use=test")

Any data items with an `ml_use` value are assigned to the specified set. Data items that don't have `ml_use` set are excluded from the training process.

## Data filter split

You can use other labels (besides ml-use) and other fields to split your data by using the [FilterSplit](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#filtersplit) object in the Agent Platform API. For example, you could set the `trainingFilter` to `labels.flower=rose` , the `validationFilter` to `labels.flower=daisy` , and the `testFilter` to `labels.flower=dahlia` . This setting causes all data labeled as `rose` to be added to the training set, all data labeled as `daisy` added to the validation set, and all data labeled as `dahlia` to be added to the test set.

If you filter on multiple fields, a data item could match more than one filter. In this case, the training set takes precedence, followed by the validation set, followed by the test set. In other words, an item is put into the test set only if it matches the filter for the test set, but does not match for either the training or validation filters. If an item does not match the filters for any of the sets, it is excluded from training.

Don't use categories for your data split related to what the model will be predicting; each of your sets must reflect the range of data that the model uses to make predictions. (For example, don't use the filters described previously for a model expected to categorize pictures by flower type.)

If you don't want a filter to match any items, set it to " `-` " (the minus sign).

## Mathematical split

The mathematical split is also known as "fraction split".

By default, your data is randomly split into the sets according to the default percentages for your data type. You can change the percentages to any values that add up to 100 (for the Agent Platform API, use fractions that add up to 1.0).

To change the percentages (fractions), use the [FractionSplit](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#FractionSplit) object to define your fractions. For image data types, you can also use the Google Cloud console to update your split percentages when you train your model.
