---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment
title: Install the CLI and configure credentials
description: Learn how to download the CodeMender CLI, configure Google Cloud credentials, and initialize your workspace.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

CodeMender is an autonomous AI code security agent that scans, verifies, and patches deep cybersecurity vulnerabilities in your codebase. Before running CodeMender, download the CLI and initialize workspace options.

## Architecture and security model

CodeMender uses a **local-first execution model** :

  - **Hosted reasoning engine** : Agentic reasoning, threat modeling, and orchestration logic run securely in Google Cloud on Gemini Enterprise Agent Platform.
  - **Local execution CLI** : Source code never leaves your workstation or CI/CD container in bulk. Local `cm` CLI tool executes file reads, local build checks, and proof-of-concept (PoC) exploit verifications in your local sandbox, sending only surgical code snippets and tool execution results to the cloud backend over the Interactions API on Gemini Enterprise Agent Platform.

## Environment setup

To begin using CodeMender, download and install the CLI, configure your Google Cloud credentials, and initialize your workspace.

### Download and install CodeMender CLI

The CodeMender CLI binaries are hosted in Artifact Registry. Choose the tab for your operating system to download and install the CLI.

> **Note:** CodeMender is currently available to a limited set of customers in Public Preview. Contact your sales team to get access.

### Linux x86\_64

To download and install CodeMender CLI for Linux (x86\_64):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command:
        
            gcloud artifacts generic download \
              --project=cmoc-prod \
              --location=us \
              --repository=codemender-cli-production \
              --package=cm \
              --version=stable \
              --name=cm-linux-amd64.zip \
              --destination=./
    
      - **curl:** Run the following command:
        
            curl -L -o cm-linux-amd64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-linux-amd64.zip:download?alt=media"

2.  Install the CLI:
    
        unzip cm-linux-amd64.zip
        chmod +x cm
        sudo mv cm /usr/local/bin/cm

### Linux ARM64

To download and install CodeMender CLI for Linux (ARM64):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command:
        
            gcloud artifacts generic download \
              --project=cmoc-prod \
              --location=us \
              --repository=codemender-cli-production \
              --package=cm \
              --version=stable \
              --name=cm-linux-arm64.zip \
              --destination=./
    
      - **curl:** Run the following command:
        
            curl -L -o cm-linux-arm64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-linux-arm64.zip:download?alt=media"

2.  Install the CLI:
    
        unzip cm-linux-arm64.zip
        chmod +x cm
        sudo mv cm /usr/local/bin/cm

### macOS Intel

To download and install CodeMender CLI for macOS (Intel):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command:
        
            gcloud artifacts generic download \
              --project=cmoc-prod \
              --location=us \
              --repository=codemender-cli-production \
              --package=cm \
              --version=stable \
              --name=cm-darwin-amd64.zip \
              --destination=./
    
      - **curl:** Run the following command:
        
            curl -L -o cm-darwin-amd64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-darwin-amd64.zip:download?alt=media"

2.  Install the CLI:
    
        unzip cm-darwin-amd64.zip
        chmod +x cm
        mv cm /usr/local/bin/cm

### macOS Apple silicon

To download and install CodeMender CLI for macOS (Apple silicon):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command:
        
            gcloud artifacts generic download \
              --project=cmoc-prod \
              --location=us \
              --repository=codemender-cli-production \
              --package=cm \
              --version=stable \
              --name=cm-darwin-arm64.zip \
              --destination=./
    
      - **curl:** Run the following command:
        
            curl -L -o cm-darwin-arm64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-darwin-arm64.zip:download?alt=media"

2.  Install the CLI:
    
        unzip cm-darwin-arm64.zip
        chmod +x cm
        mv cm /usr/local/bin/cm

### Windows x86\_64

To download and install CodeMender CLI for Windows (x86\_64):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command in PowerShell:
        
            gcloud artifacts generic download `
              --project=cmoc-prod `
              --location=us `
              --repository=codemender-cli-production `
              --package=cm `
              --version=stable `
              --name=cm-windows-amd64.zip `
              --destination=./
    
      - **PowerShell:** Run the following command:
        
            Invoke-WebRequest -Uri "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-windows-amd64.zip:download?alt=media" -OutFile cm-windows-amd64.zip

2.  Install the CLI:
    
        Expand-Archive -Path cm-windows-amd64.zip -DestinationPath ./
        # Move cm.exe to a permanent folder and add it to your system PATH (e.g. Environmental Variables)

### Windows ARM64

To download and install CodeMender CLI for Windows (ARM64):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command in PowerShell:
        
            gcloud artifacts generic download `
              --project=cmoc-prod `
              --location=us `
              --repository=codemender-cli-production `
              --package=cm `
              --version=stable `
              --name=cm-windows-arm64.zip `
              --destination=./
    
      - **PowerShell:** Run the following command:
        
            Invoke-WebRequest -Uri "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-windows-arm64.zip:download?alt=media" -OutFile cm-windows-arm64.zip

2.  Install the CLI:
    
        Expand-Archive -Path cm-windows-arm64.zip -DestinationPath ./
        # Move cm.exe to a permanent folder and add it to your system PATH (e.g. Environmental Variables)

### Configure Google Cloud credentials

Because the CodeMender CLI interacts with the cloud-hosted reasoning engine over the Interactions API, you must configure Google Cloud Application Default Credentials (ADC) in your environment.

To authenticate, run the following command and follow the login prompts:

    gcloud auth application-default login

## Initialize and configure CodeMender

Once you have authenticated, your next step should be to initialize CodeMender in your local environment. Initializing CodeMender prepares your local workspace by creating state-tracking files and establishing connection settings to the cloud-hosted reasoning engine.

### Initialize the workspace

Run `cm init` from the root directory of your codebase to create local state tracking files and establish baseline configurations:

    cm init

Use the --verify flag to test connectivity to the cloud-hosted reasoning engine and verify workspace settings:

    cm init --verify

> **Note:** If you encounter the message `Resource setup has just started. Please try again shortly.` , initial resource provisioning is underway and typically completes within a few minutes.

### Configuration parameters ( `config.yaml` )

CodeMender reads configuration settings from `~/.codemender/config.yaml` . You can customize the following sections:

#### Version control system (VCS) configuration

Specify your project's version control system type under `vcs` . CodeMender supports Git, Mercurial, or custom VCS configurations:

### Git repositories

    vcs:
      type: "git"

### Mercurial repositories

    vcs:
      type: "mercurial"

### Custom version control systems

Specify custom command mappings for non-standard VCS tools:

    vcs:
      type: "custom"
      commands:
        status: "svn status"
        diff:   "svn diff"
        stage:  "echo 'no staging needed'"
        reset:  "svn revert -R ."

#### Build and regression testing command

Define the exact shell command that CodeMender uses to build your project and execute unit and regression tests:

    build:
      command: "make build && make test"

#### Interactive execution confirmations

Configure tool confirmation behavior to determine whether the CLI prompts for confirmation before running local commands or modifying files:

    tools:
      confirm_execution: true
