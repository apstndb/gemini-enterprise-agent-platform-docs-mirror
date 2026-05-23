---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/clean-up
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/clean-up
title: 'Step 6: Clean up your project'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, either [delete the project containing the resources](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#shutting_down_projects) , or keep the project and delete the individual resources.

This section describes how to delete the Google Cloud resources and the Git repository.

## Delete the Cloud Run service

1.  In the Google Cloud console, navigate to Cloud Run.

2.  Select the checkbox next to `gemini-streamlit-cloudrun` .

3.  Click delete **Delete** .

4.  To confirm deletion, click **Delete** . This also deletes all revisions of the service.

## Delete the load balancer

1.  In the Google Cloud console, go to the **Load balancing** page.

2.  Select the checkbox next to `gemini-streamlit-app-lb` .

3.  Click delete **Delete** .

4.  Select the checkboxes next to all the additional resources, including backend services and SSL certificates.

5.  Click **Delete load balancer and the selected resources** .

## Delete the Cloud Build trigger

1.  In the Google Cloud console, navigate to the **Triggers** page.

2.  Click the menu (vertical ellipsis) located at the right end of the trigger, and then click **Delete** .

3.  To confirm deletion, click **Delete** .

## Delete the network endpoint group

1.  In the Google Cloud console, go to the **Network endpoint group** page.

2.  Select the checkbox next to `streamlit-app-neg` .

3.  Click delete **Delete** .

4.  To confirm deletion, click **Delete** .

## Delete the reserved IP address and DNS records

1.  In the Google Cloud console, go to the **External IP addresses** page.

2.  Select `genai-app-ip` .

3.  Click **Release static address** .

4.  Remove the DNS records created for the reserved IP address. You might have to contact your domain administrator to complete this step.

## Delete Git repository

Go to your Git repository and click **Settings** \> **Danger Zone** \> **Delete this repository** .
