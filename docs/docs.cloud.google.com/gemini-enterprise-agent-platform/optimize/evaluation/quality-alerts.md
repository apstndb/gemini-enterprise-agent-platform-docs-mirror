---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/quality-alerts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/quality-alerts
title: Configure quality alerts
description: Learn how to configure quality alerts to proactively detect quality drift in your production agents.
data_source: docs.cloud.google.com
---

Quality alerts notify you when your agent's performance drops below a defined threshold. You can use these alerts to detect **quality drift** —an observable decrease in agent performance over time. This decrease can occur even if the underlying model remains the same, often driven by changes in real-world user behavior, evolving data patterns, or subtle interactions in complex prompt chains.

> **Why use quality alerts?**
> 
>   - **Automatic Detection:** Identify performance drops without manual spot-checks.
>   - **Proactive Response:** Get notified using Slack, email, or Pub/Sub.
>   - **Traceability:** Link alerting policies directly back to the specific traces that caused the drift.

When you configure an **Online Monitor** , the system automatically exports numeric evaluation scores to Cloud Monitoring. These metrics trigger **incidents** in Cloud Monitoring. You can then create **alerting policies** to notify your team when quality issues arise.

You can create targeted alerting policies for a specific monitor:

1.  In the Google Cloud console, navigate to the **Agent Platform \> Agents** page.

2.  In the left navigation menu, select **Evaluation** .

3.  Select the **Online monitors** tab. Click **More options** *more\_vert* for a monitor and select **Create alerting policy** .

4.  Review the **Alerting policy templates** available for that monitor.

5.  Select the templates you want to enable. The system provides one template per metric configured on the monitor.

6.  **Configure Notifications:** Select your **Notification Channels** . If you uncheck **Use notification channels** , the system performs checks but does not proactively notify users. You can still view triggered incidents on the **Monitoring \> Alerting** page.

7.  Click **Create** .

## Create recommended alerts from the dashboard

The Evaluation Dashboard provides a shortcut to enable broad quality guardrails for all active monitors:

1.  In the Google Cloud console, navigate to the **Agent Platform \> Agents** page.

2.  In the left navigation menu, select **Deployments** and select your agent.

3.  Select the **Dashboard** tab and select the **Evaluation** subsection.

4.  Click the **Recommended Alerts** button in the top right corner.

5.  Review the available templates, such as:
    
      - **Online Monitor - Low evaluation score:** Triggers if the aggregate score for a monitor falls too low.
      - **Individual Metric Alerts:** Specific thresholds for metrics like **Task Success** or **Tool Use Quality** .

6.  Select the templates and notification channels, then click **Create** .

## Programmatic alert creation

For large-scale deployments, you can configure quality alerts using the `gcloud` CLI or the Cloud Monitoring API.

### Using gcloud

Create an alert policy from a JSON or YAML configuration file:

    gcloud monitoring policies create --policy-from-file="policy.yaml"

The following is an example `policy.yaml` that triggers if the average **Task Success** score falls below 80% over a 30-minute window:

    displayName: "Low Task Success Score"
    conditions:
    - displayName: "Task Success < 0.8"
      conditionThreshold:
        filter: >
          metric.type="aiplatform.googleapis.com/online_evaluator/scores"
          AND metric.labels.evaluation_metric_name="task_success"
        comparison: COMPARISON_LT
        thresholdValue: 0.8
        duration: 1800s
        aggregations:
        - alignmentPeriod: 60s
          perSeriesAligner: ALIGN_MEAN
    combiner: OR
    enabled: true
    notificationChannels:
    - "projects/YOUR_PROJECT_ID/notificationChannels/CHANNEL_ID"

### Using the Agent Platform SDK

    from google.cloud import monitoring_v3
    
    client = monitoring_v3.AlertPolicyServiceClient()
    project_name = f"projects/YOUR_PROJECT_ID"
    
    policy = {
        "display_name": "Agent Quality Drift",
        "conditions": [{
            "display_name": "Low Evaluation Score",
            "condition_threshold": {
                "filter": (
                    'metric.type="aiplatform.googleapis.com/online_evaluator/scores"'
                ),
                "comparison": monitoring_v3.ComparisonType.COMPARISON_LT,
                "threshold_value": 0.7,
                "duration": {"seconds": 3600},
                "aggregations": [{
                    "alignment_period": {"seconds": 60},
                    "per_series_aligner": monitoring_v3.Aggregation.Aligner.ALIGN_MEAN,
                }],
            },
        }],
        "combiner": monitoring_v3.AlertPolicy.ConditionCombinerType.OR,
        "enabled": True,
    }
    
    response = client.create_alert_policy(name=project_name, alert_policy=policy)
    print(f"Created alerting policy {response.name}")

## Manage alerting policies

Use the **Cloud Monitoring** console to view where your alerting policies are located and refine their configurations. Each incident includes labels for the associated Online Monitor to help you investigate the root cause.
