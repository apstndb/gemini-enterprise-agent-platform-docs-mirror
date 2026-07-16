---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular
title: Data types and transformations
description: Learn how to work with different types of tabular data for AutoML models.
data_source: docs.cloud.google.com
---

This page describes how Agent Platform works with different types of tabular data for AutoML models.

## Introduction to transformations in Gemini Enterprise Agent Platform

### Model training

Input tabular data must be transformed before it can be used for model training. The transformation indicates the function of a particular data feature.

The following transformations are supported:

  - [Categorical](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#categorical-transf)
  - [Text](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#text-transf)
  - [Numeric](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#numeric-transf)
  - [Timestamp](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#timestamp)

If your data source is a CSV file in Cloud Storage, commas (",") must be used for the delimiter. Agent Platform uses the [RFC 4180](https://tools.ietf.org/html/rfc4180) CSV format.

If your data source is BigQuery and you are performing classification or regression, you can include data that is made up of multiple data primitives. These compound data types must be pre-processed before transformations can be applied. The following compound data types are supported:

  - [Struct](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#struct)
  - [Array](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#array)

If a type value is missing or null, Gemini Enterprise Agent Platform handles it based on your model objective and the transformation applied for that feature. For details, see [How missing or null values are handled](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#null-values) .

### Prediction

The format of the data used for prediction must match the format used for training. For details, see [Data format for predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#format-for-prediction) .

## Agent Platform transformations

### Categorical

Applying a categorical transformation causes that feature to represent values in a category. That is, a nominal level. The values differ only based on their name without order. You can use numbers to represent categorical values, but the values have no numeric relationship with each other. That is, a categorical 1 is not "greater" than a categorical 0.

Here are some examples of categorical values:

  - Boolean - `true` , `false` .
  - Country - `"USA"` , `"Canada"` , `"China"` , and so on.
  - HTTP status code - `"200"` , `"404"` , `"500"` , and so on.

Categorical values are case-sensitive; spelling variations are treated as different categories (for example, "Color" and "Colour" are not combined).

When you train a model with a feature with a categorical transformation, Agent Platform applies the following data transformations to the feature, and uses any that provide signal for training:

  - The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
  - Convert the category name to a dictionary lookup index and generate an embedding for each index.
  - Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

Categorical transformations can be applied to STRING data in CSV files or to the following BigQuery data types:

  - INT64
  - NUMERIC, BIGNUMERIC
  - FLOAT64
  - BOOL
  - STRING
  - DATE
  - DATETIME
  - TIME
  - TIMESTAMP

### Text

A text transformation causes the feature to be used as free-form text, typically comprised of text tokens.

Here are some examples of text values:

  - `"The quick brown fox"`
  - `"This restaurant is the best! The food is delicious"`

For forecasting models, the text transformation is not supported for [covariate](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-parameters#feature-type) features.

When you train a model with a feature with a text transformation, Agent Platform applies the following data transformations to the feature, and uses any that provide signal for training:

  - The text as is--no change to case, punctuation, spelling, tense, and so on.

  - Tokenize text to words and generate 1-grams and 2-grams from words. Convert each n-gram to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
    
    [Tokenization](https://www.tensorflow.org/text#unicodescripttokenizer) is based on unicode script boundaries.

  - Missing values get their own lookup index and resulting embedding.

  - Stop-words receive no special treatment and are not removed.

Text transformations can be applied to STRING data in CSV files or to the following BigQuery data types:

  - STRING
  - DATETIME

### Numeric

A numeric transformation causes a column to be used as an ordinal or quantitative number. These numbers can be compared. That is, two distinct numbers can be less than or greater than one another.

Leading or trailing whitespace is trimmed.

The following table shows all compatible formats for a numeric transformation:

Format

Examples

Notes

Numeric string

"101", 101.5"

The period character (".") is the only valid decimal delimiter. "101,5" and "100,000" are not valid numeric strings.

Scientific notation

"1.12345E+11", "1.12345e+11"

See note for numeric strings regarding decimal delimiters.

Not a number

"NAN", "nan", "+NAN"

Case is ignored. Prepended plus ("+") or minus ("-") characters are ignored. Interpreted as NULL value.

Infinity

"INF", "+inf"

Case is ignored. Prepended plus ("+") or minus ("-") characters are ignored. Interpreted as NULL value.

If a value in a column with a numeric transformation does not conform to one of these formats, then either the entire row is excluded from training, or the value is treated as [null](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#null-values) . You choose between these outcomes when you select the numeric transformation.

When you train a model with a feature with a numeric transformation, Agent Platform applies the following data transformations to the feature, and uses any that provide signal for training:

  - The value converted to float32.
  - The z\_score of the value.
  - A bucket index of the value based on quantiles. Bucket size is 100.
  - log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
  - z\_score of log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
  - A boolean value that indicates whether the value is null.
  - Rows with invalid numerical inputs (for example, a string that can't be parsed to float32) are not included for training and prediction.
  - Extreme/outlier values are not given any special treatment.

Numeric transformations can be applied to STRING data in CSV files or to the following BigQuery data types:

  - INT64
  - NUMERIC, BIGNUMERIC
  - FLOAT64
  - STRING
  - TIMESTAMP

### Timestamp

A Timestamp transformation causes a feature to be used as a point in time, represented either as a civil time with a time zone, or a Unix timestamp. Only features with a Timestamp transformation can be used for the [Time column](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/prepare-tabular#time) .

If a time zone is not specified with the civil time, it defaults to UTC.

The following table shows all compatible timestamp string formats:

Format

Example

Notes

`%E4Y-%m-%d`

"2017-01-30"

See [the Abseil documentation](https://github.com/abseil/abseil-cpp/blob/8207907f4f7fbaeeaa2b7340c76875e06fd345ba/absl/time/time.h#L1264-L1313) for a description of this format.

`%E4Y/%m/%d`

"2017/01/30"

`%Y/%m/%d %H:%M:%E*S`

"2017/01/30 23:59:58"

`%d-%m-%E4Y`

"30-11-2018"

`%d/%m/%E4Y`

"30/11/2018"

`%d-%B-%E4Y`

"30-November-2018"

`%Y-%m-%dT%H:%M:%E*S%Ez`

"2019-05-17T23:56:09.05+00:00"

RFC 3339. Specify the time zone offset ( `z` ) in the format: `±HH:MM[:SS[.ffffff]]`

Unix timestamp string in seconds

"1541194447"

Only for times between 01/Jan/1990 and 01/Jan/2030.

Unix timestamp string in milliseconds

"1541194447000"

Unix timestamp string in microseconds

"1541194447000000"

Unix timestamp string in nanoseconds

"1541194447000000000"

If a value in a column with a timestamp transformation does not conform to one of these formats, then either the entire row is excluded from training, or the value is treated as [null](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#null-values) . You choose between these outcomes when you select the timestamp transformation.

When you train a model with a feature with a timestamp transformation, Agent Platform applies the following data transformations to the feature, and uses any that provide signal for training:

  - Apply the transformations for **Numerical** columns.
  - Determine the year, month, day,and weekday. Treat each value from the timestamp as a **Categorical** column.
  - Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.
  - Rows with invalid timestamp inputs (for example, an invalid timestamp string) are not included for training and prediction.

Timestamp transformations can be applied to STRING data in CSV files or to the following BigQuery data types:

  - INT64
  - STRING
  - DATE
  - DATETIME
  - TIMESTAMP

## Compound data types

Sometimes you need to include data that is made up of multiple data primitives, such as an array or a struct. Compound data types are available only by using BigQuery as a data source, and are not supported for forecasting models.

### Struct

A struct can be used to represent a group of labeled fields. A struct has a list of field names, each associated with a data type. The list of fields and their data types must be the same for all struct values in a column.

Here are some examples of structs:

  - Blood pressure - `{"timestamp": 1535761416, "systolic": 110, "diastolic": 70}`
  - Product - `{"name": "iPhone", price: 1000}`

You use the BigQuery STRUCT data type to represent structs.

Struct values are automatically flattened into fields. Agent Platform applies the data transformation to the flattened fields according to their transformation type.

### Array

An array can be used to represent a list of values. The contained values must accept the same transformation type. You can include structs in arrays; all of the structs in the array must have the same structure.

Agent Platform processes arrays as representing relative weight. In other words, items that appear later in the array are weighted more heavily than items that appear towards the beginning.

Here are some examples of arrays:

  - Product categories:
    
    `["Clothing", "Women", "Dress", ...]`

  - Most recent purchases:
    
    `["iPhone", "Laptop", "Suitcase", ...]`

  - User records:
    
    `[{"name": "Joelle", ID: 4093}, {"name": "Chloe", ID: 2047}, {"name": "Neko", ID: 3432}, ...]`

You use the BigQuery ARRAY data type to represent arrays.

The data transformation Agent Platform applies depends on the transformation type applied to the array:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Array type</th>
<th>Transformation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Numerical array</strong></td>
<td><ul>
<li>All transformations for <strong>Numerical</strong> types applied to the average of the last N items where N = {1, 2, 4, 8, all}. So the items most heavily emphasized are the ones towards the end of the array, not the beginning.</li>
<li>The average of empty arrays is treated as zero.</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Categorical array</strong></td>
<td><ul>
<li>For each element in the array of the last N items where N = {1, 2, 4, 8, all}, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.</li>
<li>Empty arrays treated as an embedding of zeroes.</li>
</ul></td>
</tr>
<tr class="odd">
<td><strong>Text array</strong></td>
<td><ul>
<li>Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for <strong>Text</strong> columns.</li>
<li>Empty arrays treated as an embedding of zeroes.</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Timestamp array</strong></td>
<td><ul>
<li>Apply the transformations for <strong>Numerical</strong> columns to the average of the last N items of the array. N = {1, 2, 4, 8, all}. This means that the items most heavily emphasized are the ones towards the end of the array.</li>
</ul></td>
</tr>
<tr class="odd">
<td><strong>Struct array</strong></td>
<td><ul>
<li>The structs in the array are flattened into individual fields, and assembled into arrays by field. The array transformation (as described in this table) is applied, according to the field type for that array.</li>
</ul></td>
</tr>
</tbody>
</table>

## How missing or null values are handled

How missing values are handled depends on your model objective and the transformation applied for that feature.

### Classification and Regression

For classification and regression models, null values result in an embedding for categorical and text transformations; for other transformations, the null value is left as null.

### Forecasting

For forecasting models, null values are imputed from the surrounding data. (There is no option to leave a null value as null.) If you would prefer to control the way null values are imputed, you can impute them explicitly. The best values to use might depend on your data and your business problem.

Missing rows (for example, no row for a specific date, with a data granularity of daily) are allowed, but Agent Platform does not impute values for the missing data. Because missing rows can decrease model quality, you should avoid missing rows where possible. For example, if a row is missing because sales quantity for that day was zero, add a row for that day and explicitly set sales data to 0.

### What values are treated as null values

When training an AutoML tabular model, Agent Platform treats the following values as null values:

  - A BigQuery [NULL value](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types) .

  - NaN or infinite numeric values.

  - An empty string. Agent Platform does not trim spaces from strings. That is, " " is *not* considered a null value.

  - A string that can be [converted to NaN or an infinite numeric value](https://en.cppreference.com/w/c/string/byte/strtof) .
    
      - For "NAN": ignore case, with an optional plus or minus prepended.
      - For "INF": ignore case, with an optional plus or minus prepended.

  - Missing values.

  - Values in a column with a Numeric or Timestamp transformation that are not in a valid format for the column's transformation. In this case, if you specified that the row with the invalid value should be used in training, the invalid value is considered to be null.

## Data format for predictions

The format of data used for prediction must match the format used for training.

If you trained your model on data in a CSV file in Cloud Storage, your data was of type STRING. If you are using a JSON object to send your prediction request, ensure that all the values in the key-value pairs are also of type STRING.

If you trained your model on data stored in BigQuery and you are using a JSON object to send your prediction request, the data types of the values in the JSON key-value pairs must follow the mapping in the table below.

BigQuery data type

JSON data type

INT64

String

NUMERIC, BIGNUMERIC

Number

FLOAT64

Number

BOOL

Boolean

STRING

String

DATE

String

DATETIME

String

TIME

String

TIMESTAMP

String

Array

Array

STRUCT

Object

For example, if your training data contained `length` features of type FLOAT64, the following JSON key-value pair is correct:

    "length":3.6,

Conversely, the following JSON key-value pair will throw an error:

    "length":"3.6",

## What's next

  - Learn more about [BigQuery data types](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types)
  - Learn how to [prepare your tabular training data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/prepare-tabular)
  - Learn about [best practices for creating tabular training data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/bp-tabular)
