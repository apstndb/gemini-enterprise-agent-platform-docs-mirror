---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1/schema/modelevaluation.metrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1/schema/modelevaluation.metrics
title: Package google.cloud.aiplatform.v1.schema.modelevaluation.metrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  BoundingBoxMetrics  ` (message)
  - `  BoundingBoxMetrics.ConfidenceMetrics  ` (message)
  - `  ClassificationEvaluationMetrics  ` (message)
  - `  ClassificationEvaluationMetrics.ConfidenceMetrics  ` (message)
  - `  ConfusionMatrix  ` (message)
  - `  ConfusionMatrix.AnnotationSpecRef  ` (message)
  - `  ForecastingEvaluationMetrics  ` (message)
  - `  ForecastingEvaluationMetrics.QuantileMetricsEntry  ` (message)
  - `  GeneralTextGenerationEvaluationMetrics  ` (message)
  - `  ImageObjectDetectionEvaluationMetrics  ` (message)
  - `  ImageSegmentationEvaluationMetrics  ` (message)
  - `  ImageSegmentationEvaluationMetrics.ConfidenceMetricsEntry  ` (message)
  - `  PairwiseTextGenerationEvaluationMetrics  ` (message)
  - `  QuestionAnsweringEvaluationMetrics  ` (message)
  - `  RegressionEvaluationMetrics  ` (message)
  - `  SummarizationEvaluationMetrics  ` (message)
  - `  TextExtractionEvaluationMetrics  ` (message)
  - `  TextExtractionEvaluationMetrics.ConfidenceMetrics  ` (message)
  - `  TextSentimentEvaluationMetrics  ` (message)
  - `  TrackMetrics  ` (message)
  - `  TrackMetrics.ConfidenceMetrics  ` (message)
  - `  VideoActionMetrics  ` (message)
  - `  VideoActionMetrics.ConfidenceMetrics  ` (message)
  - `  VideoActionRecognitionMetrics  ` (message)
  - `  VideoObjectTrackingMetrics  ` (message)

## BoundingBoxMetrics

Bounding box matching model metrics for a single intersection-over-union threshold and multiple label match confidence thresholds.

Fields

`confidence_metrics[]`

`  ConfidenceMetrics  `

Metrics for each label-match confidence\_threshold from 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99. Precision-recall curve is derived from them.

`iou_threshold`

`float`

The intersection-over-union threshold value used to compute this metrics entry.

`mean_average_precision`

`float`

The mean average precision, most often close to `auPrc` .

## ConfidenceMetrics

Metrics for a single confidence threshold.

Fields

`confidence_threshold`

`float`

The confidence threshold value used to compute the metrics.

`recall`

`float`

Recall under the given confidence threshold.

`precision`

`float`

Precision under the given confidence threshold.

`f1_score`

`float`

The harmonic mean of recall and precision.

## ClassificationEvaluationMetrics

Metrics for classification evaluation results.

Fields

`confidence_metrics[]`

`  ConfidenceMetrics  `

Metrics for each `confidenceThreshold` in 0.00,0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 and `positionThreshold` = INT32\_MAX\_VALUE.

ROC and precision-recall curves, and other aggregated metrics are derived from them. The confidence metrics entries may also be supplied for additional values of `positionThreshold` , but from these no aggregated metrics are computed.

`confusion_matrix`

`  ConfusionMatrix  `

Confusion matrix of the evaluation.

`au_prc`

`float`

The Area Under Precision-Recall Curve metric. Micro-averaged for the overall evaluation.

`au_roc`

`float`

The Area Under Receiver Operating Characteristic curve metric. Micro-averaged for the overall evaluation.

`log_loss`

`float`

The Log Loss metric.

## ConfidenceMetrics

Fields

`confusion_matrix`

`  ConfusionMatrix  `

Confusion matrix of the evaluation for this confidence\_threshold.

`confidence_threshold`

`float`

Metrics are computed with an assumption that the Model never returns predictions with score lower than this value.

`max_predictions`

`int32`

Metrics are computed with an assumption that the Model always returns at most this many predictions (ordered by their score, descendingly), but they all still need to meet the `confidenceThreshold` .

`recall`

`float`

Recall (True Positive Rate) for the given confidence threshold.

`precision`

`float`

Precision for the given confidence threshold.

`false_positive_rate`

`float`

False Positive Rate for the given confidence threshold.

`f1_score`

`float`

The harmonic mean of recall and precision. For summary metrics, it computes the micro-averaged F1 score.

`f1_score_micro`

`float`

Micro-averaged F1 Score.

`f1_score_macro`

`float`

Macro-averaged F1 Score.

`recall_at1`

`float`

The Recall (True Positive Rate) when only considering the label that has the highest prediction score and not below the confidence threshold for each DataItem.

`precision_at1`

`float`

The precision when only considering the label that has the highest prediction score and not below the confidence threshold for each DataItem.

`false_positive_rate_at1`

`float`

The False Positive Rate when only considering the label that has the highest prediction score and not below the confidence threshold for each DataItem.

`f1_score_at1`

`float`

The harmonic mean of recallAt1 and precisionAt1.

`true_positive_count`

`int64`

The number of Model created labels that match a ground truth label.

`false_positive_count`

`int64`

The number of Model created labels that do not match a ground truth label.

`false_negative_count`

`int64`

The number of ground truth labels that are not matched by a Model created label.

`true_negative_count`

`int64`

The number of labels that were not created by the Model, but if they would, they would not match a ground truth label.

## ConfusionMatrix

Fields

`annotation_specs[]`

`  AnnotationSpecRef  `

AnnotationSpecs used in the confusion matrix.

For AutoML Text Extraction, a special negative AnnotationSpec with empty `id` and `displayName` of "NULL" will be added as the last element.

`rows[]`

`  ListValue  `

Rows in the confusion matrix. The number of rows is equal to the size of `annotationSpecs` . `rows[i][j]` is the number of DataItems that have ground truth of the `annotationSpecs[i]` and are predicted as `annotationSpecs[j]` by the Model being evaluated.

For Text Extraction, when `annotationSpecs[i]` is the last element in `annotationSpecs` , i.e. the special negative AnnotationSpec, `rows[i][j]` is the number of predicted entities of `annoatationSpec[j]` that are not labeled as any of the ground truth AnnotationSpec. When annotationSpecs\[j\] is the special negative AnnotationSpec, `rows[i][j]` is the number of entities have ground truth of `annotationSpec[i]` that are not predicted as an entity by the Model. The value of the last cell, i.e. `row[i][j]` where i == j and `annotationSpec[i]` is the special negative AnnotationSpec, is always 0.

## AnnotationSpecRef

Fields

`id`

`string`

ID of the AnnotationSpec.

`display_name`

`string`

Display name of the AnnotationSpec.

## ForecastingEvaluationMetrics

Metrics for forecasting evaluation results.

Fields

`quantile_metrics[]`

`  QuantileMetricsEntry  `

The quantile metrics entries for each quantile.

`root_mean_squared_error`

`float`

Root Mean Squared Error (RMSE).

`mean_absolute_error`

`float`

Mean Absolute Error (MAE).

`mean_absolute_percentage_error`

`float`

Mean absolute percentage error. Infinity when there are zeros in the ground truth.

`r_squared`

`float`

Coefficient of determination as Pearson correlation coefficient. Undefined when ground truth or predictions are constant or near constant.

`root_mean_squared_log_error`

`float`

Root mean squared log error. Undefined when there are negative ground truth values or predictions.

`weighted_absolute_percentage_error`

`float`

Weighted Absolute Percentage Error. Does not use weights, this is just what the metric is called. Undefined if actual values sum to zero. Will be very large if actual values sum to a very small number.

`root_mean_squared_percentage_error`

`float`

Root Mean Square Percentage Error. Square root of MSPE. Undefined/imaginary when MSPE is negative.

## QuantileMetricsEntry

Entry for the Quantiles loss type optimization objective.

Fields

`quantile`

`double`

The quantile for this entry.

`scaled_pinball_loss`

`float`

The scaled pinball loss of this quantile.

`observed_quantile`

`double`

This is a custom metric that calculates the percentage of true values that were less than the predicted value for that quantile. Only populated when \[optimization\_objective\]\[google.cloud.aiplatform.publicfiles.trainingjob.definition.AutoMlForecastingInputs.optimization\_objective\] is minimize-quantile-loss and each entry corresponds to an entry in \[quantiles\]\[google.cloud.aiplatform.publicfiles.trainingjob.definition.AutoMlForecastingInputs.quantiles\] The percent value can be used to compare with the quantile value, which is the target value.

## GeneralTextGenerationEvaluationMetrics

Fields

`bleu`

`float`

BLEU (bilingual evaluation understudy) scores based on sacrebleu implementation.

`rouge_l_sum`

`float`

ROUGE-L (Longest Common Subsequence) scoring at summary level.

## ImageObjectDetectionEvaluationMetrics

Metrics for image object detection evaluation results.

Fields

`bounding_box_metrics[]`

`  BoundingBoxMetrics  `

The bounding boxes match metrics for each intersection-over-union threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 and each label confidence threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 pair.

`evaluated_bounding_box_count`

`int32`

The total number of bounding boxes (i.e. summed over all images) the ground truth used to create this evaluation had.

`bounding_box_mean_average_precision`

`float`

The single metric for bounding boxes evaluation: the `meanAveragePrecision` averaged over all `boundingBoxMetricsEntries` .

## ImageSegmentationEvaluationMetrics

Metrics for image segmentation evaluation results.

Fields

`confidence_metrics_entries[]`

`  ConfidenceMetricsEntry  `

Metrics for each confidenceThreshold in 0.00,0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 Precision-recall curve can be derived from it.

## ConfidenceMetricsEntry

Fields

`confusion_matrix`

`  ConfusionMatrix  `

Confusion matrix for the given confidence threshold.

`confidence_threshold`

`float`

Metrics are computed with an assumption that the model never returns predictions with score lower than this value.

`recall`

`float`

Recall (True Positive Rate) for the given confidence threshold.

`precision`

`float`

Precision for the given confidence threshold.

`dice_score_coefficient`

`float`

DSC or the F1 score, The harmonic mean of recall and precision.

`iou_score`

`float`

The intersection-over-union score. The measure of overlap of the annotation's category mask with ground truth category mask on the DataItem.

## PairwiseTextGenerationEvaluationMetrics

Metrics for general pairwise text generation evaluation results.

Fields

`model_win_rate`

`float`

Percentage of time the autorater decided the model had the better response.

`baseline_model_win_rate`

`float`

Percentage of time the autorater decided the baseline model had the better response.

`human_preference_model_win_rate`

`float`

Percentage of time humans decided the model had the better response.

`human_preference_baseline_model_win_rate`

`float`

Percentage of time humans decided the baseline model had the better response.

`true_positive_count`

`int64`

Number of examples where both the autorater and humans decided that the model had the better response.

`false_positive_count`

`int64`

Number of examples where the autorater chose the model, but humans preferred the baseline model.

`false_negative_count`

`int64`

Number of examples where the autorater chose the baseline model, but humans preferred the model.

`true_negative_count`

`int64`

Number of examples where both the autorater and humans decided that the model had the worse response.

`accuracy`

`float`

Fraction of cases where the autorater agreed with the human raters.

`precision`

`float`

Fraction of cases where the autorater and humans thought the model had a better response out of all cases where the autorater thought the model had a better response. True positive divided by all positive.

`recall`

`float`

Fraction of cases where the autorater and humans thought the model had a better response out of all cases where the humans thought the model had a better response.

`f1_score`

`float`

Harmonic mean of precision and recall.

`cohens_kappa`

`float`

A measurement of agreement between the autorater and human raters that takes the likelihood of random agreement into account.

## QuestionAnsweringEvaluationMetrics

Fields

`exact_match`

`float`

The rate at which the input predicted strings exactly match their references.

## RegressionEvaluationMetrics

Metrics for regression evaluation results.

Fields

`root_mean_squared_error`

`float`

Root Mean Squared Error (RMSE).

`mean_absolute_error`

`float`

Mean Absolute Error (MAE).

`mean_absolute_percentage_error`

`float`

Mean absolute percentage error. Infinity when there are zeros in the ground truth.

`r_squared`

`float`

Coefficient of determination as Pearson correlation coefficient. Undefined when ground truth or predictions are constant or near constant.

`root_mean_squared_log_error`

`float`

Root mean squared log error. Undefined when there are negative ground truth values or predictions.

## SummarizationEvaluationMetrics

Fields

`rouge_l_sum`

`float`

ROUGE-L (Longest Common Subsequence) scoring at summary level.

## TextExtractionEvaluationMetrics

Metrics for text extraction evaluation results.

Fields

`confidence_metrics[]`

`  ConfidenceMetrics  `

Metrics that have confidence thresholds. Precision-recall curve can be derived from them.

`confusion_matrix`

`  ConfusionMatrix  `

Confusion matrix of the evaluation. Only set for Models where number of AnnotationSpecs is no more than 10. Only set for ModelEvaluations, not for ModelEvaluationSlices.

## ConfidenceMetrics

Fields

`confidence_threshold`

`float`

Metrics are computed with an assumption that the Model never returns predictions with score lower than this value.

`recall`

`float`

Recall (True Positive Rate) for the given confidence threshold.

`precision`

`float`

Precision for the given confidence threshold.

`f1_score`

`float`

The harmonic mean of recall and precision.

## TextSentimentEvaluationMetrics

Model evaluation metrics for text sentiment problems.

Fields

`confusion_matrix`

`  ConfusionMatrix  `

Confusion matrix of the evaluation. Only set for ModelEvaluations, not for ModelEvaluationSlices.

`precision`

`float`

Precision.

`recall`

`float`

Recall.

`f1_score`

`float`

The harmonic mean of recall and precision.

`mean_absolute_error`

`float`

Mean absolute error. Only set for ModelEvaluations, not for ModelEvaluationSlices.

`mean_squared_error`

`float`

Mean squared error. Only set for ModelEvaluations, not for ModelEvaluationSlices.

`linear_kappa`

`float`

Linear weighted kappa. Only set for ModelEvaluations, not for ModelEvaluationSlices.

`quadratic_kappa`

`float`

Quadratic weighted kappa. Only set for ModelEvaluations, not for ModelEvaluationSlices.

## TrackMetrics

UNIMPLEMENTED. Track matching model metrics for a single track match threshold and multiple label match confidence thresholds.

Fields

`confidence_metrics[]`

`  ConfidenceMetrics  `

Metrics for each label-match `confidenceThreshold` from 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99. Precision-recall curve is derived from them.

`iou_threshold`

`float`

The intersection-over-union threshold value between bounding boxes across frames used to compute this metric entry.

`mean_tracking_average_precision`

`float`

The mean average precision over all confidence thresholds.

`mean_bounding_box_iou`

`float`

The mean bounding box iou over all confidence thresholds.

`mean_mismatch_rate`

`float`

The mean mismatch rate over all confidence thresholds.

## ConfidenceMetrics

Metrics for a single confidence threshold.

Fields

`confidence_threshold`

`float`

The confidence threshold value used to compute the metrics.

`tracking_precision`

`float`

Tracking precision.

`tracking_recall`

`float`

Tracking recall.

`bounding_box_iou`

`float`

Bounding box intersection-over-union precision. Measures how well the bounding boxes overlap between each other (e.g. complete overlap or just barely above iou\_threshold).

`mismatch_rate`

`float`

Mismatch rate, which measures the tracking consistency, i.e. correctness of instance ID continuity.

## VideoActionMetrics

The Evaluation metrics given a specific `  precision_window_length  ` .

Fields

`confidence_metrics[]`

`  ConfidenceMetrics  `

Metrics for each label-match confidence\_threshold from 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99.

`precision_window_length`

`  Duration  `

This `  VideoActionMetrics  ` is calculated based on this prediction window length. If the predicted action's timestamp is inside the time window whose center is the ground truth action's timestamp with this specific length, the prediction result is treated as a true positive.

`mean_average_precision`

`float`

The mean average precision.

## ConfidenceMetrics

Metrics for a single confidence threshold.

Fields

`confidence_threshold`

`float`

Output only. The confidence threshold value used to compute the metrics.

`recall`

`float`

Output only. Recall for the given confidence threshold.

`precision`

`float`

Output only. Precision for the given confidence threshold.

`f1_score`

`float`

Output only. The harmonic mean of recall and precision.

## VideoActionRecognitionMetrics

Model evaluation metrics for video action recognition.

Fields

`video_action_metrics[]`

`  VideoActionMetrics  `

The metric entries for precision window lengths: 1s,2s,3s.

`evaluated_action_count`

`int32`

The number of ground truth actions used to create this evaluation.

## VideoObjectTrackingMetrics

Model evaluation metrics for video object tracking problems. Evaluates prediction quality of both labeled bounding boxes and labeled tracks (i.e. series of bounding boxes sharing same label and instance ID).

Fields

`bounding_box_metrics[]`

`  BoundingBoxMetrics  `

The bounding boxes match metrics for each intersection-over-union threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 and each label confidence threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 pair.

`track_metrics[]`

`  TrackMetrics  `

UNIMPLEMENTED. The tracks match metrics for each intersection-over-union threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 and each label confidence threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 pair.

`evaluated_frame_count`

`int32`

UNIMPLEMENTED. The number of video frames used to create this evaluation.

`evaluated_bounding_box_count`

`int32`

UNIMPLEMENTED. The total number of bounding boxes (i.e. summed over all frames) the ground truth used to create this evaluation had.

`evaluated_track_count`

`int32`

UNIMPLEMENTED. The total number of tracks (i.e. as seen across all frames) the ground truth used to create this evaluation had.

`bounding_box_mean_average_precision`

`float`

The single metric for bounding boxes evaluation: the `meanAveragePrecision` averaged over all `boundingBoxMetrics` .

`track_mean_average_precision`

`float`

UNIMPLEMENTED. The single metric for tracks accuracy evaluation: the `meanAveragePrecision` averaged over all `trackMetrics` .

`track_mean_bounding_box_iou`

`float`

UNIMPLEMENTED. The single metric for tracks bounding box iou evaluation: the `meanBoundingBoxIou` averaged over all `trackMetrics` .

`track_mean_mismatch_rate`

`float`

UNIMPLEMENTED. The single metric for tracking consistency evaluation: the `meanMismatchRate` averaged over all `trackMetrics` .
