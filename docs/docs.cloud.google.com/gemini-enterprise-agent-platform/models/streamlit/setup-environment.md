---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/setup-environment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/streamlit/setup-environment
title: 'Step 1: Set up your project and source repository'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In this step, you set up your Google Cloud project and Python environment in Cloud Shell, enable the required APIs, and assign the Identity and Access Management (IAM) roles that you need to complete the tutorial. You also set up a GitHub repository containing the app source files by forking and cloning the [`GoogleCloudPlatform/generative-ai`](https://github.com/GoogleCloudPlatform/generative-ai) repository. After completing these steps, you verify the setup by running and testing the app locally in Cloud Shell.

## Before you begin

## Set up the source repository

1.  In GitHub, fork the [GoogleCloudPlatform/generative-ai](https://github.com/GoogleCloudPlatform/generative-ai) repository. [Learn more about forking repositories in GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) .

<!-- end list -->

2.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](https://docs.cloud.google.com/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

3.  In the Cloud Shell terminal, run the following commands to clone the forked repository and set the `gemini-streamlit-cloudrun` directory as the active directory:  
    
        cd
        git clone https://github.com/GIT_USER_NAME/FORK_NAME/
        cd FORK_NAME/gemini/sample-apps/gemini-streamlit-cloudrun
    
    Replace the following:
    
      - GIT\_USER\_NAME : Your GitHub username.
      - FORK\_NAME : The name of the fork repository that you just created in GitHub.

## Set up the environment and dependencies

1.  In the Cloud Shell terminal, run the following commands to set up a virtual environment:
    
        python3 -m venv gemini-streamlit
        source gemini-streamlit/bin/activate
        pip install -r requirements.txt

2.  Run the following commands to set the environment variables needed for Agent Platform initialization:
    
        export GCP_PROJECT=$GOOGLE_CLOUD_PROJECT
        export GCP_REGION='us-central1' 

## Test the app locally

1.  From the Cloud Shell terminal, run the app by running the following command:
    
        streamlit run app.py \
          --browser.serverAddress=localhost \
          --server.enableCORS=false \
          --server.enableXsrfProtection=false \
          --server.port 8080

2.  To preview the app, in the Cloud Shell taskbar, click ![Web Preview Button](https://docs.cloud.google.com/static/shell/docs/images/web_preview.svg) , and then click **Preview on port 8080** .
    
    For more information about using the Web Preview feature, see [Preview web apps](https://docs.cloud.google.com/shell/docs/using-web-preview) .
