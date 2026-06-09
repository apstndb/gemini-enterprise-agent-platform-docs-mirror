---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/manage-model-monitors
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/manage-model-monitors
title: Manage model monitor
description: Describes how to update and delete model monitors.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page describes how to update and delete model monitors.

## Update a model monitor

Update a model monitor to modify the default configuration for monitoring jobs. You can't change the model version that a model monitor is associated with. Instead, create a new model monitor.

### Console

1.  In the Google Cloud console, go to the **Monitoring** page.

2.  Click the model monitor to go to the **Monitor details** page.

3.  Click **Edit configuration** to update the model monitor.

4.  Modify your schema, notifications, training data source, and objectives.

5.  Click **Save** .

### Python SDK

You can update the following specifications:

  - Display name
  - Training dataset
  - Model schema
  - Default monitoring objectives
  - Default monitoring output specification
  - Default monitoring notification specification
  - Default explanation specification for feature attribution

The following example updates the model schema:

    monitor_2.update(model_monitoring_schema=MODEL_MONITORING_SCHEMA)

## Delete a model monitor

Remove model monitors to prevent authorized users from inadvertently running monitoring jobs on unused model monitors. When you delete a model monitor, any associated monitoring data is deleted except for metrics and statistics exported by Monitoring, which remain in Cloud Monitoring and in your Cloud Storage.

### Console

1.  In the Google Cloud console, go to the **Monitoring** page.

2.  Click the model monitor to go to the **Monitor details** page.

3.  Click **Edit configuration** to update the model monitor.

### Python SDK

    from google.cloud.aiplatform.private_preview.centralized_model_monitoring
    import model_monitor
    
    my_model_monitor.delete(force=true)
