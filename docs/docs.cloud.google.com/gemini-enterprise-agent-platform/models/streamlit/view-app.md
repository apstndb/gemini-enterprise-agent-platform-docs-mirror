---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/view-app
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/view-app
title: 'Step 5: Test your IAP-secured app'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In this section, you test the app that you've deployed to Cloud Run by viewing it in your browser. You can view the app only after the status of the Google-managed certificate becomes `ACTIVE` . Provisioning a Google-managed certificate might take up to 60 minutes. For more information about Google-managed SSL certificates, see [Use Google-managed SSL certificates](https://docs.cloud.google.com/load-balancing/docs/ssl-certificates/google-managed-certs#certificate-resource-status) .

## Check the status of your certificate

1.  Go to the **Classic Certificates** tab in the Google Cloud console.

2.  In the **Status** column, check the status of the `my-genai-app-certificate` certificate.
    
    You can proceed with the rest of the tutorial after the status changes to **Active** . Note that certificate provisioning might take up to 60 minutes.

## View the deployed app

1.  Sign in with a principal's account that you configured in IAP.

2.  In your browser, open the following URL:
    
        https://DOMAIN_NAME/app
    
    Replace DOMAIN\_NAME with domain name provided during certificate creation.
