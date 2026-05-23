---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/configure-iap
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/configure-iap
title: 'Step 4: Configure Identity-Aware Proxy (IAP)'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In this step, you configure Identity-Aware Proxy (IAP) to provision a centralized authorization layer for the app deployed in Cloud Run, by doing the following:

1.  **Configure the OAuth consent screen:** The OAuth consent screen is a prompt that includes a summary of your project, its policies, and the requested authorization scopes of access. By configuring the OAuth consent screen for your app, you define what is available to users and app reviewers, and also register your app so you can publish it later. To learn more about the OAuth consent screen, see [Configure the OAuth consent screen and choose scopes](https://developers.google.com/workspace/guides/configure-oauth-consent) .

2.  **Create OAuth access credentials:** You need to create an OAuth client ID for your app and domain, so your app can call the required APIs. To learn more about OAuth credentials, see [Create access credentials](https://developers.google.com/workspace/guides/create-credentials) .

3.  **Enable IAP on the load balancer** : Use the OAuth client ID and secret to enable IAP on the load balancer that you created for your app.

4.  **Turn on IAP** : Secure your app by creating principals who can access your app and then turning on IAP.

## Configure the OAuth consent screen

1.  In the Google Cloud console, go to the **OAuth consent screen** .

2.  Select one of the following user types for your app:
    
      - **External** : Any user with a Google Account can make authorization requests. For the purpose of completing this tutorial, we recommend selecting **External** .
    
      - **Internal** : Only members of your Google Cloud organization can make authorization requests to the app.

3.  Click **Create** .

4.  In the **Authorized domains** section, **Add domain** , and specify the domain name used during certificate creation.

5.  In the **Developer contact information** section, enter your email address.

6.  Click **Save and Continue** .

7.  On the **Scopes** page, click **Save and Continue** .

8.  Optional: If you selected **External** as the user type, add test users on the **Test users** page, as follows:
    
    1.  Click **Add users** .
    
    2.  Enter your email address and any other authorized test users, and then click **Save and continue** .

9.  Review your app registration summary. To make changes, click **Edit** . If the app registration looks OK, click **Back to dashboard** .

## Create OAuth access credentials

1.  In the Google Cloud console, go to the **Credentials** .

2.  Click **Create credentials** and then click **OAuth client ID** .

3.  In the **Application type** list, click **Web application** .

4.  In the **Name** field, enter `gemini-streamlit-app` .

5.  In the **Authorized JavaScript origins** section, click **Add URI** and then enter the following URI:
    
        https://DOMAIN_NAME
    
    Replace DOMAIN\_NAME with the domain name used during certificate creation.

6.  Click **Create** .
    
    The **Oauth client created** screen appears, displaying the **Client ID** and **Client secret** .

7.  Copy the **Client ID** and **Client secret** . You'll need details in the next step of the tutorial.

## Enable IAP on the load balancer

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](https://docs.cloud.google.com/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  In the Cloud Shell terminal, run the following command:  
    
    ``` 
          gcloud compute backend-services update gemini-streamlit-app-backend \
          --iap=enabled,oauth2-client-id=CLIENT_ID,oauth2-client-secret=CLIENT_SECRET \
          --global
          
    ```
    
    Replace the following
    
      - CLIENT\_ID : The OAuth client ID from the OAuth credentials that you just created.
      - CLIENT\_SECRET : The OAuth client secret from the OAuth credentials that you just created.

## Set up and use IAP

> **Caution:** When IAP is turned off, a resource is accessible to anyone with the URL. Ensure that IAP is turned on, so that the resource is accessible only by the configured principals.

1.  Go to the **Identity-Aware Proxy** page.

2.  Select your project.

3.  Select the checkbox next to `gemini-streamlit-app-backend` .

4.  Click **Add principal** .

5.  Enter the details in the following fields:
    
      - **New principals** : Enter the email addresses of groups or individuals to grant them access to your app. Any of the following can be a principal:
        
          - Google Account
        
          - Google Group
        
          - Service account
        
          - Google Workspace domain
        
        Ensure that you include a Google Account that you have access to.

6.  In the **Role** list, select **Cloud IAP** \> **IAP-secured Web App User** .

7.  Click **Save** .

8.  On the **Identity-Aware Proxy** page, under **Applications** , click the **IAP** toggle to the on position in the row corresponding to the `gemini-streamlit-app-backend` resource.

9.  In the **Turn on IAP** window that appears, select the checkbox to acknowledge that you've read the configuration requirements and configured your backend accordingly.

10. Click **Turn on** . After you turn on IAP, it requires login credentials for all connections to your load balancer. Only accounts with the **IAP-Secured Web App User** role on the project are granted given access.
