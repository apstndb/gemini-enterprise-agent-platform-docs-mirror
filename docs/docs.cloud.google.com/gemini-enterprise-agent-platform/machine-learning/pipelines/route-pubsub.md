---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/route-pubsub
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/route-pubsub
title: Route logs to a Cloud Pub/Sub sink
description: Learn how to route your pipeline logs to a Pub/Sub sink to build an event-driven ML workflows in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

You can route pipeline logs to a Cloud Pub/Sub sink to build an event-driven architecture. You can also sync pipeline logs into your observability tools. For more information about routing logs to a Cloud Pub/Sub sink, see [View logs routed to Pub/Sub](https://docs.cloud.google.com/logging/docs/export/pubsub) .

This section describes how you can create a Pub/Sub topic, route (or sink) pipeline job logs to the Pub/Sub topic, and verify the logs published to the Pub/Sub topic. You can then subscribe downstream applications to the Pub/Sub topic to power event-driven architectures, or sync pipeline logs with your observability tools in near real-time.

Use the following instructions to set up a Pub/Sub sink and view the logs routed to it on the Google Cloud console:

1.  Create a Pub/Sub topic. For more information, see [Create a topic in the Cloud Pub/Sub documentation](https://docs.cloud.google.com/pubsub/docs/create-topic#create_a_topic) .

2.  On the **Subscriptions** page of the Google Cloud console, create a pull subscription for the Pub/Sub topic. For more information, see [Create pull subscription](https://docs.cloud.google.com/pubsub/docs/create-subscription#create_a_pull_subscription) .

3.  Select **Logging** from the navigation menu, then click **Go to Log Router** :  

4.  In your project containing the logs you want to route, click **Create Sink** .

5.  Enter a name and description for the sink, and then click **Next** .

6.  In the **Service** list, select **Cloud Pub/Sub topic** .

7.  In the **Destination** list, select the Pub/Sub topic that you created, and then click **Next** .

8.  Under **Choose logs to include in sink** , specify the following inclusion filter:
    
        resource.type="aiplatform.googleapis.com/PipelineJob"

9.  Click **Create Sink** .

10. On the **Subscriptions** page, click the subscription ID.

11. Click the subcription ID that you created.

12. On the subscription details page, click the **Messages** tab.

13. To pull and view the pipeline job logs, click **Pull** .
