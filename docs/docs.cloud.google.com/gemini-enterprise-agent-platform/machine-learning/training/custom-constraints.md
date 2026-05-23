---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-constraints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-constraints
title: Create custom organization policy constraints
description: Describes how to use custom constraints to control access to resources in Gemini Enterprise Agent Platform training.
data_source: docs.cloud.google.com
---

This page shows you how to use Organization Policy Service custom constraints to restrict specific operations on the following Google Cloud resources:

  - `aiplatform.googleapis.com/CustomJob`
  - `aiplatform.googleapis.com/HyperparameterTuningJob`
  - `aiplatform.googleapis.com/NasJob`

To learn more about Organization Policy, see [Custom organization policies](https://docs.cloud.google.com/organization-policy/overview#custom-organization-policies) .

## About organization policies and constraints

The Google Cloud Organization Policy Service gives you centralized, programmatic control over your organization's resources. As the [organization policy administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/orgpolicy#orgpolicy.policyAdmin) , you can define an organization policy, which is a set of restrictions called *constraints* that apply to Google Cloud resources and descendants of those resources in the [Google Cloud resource hierarchy](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy) . You can enforce organization policies at the organization, folder, or project level.

Organization Policy provides built-in [managed constraints](https://docs.cloud.google.com/organization-policy/reference/org-policy-constraints) for various Google Cloud services. However, if you want more granular, customizable control over the specific fields that are restricted in your organization policies, you can also create *custom constraints* and use those custom constraints in an organization policy.

### Policy inheritance

By default, organization policies are inherited by the descendants of the resources on which you enforce the policy. For example, if you enforce a policy on a folder, Google Cloud enforces the policy on all projects in the folder. To learn more about this behavior and how to change it, refer to [Hierarchy evaluation rules](https://docs.cloud.google.com/organization-policy/hierarchy-evaluation#disallow_inheritance) .

### Benefits

You can use custom organization policies to allow or deny specific values for Agent Platform training resources. For example, if a request to create a Gemini Enterprise Agent Platform serverless training job fails to satisfy custom constraint validation as set by your organization policy, the request fails and an error is returned to the caller.

## Limitations

Like all organization policy constraints, policy changes don't apply retroactively to existing resources.

  - A new policy doesn't impact existing resource configurations.
  - An existing resource configuration remains valid, unless you change a value in its configuration from a compliant to a non-compliant value.

## Before you begin

1.  Ensure that you know your [organization ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id) .

### Required roles

To get the permissions that you need to manage custom organization policies, ask your administrator to grant you the Organization Policy Administrator (\`roles/orgpolicy.policyAdmin\`) IAM role on the organization resource. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Gemini Enterprise Agent Platform supported resources

The following table lists the Gemini Enterprise Agent Platform resources that you can reference in custom constraints.

Resource

Field

aiplatform.googleapis.com/CustomJob

`resource.displayName`

`resource.encryptionSpec.kmsKeyName`

`resource.jobSpec.baseOutputDirectory.outputUriPrefix`

`resource.jobSpec.enableDashboardAccess`

`resource.jobSpec.enableWebAccess`

`resource.jobSpec.experiment`

`resource.jobSpec.experimentRun`

`resource.jobSpec.models`

`resource.jobSpec.network`

`resource.jobSpec.persistentResourceId`

`resource.jobSpec.protectedArtifactLocationId`

`resource.jobSpec.pscInterfaceConfig.networkAttachment`

`resource.jobSpec.reservedIpRanges`

`resource.jobSpec.scheduling.disableRetries`

`resource.jobSpec.scheduling.maxWaitDuration`

`resource.jobSpec.scheduling.restartJobOnWorkerRestart`

`resource.jobSpec.scheduling.strategy`

`resource.jobSpec.scheduling.timeout`

`resource.jobSpec.serviceAccount`

`resource.jobSpec.tensorboard`

`resource.jobSpec.workerPoolSpecs.containerSpec.args`

`resource.jobSpec.workerPoolSpecs.containerSpec.command`

`resource.jobSpec.workerPoolSpecs.containerSpec.imageUri`

`resource.jobSpec.workerPoolSpecs.diskSpec.bootDiskSizeGb`

`resource.jobSpec.workerPoolSpecs.diskSpec.bootDiskType`

`resource.jobSpec.workerPoolSpecs.machineSpec.acceleratorCount`

`resource.jobSpec.workerPoolSpecs.machineSpec.acceleratorType`

`resource.jobSpec.workerPoolSpecs.machineSpec.machineType`

`resource.jobSpec.workerPoolSpecs.machineSpec.reservationAffinity.key`

`resource.jobSpec.workerPoolSpecs.machineSpec.reservationAffinity.reservationAffinityType`

`resource.jobSpec.workerPoolSpecs.machineSpec.reservationAffinity.values`

`resource.jobSpec.workerPoolSpecs.machineSpec.tpuTopology`

`resource.jobSpec.workerPoolSpecs.nfsMounts.mountPoint`

`resource.jobSpec.workerPoolSpecs.nfsMounts.path`

`resource.jobSpec.workerPoolSpecs.nfsMounts.server`

`resource.jobSpec.workerPoolSpecs.pythonPackageSpec.args`

`resource.jobSpec.workerPoolSpecs.pythonPackageSpec.executorImageUri`

`resource.jobSpec.workerPoolSpecs.pythonPackageSpec.packageUris`

`resource.jobSpec.workerPoolSpecs.pythonPackageSpec.pythonModule`

`resource.jobSpec.workerPoolSpecs.replicaCount`

aiplatform.googleapis.com/HyperparameterTuningJob

`resource.displayName`

`resource.encryptionSpec.kmsKeyName`

`resource.maxFailedTrialCount`

`resource.maxTrialCount`

`resource.parallelTrialCount`

`resource.studySpec.algorithm`

`resource.studySpec.convexAutomatedStoppingSpec.learningRateParameterName`

`resource.studySpec.convexAutomatedStoppingSpec.maxStepCount`

`resource.studySpec.convexAutomatedStoppingSpec.minMeasurementCount`

`resource.studySpec.convexAutomatedStoppingSpec.minStepCount`

`resource.studySpec.convexAutomatedStoppingSpec.updateAllStoppedTrials`

`resource.studySpec.convexAutomatedStoppingSpec.useElapsedDuration`

`resource.studySpec.decayCurveStoppingSpec.useElapsedDuration`

`resource.studySpec.measurementSelectionType`

`resource.studySpec.medianAutomatedStoppingSpec.useElapsedDuration`

`resource.studySpec.metrics.goal`

`resource.studySpec.metrics.metricId`

`resource.studySpec.metrics.safetyConfig.desiredMinSafeTrialsFraction`

`resource.studySpec.metrics.safetyConfig.safetyThreshold`

`resource.studySpec.observationNoise`

`resource.studySpec.parameters.categoricalValueSpec.defaultValue`

`resource.studySpec.parameters.categoricalValueSpec.values`

`resource.studySpec.parameters.conditionalParameterSpecs.parentCategoricalValues.values`

`resource.studySpec.parameters.conditionalParameterSpecs.parentDiscreteValues.values`

`resource.studySpec.parameters.conditionalParameterSpecs.parentIntValues.values`

`resource.studySpec.parameters.discreteValueSpec.defaultValue`

`resource.studySpec.parameters.discreteValueSpec.values`

`resource.studySpec.parameters.doubleValueSpec.defaultValue`

`resource.studySpec.parameters.doubleValueSpec.maxValue`

`resource.studySpec.parameters.doubleValueSpec.minValue`

`resource.studySpec.parameters.integerValueSpec.defaultValue`

`resource.studySpec.parameters.integerValueSpec.maxValue`

`resource.studySpec.parameters.integerValueSpec.minValue`

`resource.studySpec.parameters.parameterId`

`resource.studySpec.parameters.scaleType`

`resource.studySpec.studyStoppingConfig.maxDurationNoProgress`

`resource.studySpec.studyStoppingConfig.maximumRuntimeConstraint.endTime`

`resource.studySpec.studyStoppingConfig.maximumRuntimeConstraint.maxDuration`

`resource.studySpec.studyStoppingConfig.maxNumTrials`

`resource.studySpec.studyStoppingConfig.maxNumTrialsNoProgress`

`resource.studySpec.studyStoppingConfig.minimumRuntimeConstraint.endTime`

`resource.studySpec.studyStoppingConfig.minimumRuntimeConstraint.maxDuration`

`resource.studySpec.studyStoppingConfig.minNumTrials`

`resource.studySpec.studyStoppingConfig.shouldStopAsap`

`resource.trialJobSpec.baseOutputDirectory.outputUriPrefix`

`resource.trialJobSpec.enableDashboardAccess`

`resource.trialJobSpec.enableWebAccess`

`resource.trialJobSpec.experiment`

`resource.trialJobSpec.experimentRun`

`resource.trialJobSpec.models`

`resource.trialJobSpec.network`

`resource.trialJobSpec.persistentResourceId`

`resource.trialJobSpec.protectedArtifactLocationId`

`resource.trialJobSpec.pscInterfaceConfig.networkAttachment`

`resource.trialJobSpec.reservedIpRanges`

`resource.trialJobSpec.scheduling.disableRetries`

`resource.trialJobSpec.scheduling.maxWaitDuration`

`resource.trialJobSpec.scheduling.restartJobOnWorkerRestart`

`resource.trialJobSpec.scheduling.strategy`

`resource.trialJobSpec.scheduling.timeout`

`resource.trialJobSpec.serviceAccount`

`resource.trialJobSpec.tensorboard`

`resource.trialJobSpec.workerPoolSpecs.containerSpec.args`

`resource.trialJobSpec.workerPoolSpecs.containerSpec.command`

`resource.trialJobSpec.workerPoolSpecs.containerSpec.imageUri`

`resource.trialJobSpec.workerPoolSpecs.diskSpec.bootDiskSizeGb`

`resource.trialJobSpec.workerPoolSpecs.diskSpec.bootDiskType`

`resource.trialJobSpec.workerPoolSpecs.machineSpec.acceleratorCount`

`resource.trialJobSpec.workerPoolSpecs.machineSpec.acceleratorType`

`resource.trialJobSpec.workerPoolSpecs.machineSpec.machineType`

`resource.trialJobSpec.workerPoolSpecs.machineSpec.reservationAffinity.key`

`resource.trialJobSpec.workerPoolSpecs.machineSpec.reservationAffinity.reservationAffinityType`

`resource.trialJobSpec.workerPoolSpecs.machineSpec.reservationAffinity.values`

`resource.trialJobSpec.workerPoolSpecs.machineSpec.tpuTopology`

`resource.trialJobSpec.workerPoolSpecs.nfsMounts.mountPoint`

`resource.trialJobSpec.workerPoolSpecs.nfsMounts.path`

`resource.trialJobSpec.workerPoolSpecs.nfsMounts.server`

`resource.trialJobSpec.workerPoolSpecs.pythonPackageSpec.args`

`resource.trialJobSpec.workerPoolSpecs.pythonPackageSpec.executorImageUri`

`resource.trialJobSpec.workerPoolSpecs.pythonPackageSpec.packageUris`

`resource.trialJobSpec.workerPoolSpecs.pythonPackageSpec.pythonModule`

`resource.trialJobSpec.workerPoolSpecs.replicaCount`

aiplatform.googleapis.com/NasJob

`resource.displayName`

`resource.encryptionSpec.kmsKeyName`

`resource.nasJobSpec.multiTrialAlgorithmSpec.metric.goal`

`resource.nasJobSpec.multiTrialAlgorithmSpec.metric.metricId`

`resource.nasJobSpec.multiTrialAlgorithmSpec.multiTrialAlgorithm`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.maxFailedTrialCount`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.maxParallelTrialCount`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.maxTrialCount`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.baseOutputDirectory.outputUriPrefix`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.enableDashboardAccess`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.enableWebAccess`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.experiment`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.experimentRun`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.models`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.network`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.persistentResourceId`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.protectedArtifactLocationId`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.pscInterfaceConfig.networkAttachment`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.reservedIpRanges`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.scheduling.disableRetries`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.scheduling.maxWaitDuration`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.scheduling.restartJobOnWorkerRestart`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.scheduling.strategy`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.scheduling.timeout`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.serviceAccount`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.tensorboard`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.containerSpec.args`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.containerSpec.command`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.containerSpec.imageUri`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.diskSpec.bootDiskSizeGb`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.diskSpec.bootDiskType`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.machineSpec.acceleratorCount`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.machineSpec.acceleratorType`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.machineSpec.machineType`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.machineSpec.reservationAffinity.key`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.machineSpec.reservationAffinity.reservationAffinityType`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.machineSpec.reservationAffinity.values`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.machineSpec.tpuTopology`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.nfsMounts.mountPoint`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.nfsMounts.path`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.nfsMounts.server`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.pythonPackageSpec.args`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.pythonPackageSpec.executorImageUri`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.pythonPackageSpec.packageUris`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.pythonPackageSpec.pythonModule`

`resource.nasJobSpec.multiTrialAlgorithmSpec.searchTrialSpec.searchTrialJobSpec.workerPoolSpecs.replicaCount`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.frequency`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.maxParallelTrialCount`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.baseOutputDirectory.outputUriPrefix`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.enableDashboardAccess`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.enableWebAccess`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.experiment`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.experimentRun`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.models`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.network`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.persistentResourceId`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.protectedArtifactLocationId`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.pscInterfaceConfig.networkAttachment`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.reservedIpRanges`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.scheduling.disableRetries`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.scheduling.maxWaitDuration`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.scheduling.restartJobOnWorkerRestart`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.scheduling.strategy`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.scheduling.timeout`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.serviceAccount`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.tensorboard`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.containerSpec.args`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.containerSpec.command`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.containerSpec.imageUri`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.diskSpec.bootDiskSizeGb`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.diskSpec.bootDiskType`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.machineSpec.acceleratorCount`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.machineSpec.acceleratorType`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.machineSpec.machineType`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.machineSpec.reservationAffinity.key`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.machineSpec.reservationAffinity.reservationAffinityType`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.machineSpec.reservationAffinity.values`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.machineSpec.tpuTopology`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.nfsMounts.mountPoint`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.nfsMounts.path`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.nfsMounts.server`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.pythonPackageSpec.args`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.pythonPackageSpec.executorImageUri`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.pythonPackageSpec.packageUris`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.pythonPackageSpec.pythonModule`

`resource.nasJobSpec.multiTrialAlgorithmSpec.trainTrialSpec.trainTrialJobSpec.workerPoolSpecs.replicaCount`

`resource.nasJobSpec.resumeNasJobId`

`resource.nasJobSpec.searchSpaceSpec`

## Set up a custom constraint

A custom constraint is defined in a YAML file by the resources, methods, conditions, and actions that are supported by the service on which you are enforcing the organization policy. Conditions for your custom constraints are defined using [Common Expression Language (CEL)](https://github.com/google/cel-spec/blob/master/doc/intro.md) . For more information about how to build conditions in custom constraints using CEL, see the CEL section of [Creating and managing custom constraints](https://docs.cloud.google.com/organization-policy/create-custom-constraints#common_expression_language) .

### Console

To create a custom constraint, do the following:

In the Google Cloud console, go to the **Organization policies** page.

From the project picker, select the project that you want to set the organization policy for.

Click add **Custom constraint** .

In the **Display name** box, enter a human-readable name for the constraint. This name is used in error messages and can be used for identification and debugging. Don't use personally identifiable information (PII) or sensitive data in display names because this name could be exposed in error messages. This field can contain up to 200 characters.

In the **Constraint ID** box, enter the ID that you want for your new custom constraint. A custom constraint can only contain letters (including upper and lowercase) or numbers, for example `custom.restrictMachineType` . This field can contain up to 70 characters, not counting the prefix ( `custom.` ), for example, `organizations/123456789/customConstraints/custom` . Don't include PII or sensitive data in your constraint ID, because it could be exposed in error messages.

In the **Description** box, enter a human-readable description of the constraint. This description is used as an error message when the policy is violated. Include details about why the policy violation occurred and how to resolve the policy violation. Don't include PII or sensitive data in your description, because it could be exposed in error messages. This field can contain up to 2000 characters.

In the **Resource type** box, select the name of the Google Cloud REST resource containing the object and field that you want to restrict—for example, `container.googleapis.com/NodePool` . Most resource types support up to 20 custom constraints. If you attempt to create more custom constraints, the operation fails.

Under **Enforcement method** , select whether to enforce the constraint on a REST `CREATE` method or both `CREATE` and `UPDATE` methods. If you enforce the constraint with the `UPDATE` method on a resource that violates the constraint, changes to that resource are blocked by the organization policy unless the change resolves the violation.

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
      - UPDATE 
    condition: "CONDITION"
    actionType: ACTION
    displayName: DISPLAY_NAME
    description: DESCRIPTION

Replace the following:

  - `  ORGANIZATION_ID  ` : your organization ID, such as `123456789` .
  - `  CONSTRAINT_NAME  ` : the name that you want for your new custom constraint. A custom constraint can only contain letters (including upper and lowercase) or numbers, for example, `custom.restrictMachineType` . This field can contain up to 70 characters, not counting the prefix ( `custom.` )— for example, `organizations/123456789/customConstraints/custom` . Don't include PII or sensitive data in your constraint ID, because it could be exposed in error messages.
  - `  RESOURCE_NAME  ` : the fully qualified name of the Google Cloud resource containing the object and field that you want to restrict. For example, `aiplatform.googleapis.com/CustomJob` . Most resource types support up to 20 custom constraints. If you attempt to create more custom constraints, the operation fails.
  - `methodTypes` : the REST methods that the constraint is enforced on. Can be `CREATE` or both `CREATE` and `UPDATE` . If you enforce the constraint with the `UPDATE` method on a resource that violates the constraint, changes to that resource are blocked by the organization policy unless the change resolves the violation.
  - `  CONDITION  ` : a [CEL condition](https://docs.cloud.google.com/resource-manager/docs/organization-policy/creating-managing-custom-constraints#common_expression_language) that is written against a representation of a supported service resource. This field can contain up to 1000 characters. For example, `"resource.jobSpec.workerPoolSpecs.exists(spec, spec.machineSpec.machineType != \"n1-standard-4\")"` .
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
  - `  CONSTRAINT_NAME  ` : the name you defined for your custom constraint. For example, `custom.restrictMachineType` .

To enforce the organization policy in [dry-run mode](https://docs.cloud.google.com/organization-policy/test-policies) , run the following command with the `dryRunSpec` flag:

    gcloud org-policies set-policy POLICY_PATH --update-mask=dryRunSpec

Replace `  POLICY_PATH  ` with the full path to your organization policy YAML file. The policy requires up to 15 minutes to take effect.

After you verify that the organization policy in dry-run mode works as intended, set the live policy with the `org-policies set-policy` command and the `spec` flag:

    gcloud org-policies set-policy POLICY_PATH --update-mask=spec

Replace `  POLICY_PATH  ` with the full path to your organization policy YAML file. The policy requires up to 15 minutes to take effect.

## Test the custom organization policy

The following example creates a custom constraint and policy that restricts the machine type.

Before you begin, you must know the following:

  - Your organization ID
  - A project ID

### Create the constraint

1.  Save the following file as `constraint-custom-job.yaml` :
    
        name: organizations/ORGANIZATION_ID/customConstraints/custom.restrictMachineType
        resourceTypes:
        - aiplatform.googleapis.com/CustomJob
        methodTypes:
        - CREATE
        condition: "resource.jobSpec.workerPoolSpecs.exists(spec, spec.machineSpec.machineType != \"n1-standard-4\")"
        actionType: DENY
        displayName: Restrict machine type custom training jobs
        description: All new custom training jobs must use n1-standard-4 machines.
    
    This defines a constraint where every new serverless training job must use the `n1-standard-4` machine type. If a serverless training job doesn't use this machine type, its creation is denied.

2.  Apply the constraint:
    
        gcloud org-policies set-custom-constraint ~/constraint-custom-job.yaml

3.  Verify that the constraint exists:
    
        gcloud org-policies list-custom-constraints --organization=ORGANIZATION_ID
    
    The output is similar to the following:
    
        CUSTOM_CONSTRAINT                            ACTION_TYPE  METHOD_TYPES   RESOURCE_TYPES                                     DISPLAY_NAME
        custom.restrictMachineType                   DENY         CREATE         aiplatform.googleapis.com/CustomJob                Restrict machine type custom training jobs
        ...

### Create the policy

1.  Save the following file as `policy-deny-custom-job.yaml` :
    
        name: projects/PROJECT_ID/policies/custom.restrictMachineType
        spec:
          rules:
          - enforce: true
    
    Replace `  PROJECT_ID  ` with your project ID.

2.  Apply the policy:
    
        gcloud org-policies set-policy ~/policy-deny-custom-job.yaml

3.  Verify that the policy exists:
    
        gcloud org-policies list --project=PROJECT_ID
    
    The output is similar to the following:
    
        CONSTRAINT                          LIST_POLICY  BOOLEAN_POLICY        ETAG
        custom.restrictMachineType          -            SET                   CLj9zMIGEIiS3K4D-

After you apply the policy, wait about two minutes for Google Cloud to start enforcing the policy.

### Test the policy

Try to create a serverless training job with restricted machine type:

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --worker-pool-spec=machine-type=n1-standard-8,replica-count=REPLICA_COUNT,container-image-uri=CUSTOM_CONTAINER_IMAGE_URI

The output is the following:

    Operation denied by org policy on resource 'projects/PROJECT_ID/locations/LOCATION': ["customConstraints/custom.restrictMachineType": "All new custom training jobs must use n1-standard-4 machines."]

## Example custom organization policies for common use cases

This table provides syntax examples for some common custom constraints.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Description</th>
<th>Constraint syntax</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Restrict machine type for Agent Platform custom training jobs</td>
<td><pre dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>      name: organizations/ORGANIZATION_ID/customConstraints/custom.restrictMachineType
      resourceTypes:
      - aiplatform.googleapis.com/CustomJob
      methodTypes:
      - CREATE
      condition: &quot;resource.jobSpec.workerPoolSpecs.exists(spec, spec.machineSpec.machineType != &quot;n1-standard-4&quot;)&quot;
      actionType: DENY
      displayName: Restrict machine type custom training jobs
      description: All new custom training jobs must use n1-standard-4 machines.
    </code></pre></td>
</tr>
</tbody>
</table>

## What's next

  - Learn more about [Organization Policy Service](https://docs.cloud.google.com/organization-policy/overview) .
  - Learn more about how to [create and manage organization policies](https://docs.cloud.google.com/organization-policy/create-organization-policies) .
  - See the full list of managed [organization policy constraints](https://docs.cloud.google.com/organization-policy/reference/org-policy-constraints) .
