---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/save-to-github
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/save-to-github
title: Save a notebook to GitHub
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page describes how you can save your Agent Platform Workbench instance's notebook files to GitHub by using the `jupyterlab-git` extension. You might do this to create a backup of the notebook or to make the notebook available to others.

In Agent Platform Workbench instances, you can use the `jupyterlab-git` extension to help you with version control. To learn more, see [`jupyterlab-git`](https://github.com/jupyterlab/jupyterlab-git/blob/main/README.md) on GitHub.

## Create a GitHub repository

If you don't already have a [GitHub](https://github.com/) repository, you must create one.

When you create your GitHub repository make sure that your GitHub repository can be cloned by selecting the **Initialize this repository with a README** checkbox.

![Initialize a GitHub repository with a README file.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/instances/images/github-01.png)

## Clone your GitHub repository in your Agent Platform Workbench instance

To clone your GitHub repository in your Agent Platform Workbench instance, complete the following steps:

1.  In your GitHub repository, click the **Code** button, and then click the **Local** tab.

2.  Copy the **HTTPS** URL.

3.  In the Google Cloud console, go to the **Instances** page.

4.  Click **Open JupyterLab** to open your Agent Platform Workbench instance.

5.  In the JupyterLab folder **File Browser** , select the folder where you want to clone the GitHub repository. For example, the home folder.
    
    ![The JupyterLab file browser in Gemini Enterprise Agent Platform Workbench, highlighting the home folder where a GitHub repository can be cloned.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/instances/images/github-04.png)

6.  In JupyterLab, select **Git \> Clone a Repository** .

7.  In the **Clone a repo** dialog, paste the HTTPS URL for your GitHub repository.
    
    ![Dialog showing the field for the repository URL and options for submodules and download repository.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/instances/images/github-06.png)

8.  If prompted, enter your credentials.
    
      - If you use a GitHub username and password, enter your GitHub username and password.
    
      - If you use two-factor authentication with GitHub, create and use a [personal access token](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line) .

9.  Click **Clone** .

10. Your Agent Platform Workbench instance shows your repository as a new folder. If you don't see your cloned GitHub repository as a folder, click the **Refresh File List** button.
    
    ![The JupyterLab file browser in Gemini Enterprise Agent Platform Workbench, with the Refresh File List button highlighted.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/instances/images/github-09.png)

## Configure your instance with your GitHub user information

1.  In JupyterLab, open the folder where your repository is located.

2.  Select **Git \> Open Git Repository in Terminal** to open a Git terminal window.

3.  In the Git terminal window, enter the following commands to configure your Git username and email:
    
        git config --global user.name "USERNAME"
        git config --global user.email "EMAIL_ADDRESS"
    
    Replace the following:
    
      - `  USERNAME  ` : your GitHub username
      - `  EMAIL_ADDRESS  ` : your GitHub account email address

4.  If your GitHub account requires SSH authentication, complete the following steps to connect your account:
    
    1.  From your Git terminal in your Agent Platform Workbench instance, follow GitHub's [instructions for generating a new SSH key](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) .
    
    2.  Follow the [instructions for adding that SSH key to your GitHub account](https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account) .

5.  Close the Git terminal window.

## Add your committed files to your GitHub repository

1.  In JupyterLab, open the folder where your repository is located.

2.  [Add a new notebook](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart#open-a-new-notebook-file) .

3.  Select the **Git** tab. Your new notebook is listed in the **Untracked** grouping.

4.  To add the new notebook as a file for your GitHub repository, right-click the new notebook and select **Track** . On the **Git** tab, your notebook is now added to the **Staged** grouping.

5.  To commit your new notebook to your GitHub repository, on the **Git** tab, in the **Summary** field, add a commit comment, and then click **Commit** .

6.  Select **Git \> Push to Remote** .
    
      - If you use a GitHub username and password, when prompted, enter your GitHub username and password.
    
      - If you use two-factor authentication with GitHub, enter your GitHub username and personal access token.
    
    After the `git push` command completes, your committed files are in your GitHub repository.

## What's next

  - [Use Cloud Storage to back up and restore files](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/restore-cloud-storage)

  - [Use a snapshot to back up and restore data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/restore-snapshot)
