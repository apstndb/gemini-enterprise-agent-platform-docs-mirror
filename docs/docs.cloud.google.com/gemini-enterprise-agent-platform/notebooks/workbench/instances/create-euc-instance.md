---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-euc-instance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-euc-instance
title: Create a Agent Platform Workbench instance with user credential access
description: Create a Agent Platform Workbench instance with user crential-based access to {{dynamic_data.site_values.cloud_name_short}} services and APIs
data_source: docs.cloud.google.com
---

# Create an instance with user credential access

This page describes how to create a Gemini Enterprise Agent Platform Workbench instance that accesses Google Cloud services and APIs through your user credentials.

Your user credentials are the credentials associated with your Google Account. Your user credentials determine which Google Cloud services and APIs your Google Account has access to.

By default, when you run code in a Agent Platform Workbench instance, your instance can access Google Cloud services and APIs by using the credentials associated with your instance's service account. This means that your instance has the same access to Google Cloud as the service account.

This page describes how to create and configure an instance so that it has the same access to Google Cloud as your user credentials.

## Overview

Agent Platform Workbench uses a global google-managed OAuth client to manage user credential access, scoped for the Google Cloud resources in the user's project. Users must grant consent to the OAuth Client to manage their credentials for each Agent Platform Workbench instance. This is done one time per instance through a dialog that opens when you click the **Open JupyterLab** button in the Google Cloud console.

The service account used to create the Agent Platform Workbench instance is the following service agent:

`service- PROJECT_NUMBER @gcp-sa-notebooks-vm. iam. gserviceaccount. com` .

This service agent provides limited permissions for essential services such as exporting logs. Users can't specify a different service account if the end user credentials feature is enabled.

Instances with end user credentials enabled have the `notebooks-managed-euc: true` Compute Engine label and the `euc-enabled: true` metadata key attached to the VM resource to denote the feature enablement.

## Create instances with post-startup scripts

You can use post-startup scripts to perform actions after your instance starts. If you enable end-user credentials on your Agent Platform Workbench instance, credentials are not available at startup. They are available only after the instance owner first accesses the JupyterLab interface. Because of this delay, your script must poll for credential availability before running commands that require authentication. For your script to run, you must grant the instance's service account permission to read the script file from its Cloud Storage location. For security reasons, you cannot change the script location after the instance is created.

Post-startup script support for instances with end-user credentials is in private GA. For information about access to this release, see the [access request page](https://docs.google.com/forms/d/e/1FAIpQLSdzNZUFsRRbB0KaMCObGUYzIo6lK3X2tO7JZOm_DZrUhBYw5Q/viewform) .

## Limitations

Consider the following limitations when you plan your project:

  - Agent Platform Workbench uses a global google-managed OAuth client to manage user credential access. Organizations can't enact fine grain controls, access the OAuth client, or use logging to check for use of the OAuth client.

  - To protect the security of Agent Platform Workbench instances with managed user credentials, **users aren't able to** :
    
      - Use SSH to access the instance.
      - Run a [Compute Engine startup script](https://docs.cloud.google.com/compute/docs/instances/startup-scripts/linux) .
      - Access the detailed VM page.
      - Use an image that isn't created by Google.

  - Using [third party credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-third-party-instance) isn't supported because the OAuth client only supports Google-managed OAuth credentials.

## Before you begin

### Required roles

To get the permissions that you need to create a Agent Platform Workbench instance, ask your administrator to grant you the [Notebooks Runner](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.runner) ( `roles/notebooks.runner` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create a single user instance

To create a Agent Platform Workbench instance by using the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click add\_box **Create new** .

3.  In the **New instance** dialog, click **Advanced options** .

4.  In the **Create instance** dialog, in the **Details** section, provide the following information for your new instance:
    
      - **Name** : Provide a name for your new instance. The name must start with a letter followed by up to 62 lowercase letters, numbers, or hyphens (-), and cannot end with a hyphen.
      - **Region** and **Zone** : Select a region and zone for the new instance. For best network performance, select the region that is geographically closest to you. See the available [Agent Platform Workbench locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations#instances) .

5.  In the **IAM and Security** section, select **Single user** .

6.  In the **User email** field, enter the user account that you want to grant access. If the specified user is not the creator of the instance, you must grant the specified user the [Service Account User role](https://docs.cloud.google.com/iam/docs/service-account-permissions#user-role) ( `roles/iam.serviceAccountUser` ) on the instance's service account.

7.  Select **Enable managed end user credentials** .

8.  Complete the rest of the instance creation dialog, and then click **Create** .
    
    Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link in the Google Cloud console.

9.  Users must grant consent to the OAuth client to manage their credentials for each Agent Platform Workbench instance. This is done one time per instance. To grant consent, click **Open JupyterLab** and complete the dialog that appears.
    
    If you try to access the instance without granting consent, JupyterLab displays a message to authenticate by opening JupyterLab from the Google Cloud console.

10. To verify that your end user credentials are available within JupyterLab, open a Terminal in JupyterLab, and enter the following command:
    
        gcloud auth list

## Authenticate the instance with your user credentials

Agent Platform Workbench can use Application Default Credentials (ADC) to authenticate your user credentials to Google Cloud services and APIs. This section describes how to provide your user credentials to ADC if any of the limitations prevent you from enabling managed credentials.

The authentication steps depend on whether you are using a Google Account or third party credentials.

### Google Account

After you can access JupyterLab on your instance, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to your instance's name, click **Open JupyterLab** .

3.  In JupyterLab, select **File \> New \> Terminal** .

4.  In the terminal window, run the following:
    
        gcloud auth login

5.  Enter `Y` .

6.  Follow the instructions to copy a verification code and enter it into the terminal.

### Third party credentials

If you [created an instance with third party credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-third-party-instance) , then after the JupyterLab proxy is available, do the following:

1.  Open JupyterLab by using the federated JupyterLab proxy.

2.  In JupyterLab, select **File \> New \> Terminal** .

3.  Create a Workforce Identity Federation [credential file](https://docs.cloud.google.com/iam/docs/workforce-sign-in-okta) with headless sign-in.

4.  In the terminal window, run the following:
    
        gcloud auth login --cred-file="CREDENTIAL_FILE"
    
    Replace CREDENTIAL\_FILE with the path and name of the credential file that you created.

5.  Follow the instructions to authenticate through the third party authentication portal.

6.  Confirm that your credentials are accessible through your instance by using the following command:
    
        gcloud auth list
