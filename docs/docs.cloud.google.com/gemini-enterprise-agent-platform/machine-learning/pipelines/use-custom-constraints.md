---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/use-custom-constraints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/use-custom-constraints
title: Use custom constraints with pipelines
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page shows you how to use Organization Policy Service custom constraints to restrict specific operations on the following Google Cloud resources:

  - `aiplatform.googleapis.com/PipelineJob`

To learn more about Organization Policy, see [Custom organization policies](https://docs.cloud.google.com/organization-policy/overview#custom-organization-policies) .

## About organization policies and constraints

The Google Cloud Organization Policy Service gives you centralized, programmatic control over your organization's resources. As the [organization policy administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/orgpolicy#orgpolicy.policyAdmin) , you can define an organization policy, which is a set of restrictions called *constraints* that apply to Google Cloud resources and descendants of those resources in the [Google Cloud resource hierarchy](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy) . You can enforce organization policies at the organization, folder, or project level.

Organization Policy provides built-in [managed constraints](https://docs.cloud.google.com/organization-policy/reference/org-policy-constraints) for various Google Cloud services. However, if you want more granular, customizable control over the specific fields that are restricted in your organization policies, you can also create *custom constraints* and use those custom constraints in an organization policy.

### Policy inheritance

By default, organization policies are inherited by the descendants of the resources on which you enforce the policy. For example, if you enforce a policy on a folder, Google Cloud enforces the policy on all projects in the folder. To learn more about this behavior and how to change it, refer to [Hierarchy evaluation rules](https://docs.cloud.google.com/organization-policy/hierarchy-evaluation#disallow_inheritance) .

### Benefits

You can use a custom organization policy to allow or deny specific operations on Gemini Enterprise Agent Platform Pipelines resources. For example, if the template URI specified to create a `PipelineJob` resource fails to satisfy a custom constraint validation set by your organization policy, the request fails, and an error is returned to the caller.

## Limitations

Custom organization policies aren't enforced on [pipeline runs scheduled using the scheduler API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/schedule-pipeline-run) .

## Before you begin

1\. **Set up your project**

1.  [Get your organization resource ID.](https://docs.cloud.google.com/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id)
2.  [Define and compile a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline) that you can use to test the custom constraint.

### Required roles

To get the permissions that you need to manage organization policies, ask your administrator to grant you the following IAM roles:

  - To manage organization policies: [Organization Policy Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/orgpolicy#orgpolicy.policyAdmin) ( `roles/orgpolicy.policyAdmin` ) on the organization resource
  - Create or update an ML pipeline: [Agent Platform Admin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.admin) ( `roles/aiplatform.admin` ) or [Agent Platform User](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.user) ( `roles/aiplatform.user` ) on the project resource

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Gemini Enterprise Agent Platform Pipelines supported resources

The following table lists the Gemini Enterprise Agent Platform Pipelines resources that you can reference in custom constraints.

Resource

Field

aiplatform.googleapis.com/PipelineJob

`resource.displayName`

`resource.encryptionSpec.kmsKeyName`

`resource.network`

`resource.pipelineSpec`

`resource.preflightValidations`

`resource.pscInterfaceConfig.networkAttachment`

`resource.reservedIpRanges`

`resource.runtimeConfig.failurePolicy`

`resource.runtimeConfig.gcsOutputDirectory`

`resource.runtimeConfig.inputArtifacts[*].artifactId`

`resource.runtimeConfig.parameterValues[*].boolValue`

`resource.runtimeConfig.parameterValues[*].listValue.values`

`resource.runtimeConfig.parameterValues[*].nullValue`

`resource.runtimeConfig.parameterValues[*].numberValue`

`resource.runtimeConfig.parameterValues[*].stringValue`

`resource.runtimeConfig.parameterValues[*].structValue`

`resource.serviceAccount`

`resource.templateUri`

## Set up a custom constraint

A custom constraint is defined in a YAML file by the resources, methods, conditions, and actions that are supported by the service on which you are enforcing the organization policy. Conditions for your custom constraints are defined using [Common Expression Language (CEL)](https://github.com/google/cel-spec/blob/master/doc/intro.md) . For more information about how to build conditions in custom constraints using CEL, see the CEL section of [Creating and managing custom constraints](https://docs.cloud.google.com/organization-policy/create-custom-constraints#common_expression_language) .

### Console

To create a custom constraint, do the following:

In the Google Cloud console, go to the **Organization policies** page.

From the project picker, select the project that you want to set the organization policy for.

Click add **Custom constraint** .

In the **Display name** box, enter a human-readable name for the constraint. This name is used in error messages and can be used for identification and debugging. Don't use personally identifiable information (PII) or sensitive data in display names because this name could be exposed in error messages. This field can contain up to 200 characters.

In the **Constraint ID** box, enter the ID that you want for your new custom constraint. A custom constraint can only contain letters (including upper and lowercase) or numbers, for example `custom.denyPipelineTemplate` . This field can contain up to 70 characters, not counting the prefix ( `custom.` ), for example, `organizations/123456789/customConstraints/custom` . Don't include PII or sensitive data in your constraint ID, because it could be exposed in error messages.

In the **Description** box, enter a human-readable description of the constraint. This description is used as an error message when the policy is violated. Include details about why the policy violation occurred and how to resolve the policy violation. Don't include PII or sensitive data in your description, because it could be exposed in error messages. This field can contain up to 2000 characters.

In the **Resource type** box, select the name of the Google Cloud REST resource containing the object and field that you want to restrict—for example, `container.googleapis.com/NodePool` . Most resource types support up to 20 custom constraints. If you attempt to create more custom constraints, the operation fails.

This constraint can only be enforced on the REST `CREATE` method.

To see supported methods for each service, find the service in [Services that support custom constraints](https://docs.cloud.google.com/organization-policy/reference/custom-constraint-supported-services) .

To define a condition, click edit **Edit condition** .

1.  In the **Add condition** panel, create a CEL condition that refers to a supported service resource, for example, `resource.management.autoUpgrade == false` . This field can contain up to 1000 characters. For details about CEL usage, see [Common Expression Language](https://docs.cloud.google.com/resource-manager/docs/organization-policy/creating-managing-custom-constraints#common_expression_language) . For more information about the service resources you can use in your custom constraints, see [Custom constraint supported services](https://docs.cloud.google.com/resource-manager/docs/organization-policy/custom-constraint-supported-services) .
2.  Click **Save** .

Under **Action** , select whether to allow or deny the evaluated method if the condition is met.

The deny action means that the operation to create or update the resource is blocked if the condition evaluates to true.

The allow action means that the operation to create or update the resource is permitted only if the condition evaluates to true. Every other case except those explicitly listed in the condition is blocked.

Click **Create constraint** .

When you have entered a value into each field, the equivalent YAML configuration for this custom constraint appears on the right.

### gcloud

To create a custom constraint, create a YAML file using the following format:

    name: organizations/ORGANIZATION_ID/customConstraints/CONSTRAINT_NAME
    resourceTypes: RESOURCE_NAME
    methodTypes:
      - CREATE
    condition: "CONDITION"
    actionType: ACTION
    displayName: DISPLAY_NAME
    description: DESCRIPTION

Replace the following:

  - `  ORGANIZATION_ID  ` : your organization ID, such as `123456789` .
  - `  CONSTRAINT_NAME  ` : the name that you want for your new custom constraint. A custom constraint can only contain letters (including upper and lowercase) or numbers, for example, `custom.denyPipelineTemplate` . This field can contain up to 70 characters, not counting the prefix ( `custom.` )— for example, `organizations/123456789/customConstraints/custom` . Don't include PII or sensitive data in your constraint ID, because it could be exposed in error messages.
  - `  RESOURCE_NAME  ` : the fully qualified name of the Google Cloud resource containing the object and field that you want to restrict. For example, `aiplatform.googleapis.com/PipelineJob/resource.templateUri` . Most resource types support up to 20 custom constraints. If you attempt to create more custom constraints, the operation fails.
  - `methodTypes` : the REST methods that the constraint is enforced on. Can only be `CREATE` .
  - `  CONDITION  ` : a [CEL condition](https://docs.cloud.google.com/resource-manager/docs/organization-policy/creating-managing-custom-constraints#common_expression_language) that is written against a representation of a supported service resource. This field can contain up to 1000 characters. For example, `"resource.templateUri.contains("test")"` .
  - `  ACTION  ` : the action to take if the `condition` is met. Possible values are `ALLOW` and `DENY` .
  - `  DISPLAY_NAME  ` : a human-readable name for the constraint. This name is used in error messages and can be used for identification and debugging. Don't use PII or sensitive data in display names because this name could be exposed in error messages. This field can contain up to 200 characters.
  - `  DESCRIPTION  ` : a human-friendly description of the constraint to display as an error message when the policy is violated. This field can contain up to 2000 characters.

After you have created the YAML file for a new custom constraint, you must set it up to make it available for organization policies in your organization. To set up a custom constraint, use the [`gcloud org-policies set-custom-constraint`](https://docs.cloud.google.com/sdk/gcloud/reference/org-policies/set-custom-constraint) command:

    gcloud org-policies set-custom-constraint CONSTRAINT_PATH

Replace `  CONSTRAINT_PATH  ` with the full path to your custom constraint file. For example, `/home/user/customconstraint.yaml` .

After this operation is complete, your custom constraints are available as organization policies in your list of Google Cloud organization policies.

To verify that the custom constraint exists, use the [`gcloud org-policies list-custom-constraints`](https://docs.cloud.google.com/sdk/gcloud/reference/org-policies/list-custom-constraints) command:

    gcloud org-policies list-custom-constraints --organization=ORGANIZATION_ID

Replace `  ORGANIZATION_ID  ` with the ID of your organization resource.

For more information, see [Viewing organization policies](https://docs.cloud.google.com/resource-manager/docs/organization-policy/creating-managing-policies#viewing_organization_policies) .

## Enforce a custom organization policy

You can enforce a constraint by creating an organization policy that references it, and then applying that organization policy to a Google Cloud resource.

### Console

1.  In the Google Cloud console, go to the **Organization policies** page.
2.  From the project picker, select the project that you want to set the organization policy for.
3.  From the list on the **Organization policies** page, select your constraint to view the **Policy details** page for that constraint.
4.  To configure the organization policy for this resource, click **Manage policy** .
5.  On the **Edit policy** page, select **Override parent's policy** .
6.  Click **Add a rule** .
7.  In the **Enforcement** section, select whether this organization policy is enforced or not.
8.  Optional: To make the organization policy conditional on a tag, click **Add condition** . Note that if you add a conditional rule to an organization policy, you must add at least one unconditional rule or the policy cannot be saved. For more information, see [Scope organization policies with tags](https://docs.cloud.google.com/organization-policy/scope-policies) .
9.  Click **Test changes** to simulate the effect of the organization policy. For more information, see [Test organization policy changes with Policy Simulator](https://docs.cloud.google.com/policy-intelligence/docs/test-organization-policies) .
10. To enforce the organization policy in dry-run mode, click **Set dry run policy** . For more information, see [Test organization policies](https://docs.cloud.google.com/organization-policy/test-policies) .
11. After you verify that the organization policy in dry-run mode works as intended, set the live policy by clicking **Set policy** .

### gcloud

To create an organization policy with boolean rules, create a policy YAML file that references the constraint:

    name: projects/PROJECT_ID/policies/CONSTRAINT_NAME
    spec:
      rules:
      - enforce: true
    
    dryRunSpec:
      rules:
      - enforce: true

Replace the following:

  - `  PROJECT_ID  ` : the project that you want to enforce your constraint on.
  - `  CONSTRAINT_NAME  ` : the name you defined for your custom constraint. For example, `custom.denyPipelineTemplate` .

To enforce the organization policy in [dry-run mode](https://docs.cloud.google.com/organization-policy/test-policies) , run the following command with the `dryRunSpec` flag:

    gcloud org-policies set-policy POLICY_PATH --update-mask=dryRunSpec

Replace `  POLICY_PATH  ` with the full path to your organization policy YAML file. The policy requires up to 15 minutes to take effect.

After you verify that the organization policy in dry-run mode works as intended, set the live policy with the `org-policies set-policy` command and the `spec` flag:

    gcloud org-policies set-policy POLICY_PATH --update-mask=spec

Replace `  POLICY_PATH  ` with the full path to your organization policy YAML file. The policy requires up to 15 minutes to take effect.

## Test the custom organization policy

The following example creates a custom constraint and policy that don't allow pipeline runs to be created by specifying a template URI that contains "test".

Before you begin, you must know the following:

  - Your organization ID
  - A project ID

### Create the constraint

1.  Save the following file as `constraint-validate-pipeline-template-uri.yaml` :
    
        name: organizations/ORGANIZATION_ID/customConstraints/custom.denyPipelineTemplate
        resourceTypes:
        - resource.templateUri
        methodTypes:
          - CREATE
          condition: "resource.templateUri.contains("test")"
          actionType: DENY
          displayName: Deny pipeline runs if the template URI contains 'test'
          description: Deny the creation of a new pipeline run if it's based on a template URI containing 'test'
    
    This defines a constraint where the pipeline template URI can't contain `test` .
    
    1.  Apply the constraint:
        
            gcloud org-policies set-custom-constraint ~/constraint-validate-pipeline-template-uri.yaml
    
    2.  Verify that the constraint exists:
        
            gcloud org-policies list-custom-constraints --organization=ORGANIZATION_ID
        
        The output is similar to the following:
        
            CUSTOM_CONSTRAINT                          ACTION_TYPE  METHOD_TYPES   RESOURCE_TYPES          DISPLAY_NAME
            custom.denyPipelineTemplate                DENY         CREATE         resource.templateUri    Deny pipeline runs if the template URI contains 'test'
            ...

### Create the policy

1.  Save the following file as `policy-validate-pipeline-template-uri.yaml` :
    
    ``` 
      name: projects/PROJECT_ID/policies/custom.denyPipelineTemplate
      spec:
        rules:
        - enforce: true
    ```
    
    Replace `  PROJECT_ID  ` with your project ID.

2.  Apply the policy:
    
    ``` 
      gcloud org-policies set-policy ~/policy-validate-pipeline-template-uri.yaml
    ```

3.  Verify that the policy exists:
    
    ``` 
      gcloud org-policies list --project=PROJECT_ID
    ```
    
    The output is similar to the following:
    
    ``` 
      CONSTRAINT                    LIST_POLICY    BOOLEAN_POLICY    ETAG
      custom.denyPipelineTemplate   -              SET               COCsm5QGENiXi2E=
    ```
    
    After you apply the policy, wait for about two minutes for Google Cloud to start enforcing the policy.

### Test the policy

Try to create an ML pipeline with the template URI containing `test` .

### REST

To create a [`PipelineJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs#PipelineJob) resource, send a `POST` request by using the [`pipelineJobs/create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where you want to create the pipeline run. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform Pipelines locations guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project where you want to create the pipeline run.
  - DISPLAY\_NAME : The name of the pipeline run. This will be displayed in the Google Cloud console.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs

Request JSON body:

    {
      "displayName":"DISPLAY_NAME",
      "templateUri":"test_pipeline_template.json"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "error": {
        "code": 400,
        "message": "Operation denied by org policy on resource 'projects/PROJECT_ID/locations/LOCATION': [\"customConstraints/custom.denyPipelineTemplate\": \"Deny the creation of a new pipeline run if it's based on a template URI containing 'test'\"]",
        "status": "FAILED_PRECONDITION",
        "details": [
          {
            "@type": "type.googleapis.com/google.rpc.ErrorInfo",
            "reason": "CUSTOM_ORG_POLICY_VIOLATION",
            "domain": "googleapis.com",
            "metadata": {
              "service": "aiplatform.googleapis.com",
              "customConstraints": "customConstraints/custom.denyPipelineTemplate"
            }
          }
        ]
      }
    }

## What's next

  - Learn more about [Organization Policy Service](https://docs.cloud.google.com/organization-policy/overview) .
  - Learn more about how to [create and manage organization policies](https://docs.cloud.google.com/organization-policy/create-organization-policies) .
  - See the full list of managed [organization policy constraints](https://docs.cloud.google.com/organization-policy/reference/org-policy-constraints) .
