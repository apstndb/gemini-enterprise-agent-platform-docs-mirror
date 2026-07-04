---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/iam
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/iam
title: Agent Platform Workbench instances access control
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page describes how to use [Identity and Access Management (IAM)](https://docs.cloud.google.com/iam) and an access mode to manage access to Gemini Enterprise Agent Platform Workbench resources. To manage access to Gemini Enterprise Agent Platform resources, see the [Agent Platform page on access control](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) .

Agent Platform Workbench uses IAM to manage access to instances and an access mode to manage access to each instance's JupyterLab interface.

## Control access to an instance with IAM

You can manage access to a Agent Platform Workbench instance at the project level or per instance.

  - To grant access to resources at the project level, assign one or more [roles](https://docs.cloud.google.com/iam/docs/understanding-roles) to a principal (user, group, or [service account](https://docs.cloud.google.com/iam/docs/overview#service_account) ).
  - To grant access to a specific instance, set an IAM policy on that resource. The policy defines which roles are assigned to which principals. To learn more, see [Manage access to an instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access) .

Access to an instance can include a broad range of abilities. For example, you might grant a principal the ability to start, stop, and upgrade an instance. However, even granting a principal full access to a Agent Platform Workbench instance doesn't grant the ability to use the instance's JupyterLab interface. See the following section.

## Control access to an instance's JupyterLab interface with the access mode

You control access to a Agent Platform Workbench instance's JupyterLab interface through the instance's access mode. You set a JupyterLab access mode when you create a Agent Platform Workbench instance. The access mode can't be changed after the notebook is created.

The JupyterLab access mode determines who can use the instance's JupyterLab interface. The access mode also determines which credentials are used when your instance interacts with other Google Cloud services. To learn more, see [Manage access to an instance's JupyterLab interface](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access-jupyterlab) .

## Types of IAM roles

There are different types of IAM roles that can be used in Agent Platform Workbench:

  - [Predefined roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/iam#iam-roles) let you grant a set of related permissions to your Agent Platform Workbench resources at the project level.

  - [Basic roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/iam#basic-roles) (Owner, Editor, and Viewer) provide access control to your Agent Platform Workbench resources at the project level, and are common to all Google Cloud services.

  - [Custom roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/iam#custom-roles) enable you to choose a specific set of permissions, create your own role with those permissions, and grant the role to users in your organization.

To add, update, or remove these roles in your Agent Platform Workbench project, see the documentation on [granting, changing, and revoking access](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

## Predefined Agent Platform Workbench IAM roles

Agent Platform Workbench resources are managed through the Notebooks API. Therefore, Notebooks roles define permissions and access to the use of Agent Platform Workbench.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><h4 id="notebooks.admin" class="role-title add-link" data-text="Notebooks Admin" tabindex="-1">Notebooks Admin</h4>
<p>( <code dir="ltr" translate="no">roles/  notebooks.admin</code> )</p>
<p>Full access to Notebooks, all resources.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Instance</li>
</ul></td>
<td><p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.acceleratorTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.addresses.get</code></p>
<p><code dir="ltr" translate="no">compute.addresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacity</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacityHistory</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.get</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.list</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.commitments.get</code></p>
<p><code dir="ltr" translate="no">compute.commitments.list</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.diskSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.diskTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.diskTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.diskTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.disks.get</code></p>
<p><code dir="ltr" translate="no">compute.disks.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.disks.list</code></p>
<p><code dir="ltr" translate="no">compute.  disks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.disks.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  get</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  list</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.get</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.get</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.list</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.futureReservations.get</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  list</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.get</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  globalOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.hosts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.hosts.get</code></li>
<li><code dir="ltr" translate="no">compute.hosts.getVersion</code></li>
<li><code dir="ltr" translate="no">compute.hosts.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.images.get</code></p>
<p><code dir="ltr" translate="no">compute.images.getFromFamily</code></p>
<p><code dir="ltr" translate="no">compute.images.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.images.list</code></p>
<p><code dir="ltr" translate="no">compute.  images.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.images.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  get</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  list</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.instanceGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.instanceGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.instanceSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.instanceTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  instanceTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instanceTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.instances.get</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getGuestAttributes</code></p>
<p><code dir="ltr" translate="no">compute.instances.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getScreenshot</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getSerialPortOutput</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getShieldedInstanceIdentity</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getShieldedVmIdentity</code></p>
<p><code dir="ltr" translate="no">compute.instances.list</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listReferrers</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.interconnectGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.interconnects.get</code></p>
<p><code dir="ltr" translate="no">compute.interconnects.list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.get</code></p>
<p><code dir="ltr" translate="no">compute.  licenseCodes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.list</code></p>
<p><code dir="ltr" translate="no">compute.licenses.get</code></p>
<p><code dir="ltr" translate="no">compute.licenses.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenses.list</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.get</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.list</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.machineTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.machineTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.machineTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.multiMig.get</code></p>
<p><code dir="ltr" translate="no">compute.multiMig.list</code></p>
<p><code dir="ltr" translate="no">compute.multiMigMembers.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.multiMigMembers.get</code></li>
<li><code dir="ltr" translate="no">compute.multiMigMembers.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networkAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.networkProfiles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.networkProfiles.get</code></li>
<li><code dir="ltr" translate="no">compute.networkProfiles.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networks.get</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getRegionEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.networks.list</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listPeeringRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.nodeTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.nodeTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.  organizations.  listAssociations</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.get</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.list</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.get</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.list</code></p>
<p><code dir="ltr" translate="no">compute.projects.get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.regions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.regions.get</code></li>
<li><code dir="ltr" translate="no">compute.regions.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.reservationBlocks.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationBlocks.list</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  list</code></p>
<p><code dir="ltr" translate="no">compute.reservations.get</code></p>
<p><code dir="ltr" translate="no">compute.reservations.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  resourcePolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.get</code></p>
<p><code dir="ltr" translate="no">compute.routers.getRoutePolicy</code></p>
<p><code dir="ltr" translate="no">compute.routers.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.listBgpRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listRoutePolicies</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.routes.get</code></p>
<p><code dir="ltr" translate="no">compute.routes.list</code></p>
<p><code dir="ltr" translate="no">compute.  routes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.routes.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.serviceAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  snapshotGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.snapshotSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  snapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  snapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.spotAssistants.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.get</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.list</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpsProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.get</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.get</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  zoneOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.zones.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.zones.get</code></li>
<li><code dir="ltr" translate="no">compute.zones.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.*</code></p>
<ul>
<li><code dir="ltr" translate="no">notebooks.environments.create</code></li>
<li><code dir="ltr" translate="no">notebooks.environments.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.environments.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  environments.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.environments.list</code></li>
<li><code dir="ltr" translate="no">notebooks.  environments.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.create</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  executions.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.list</code></li>
<li><code dir="ltr" translate="no">notebooks.  executions.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  checkUpgradability</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.create</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.diagnose</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.get</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.getHealth</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.list</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.reset</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  setAccelerator</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.setLabels</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  setMachineType</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.start</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.stop</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.update</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  updateConfig</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  updateShieldInstanceConfig</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.upgrade</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.use</code></li>
<li><code dir="ltr" translate="no">notebooks.locations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.locations.list</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.cancel</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.list</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.create</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.diagnose</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  runtimes.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.list</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.reset</code></li>
<li><code dir="ltr" translate="no">notebooks.  runtimes.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.start</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.stop</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.switch</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.update</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.upgrade</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.create</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  schedules.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.list</code></li>
<li><code dir="ltr" translate="no">notebooks.  schedules.  setIamPolicy</code></li>
</ul>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  analyze</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.  effectivepolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.groups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">serviceusage.groups.list</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listExpandedMembers</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listMembers</code></li>
</ul>
<p><code dir="ltr" translate="no">serviceusage.quotas.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.values.test</code></p></td>
</tr>
<tr class="even">
<td><h4 id="notebooks.editor" class="role-title add-link" data-text="Notebooks Editor" tabindex="-1">Notebooks Editor</h4>
<p>( <code dir="ltr" translate="no">roles/  notebooks.editor</code> )</p>
<p>Editor role for notebooks</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.list</code></p>
<p><code dir="ltr" translate="no">compute.acceleratorTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.addresses.get</code></p>
<p><code dir="ltr" translate="no">compute.addresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacity</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacityHistory</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.get</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.list</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.commitments.get</code></p>
<p><code dir="ltr" translate="no">compute.commitments.list</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.diskSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.diskTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.diskTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.diskTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.disks.get</code></p>
<p><code dir="ltr" translate="no">compute.disks.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.disks.list</code></p>
<p><code dir="ltr" translate="no">compute.  disks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.disks.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  get</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  list</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.get</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.get</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.list</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.futureReservations.get</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  list</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.get</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  globalOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.hosts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.hosts.get</code></li>
<li><code dir="ltr" translate="no">compute.hosts.getVersion</code></li>
<li><code dir="ltr" translate="no">compute.hosts.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.images.get</code></p>
<p><code dir="ltr" translate="no">compute.images.getFromFamily</code></p>
<p><code dir="ltr" translate="no">compute.images.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.images.list</code></p>
<p><code dir="ltr" translate="no">compute.  images.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.images.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  get</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  list</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.instanceGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.instanceGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.instanceSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.instanceTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  instanceTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instanceTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.instances.get</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getGuestAttributes</code></p>
<p><code dir="ltr" translate="no">compute.instances.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getScreenshot</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getSerialPortOutput</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getShieldedInstanceIdentity</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getShieldedVmIdentity</code></p>
<p><code dir="ltr" translate="no">compute.instances.list</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listReferrers</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.interconnectGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.interconnects.get</code></p>
<p><code dir="ltr" translate="no">compute.interconnects.list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.get</code></p>
<p><code dir="ltr" translate="no">compute.  licenseCodes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.list</code></p>
<p><code dir="ltr" translate="no">compute.licenses.get</code></p>
<p><code dir="ltr" translate="no">compute.licenses.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenses.list</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.get</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.list</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.machineTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.machineTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.machineTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.multiMig.get</code></p>
<p><code dir="ltr" translate="no">compute.multiMig.list</code></p>
<p><code dir="ltr" translate="no">compute.multiMigMembers.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.multiMigMembers.get</code></li>
<li><code dir="ltr" translate="no">compute.multiMigMembers.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networkAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.networkProfiles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.networkProfiles.get</code></li>
<li><code dir="ltr" translate="no">compute.networkProfiles.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networks.get</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getRegionEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.networks.list</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listPeeringRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.nodeTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.nodeTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.  organizations.  listAssociations</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.get</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.list</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.get</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.list</code></p>
<p><code dir="ltr" translate="no">compute.projects.get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.regions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.regions.get</code></li>
<li><code dir="ltr" translate="no">compute.regions.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.reservationBlocks.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationBlocks.list</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  list</code></p>
<p><code dir="ltr" translate="no">compute.reservations.get</code></p>
<p><code dir="ltr" translate="no">compute.reservations.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  resourcePolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.get</code></p>
<p><code dir="ltr" translate="no">compute.routers.getRoutePolicy</code></p>
<p><code dir="ltr" translate="no">compute.routers.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.listBgpRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listRoutePolicies</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.routes.get</code></p>
<p><code dir="ltr" translate="no">compute.routes.list</code></p>
<p><code dir="ltr" translate="no">compute.  routes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.routes.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.serviceAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  snapshotGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.snapshotSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  snapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  snapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.spotAssistants.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.get</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.list</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpsProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.get</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.get</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  zoneOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.zones.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.zones.get</code></li>
<li><code dir="ltr" translate="no">compute.zones.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.environments.create</code></p>
<p><code dir="ltr" translate="no">notebooks.environments.delete</code></p>
<p><code dir="ltr" translate="no">notebooks.environments.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  environments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.environments.list</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.create</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.delete</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  executions.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.list</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  checkUpgradability</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.create</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.delete</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.diagnose</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.get</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.getHealth</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.list</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.reset</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  setAccelerator</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.setLabels</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  setMachineType</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.start</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.stop</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.update</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  updateConfig</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  updateShieldInstanceConfig</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.upgrade</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.use</code></p>
<p><code dir="ltr" translate="no">notebooks.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">notebooks.locations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.operations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">notebooks.operations.cancel</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.runtimes.create</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.delete</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.diagnose</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  runtimes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.list</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.reset</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.start</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.stop</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.switch</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.update</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.upgrade</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.create</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.delete</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  schedules.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.list</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  analyze</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.  effectivepolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.groups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">serviceusage.groups.list</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listExpandedMembers</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listMembers</code></li>
</ul>
<p><code dir="ltr" translate="no">serviceusage.quotas.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.values.test</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="notebooks.viewer" class="role-title add-link" data-text="Notebooks Viewer" tabindex="-1">Notebooks Viewer</h4>
<p>( <code dir="ltr" translate="no">roles/  notebooks.viewer</code> )</p>
<p>Read-only access to Notebooks, all resources.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Instance</li>
</ul></td>
<td><p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.list</code></p>
<p><code dir="ltr" translate="no">compute.acceleratorTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.addresses.get</code></p>
<p><code dir="ltr" translate="no">compute.addresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacity</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacityHistory</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.get</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.list</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.commitments.get</code></p>
<p><code dir="ltr" translate="no">compute.commitments.list</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.diskSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.diskTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.diskTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.diskTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.disks.get</code></p>
<p><code dir="ltr" translate="no">compute.disks.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.disks.list</code></p>
<p><code dir="ltr" translate="no">compute.  disks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.disks.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  get</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  list</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.get</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.get</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.list</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.futureReservations.get</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  list</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.get</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  globalOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.hosts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.hosts.get</code></li>
<li><code dir="ltr" translate="no">compute.hosts.getVersion</code></li>
<li><code dir="ltr" translate="no">compute.hosts.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.images.get</code></p>
<p><code dir="ltr" translate="no">compute.images.getFromFamily</code></p>
<p><code dir="ltr" translate="no">compute.images.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.images.list</code></p>
<p><code dir="ltr" translate="no">compute.  images.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.images.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  get</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  list</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.instanceGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.instanceGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.instanceSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.instanceTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  instanceTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instanceTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.instances.get</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getGuestAttributes</code></p>
<p><code dir="ltr" translate="no">compute.instances.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getScreenshot</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getSerialPortOutput</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getShieldedInstanceIdentity</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getShieldedVmIdentity</code></p>
<p><code dir="ltr" translate="no">compute.instances.list</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listReferrers</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.interconnectGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.interconnects.get</code></p>
<p><code dir="ltr" translate="no">compute.interconnects.list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.get</code></p>
<p><code dir="ltr" translate="no">compute.  licenseCodes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.list</code></p>
<p><code dir="ltr" translate="no">compute.licenses.get</code></p>
<p><code dir="ltr" translate="no">compute.licenses.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenses.list</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.get</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.list</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.machineTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.machineTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.machineTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.multiMig.get</code></p>
<p><code dir="ltr" translate="no">compute.multiMig.list</code></p>
<p><code dir="ltr" translate="no">compute.multiMigMembers.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.multiMigMembers.get</code></li>
<li><code dir="ltr" translate="no">compute.multiMigMembers.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networkAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.networkProfiles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.networkProfiles.get</code></li>
<li><code dir="ltr" translate="no">compute.networkProfiles.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networks.get</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getRegionEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.networks.list</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listPeeringRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.nodeTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.nodeTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.  organizations.  listAssociations</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.get</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.list</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.get</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.list</code></p>
<p><code dir="ltr" translate="no">compute.projects.get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.regions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.regions.get</code></li>
<li><code dir="ltr" translate="no">compute.regions.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.reservationBlocks.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationBlocks.list</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  list</code></p>
<p><code dir="ltr" translate="no">compute.reservations.get</code></p>
<p><code dir="ltr" translate="no">compute.reservations.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  resourcePolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.get</code></p>
<p><code dir="ltr" translate="no">compute.routers.getRoutePolicy</code></p>
<p><code dir="ltr" translate="no">compute.routers.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.listBgpRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listRoutePolicies</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.routes.get</code></p>
<p><code dir="ltr" translate="no">compute.routes.list</code></p>
<p><code dir="ltr" translate="no">compute.  routes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.routes.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.serviceAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  snapshotGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.snapshotSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  snapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  snapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.spotAssistants.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.get</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.list</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpsProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.get</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.get</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  zoneOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.zones.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.zones.get</code></li>
<li><code dir="ltr" translate="no">compute.zones.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.environments.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  environments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.environments.list</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  executions.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.list</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  checkUpgradability</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.get</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.getHealth</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.list</code></p>
<p><code dir="ltr" translate="no">notebooks.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">notebooks.locations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.operations.get</code></p>
<p><code dir="ltr" translate="no">notebooks.operations.list</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  runtimes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.list</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  schedules.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.list</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  analyze</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.  effectivepolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.groups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">serviceusage.groups.list</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listExpandedMembers</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listMembers</code></li>
</ul>
<p><code dir="ltr" translate="no">serviceusage.quotas.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.values.test</code></p></td>
</tr>
<tr class="even">
<td><h4 id="notebooks.legacyAdmin" class="role-title add-link" data-text="Notebooks Legacy Admin" tabindex="-1">Notebooks Legacy Admin</h4>
<p>( <code dir="ltr" translate="no">roles/  notebooks.legacyAdmin</code> )</p>
<p>Full access to Notebooks all resources through compute API.</p></td>
<td><p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  createForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  createForComputeInstance</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  deleteForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  deleteForComputeInstance</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  fetchForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  getForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  list</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  triggerBackupForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  triggerBackupForComputeInstance</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  updateForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  updateForComputeInstance</code></p>
<p><code dir="ltr" translate="no">backupdr.backupPlans.get</code></p>
<p><code dir="ltr" translate="no">backupdr.backupPlans.list</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlans.  useForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlans.  useForComputeInstance</code></p>
<p><code dir="ltr" translate="no">backupdr.backupVaults.get</code></p>
<p><code dir="ltr" translate="no">backupdr.backupVaults.list</code></p>
<p><code dir="ltr" translate="no">backupdr.locations.list</code></p>
<p><code dir="ltr" translate="no">backupdr.operations.get</code></p>
<p><code dir="ltr" translate="no">backupdr.operations.list</code></p>
<p><code dir="ltr" translate="no">backupdr.  serviceConfig.  initialize</code></p>
<p><code dir="ltr" translate="no">cloudkms.keyHandles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">cloudkms.keyHandles.create</code></li>
<li><code dir="ltr" translate="no">cloudkms.keyHandles.get</code></li>
<li><code dir="ltr" translate="no">cloudkms.keyHandles.list</code></li>
</ul>
<p><code dir="ltr" translate="no">cloudkms.operations.get</code></p>
<p><code dir="ltr" translate="no">cloudkms.  projects.  showEffectiveAutokeyConfig</code></p>
<p><code dir="ltr" translate="no">compute.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.list</code></li>
<li><code dir="ltr" translate="no">compute.addresses.create</code></li>
<li><code dir="ltr" translate="no">compute.  addresses.  createInternal</code></li>
<li><code dir="ltr" translate="no">compute.  addresses.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.addresses.delete</code></li>
<li><code dir="ltr" translate="no">compute.  addresses.  deleteInternal</code></li>
<li><code dir="ltr" translate="no">compute.  addresses.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.addresses.get</code></li>
<li><code dir="ltr" translate="no">compute.addresses.list</code></li>
<li><code dir="ltr" translate="no">compute.  addresses.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  addresses.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.addresses.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.addresses.use</code></li>
<li><code dir="ltr" translate="no">compute.addresses.useInternal</code></li>
<li><code dir="ltr" translate="no">compute.advice.calendarMode</code></li>
<li><code dir="ltr" translate="no">compute.advice.capacity</code></li>
<li><code dir="ltr" translate="no">compute.advice.capacityHistory</code></li>
<li><code dir="ltr" translate="no">compute.autoscalers.create</code></li>
<li><code dir="ltr" translate="no">compute.autoscalers.delete</code></li>
<li><code dir="ltr" translate="no">compute.autoscalers.get</code></li>
<li><code dir="ltr" translate="no">compute.autoscalers.list</code></li>
<li><code dir="ltr" translate="no">compute.autoscalers.update</code></li>
<li><code dir="ltr" translate="no">compute.  backendBuckets.  addSignedUrlKey</code></li>
<li><code dir="ltr" translate="no">compute.backendBuckets.create</code></li>
<li><code dir="ltr" translate="no">compute.  backendBuckets.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.backendBuckets.delete</code></li>
<li><code dir="ltr" translate="no">compute.  backendBuckets.  deleteSignedUrlKey</code></li>
<li><code dir="ltr" translate="no">compute.  backendBuckets.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.backendBuckets.get</code></li>
<li><code dir="ltr" translate="no">compute.  backendBuckets.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.backendBuckets.list</code></li>
<li><code dir="ltr" translate="no">compute.  backendBuckets.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  backendBuckets.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  backendBuckets.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  backendBuckets.  setSecurityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.backendBuckets.update</code></li>
<li><code dir="ltr" translate="no">compute.backendBuckets.use</code></li>
<li><code dir="ltr" translate="no">compute.  backendServices.  addSignedUrlKey</code></li>
<li><code dir="ltr" translate="no">compute.backendServices.create</code></li>
<li><code dir="ltr" translate="no">compute.  backendServices.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.backendServices.delete</code></li>
<li><code dir="ltr" translate="no">compute.  backendServices.  deleteSignedUrlKey</code></li>
<li><code dir="ltr" translate="no">compute.  backendServices.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.backendServices.get</code></li>
<li><code dir="ltr" translate="no">compute.  backendServices.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.backendServices.list</code></li>
<li><code dir="ltr" translate="no">compute.  backendServices.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  backendServices.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  backendServices.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  backendServices.  setSecurityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.backendServices.update</code></li>
<li><code dir="ltr" translate="no">compute.backendServices.use</code></li>
<li><code dir="ltr" translate="no">compute.commitments.create</code></li>
<li><code dir="ltr" translate="no">compute.  commitments.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  commitments.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.commitments.get</code></li>
<li><code dir="ltr" translate="no">compute.commitments.list</code></li>
<li><code dir="ltr" translate="no">compute.  commitments.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  commitments.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.commitments.update</code></li>
<li><code dir="ltr" translate="no">compute.  commitments.  updateReservations</code></li>
<li><code dir="ltr" translate="no">compute.  crossSiteNetworks.  create</code></li>
<li><code dir="ltr" translate="no">compute.  crossSiteNetworks.  delete</code></li>
<li><code dir="ltr" translate="no">compute.crossSiteNetworks.get</code></li>
<li><code dir="ltr" translate="no">compute.crossSiteNetworks.list</code></li>
<li><code dir="ltr" translate="no">compute.  crossSiteNetworks.  update</code></li>
<li><code dir="ltr" translate="no">compute.diskSettings.get</code></li>
<li><code dir="ltr" translate="no">compute.diskSettings.update</code></li>
<li><code dir="ltr" translate="no">compute.diskTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.diskTypes.list</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  addResourcePolicies</code></li>
<li><code dir="ltr" translate="no">compute.disks.create</code></li>
<li><code dir="ltr" translate="no">compute.disks.createSnapshot</code></li>
<li><code dir="ltr" translate="no">compute.disks.createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.disks.delete</code></li>
<li><code dir="ltr" translate="no">compute.disks.deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.disks.get</code></li>
<li><code dir="ltr" translate="no">compute.disks.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.disks.list</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.disks.listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  removeResourcePolicies</code></li>
<li><code dir="ltr" translate="no">compute.disks.resize</code></li>
<li><code dir="ltr" translate="no">compute.disks.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.disks.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  startAsyncReplication</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  stopAsyncReplication</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  stopGroupAsyncReplication</code></li>
<li><code dir="ltr" translate="no">compute.disks.update</code></li>
<li><code dir="ltr" translate="no">compute.disks.updateKmsKey</code></li>
<li><code dir="ltr" translate="no">compute.disks.use</code></li>
<li><code dir="ltr" translate="no">compute.disks.useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.  externalVpnGateways.  create</code></li>
<li><code dir="ltr" translate="no">compute.  externalVpnGateways.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  externalVpnGateways.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  externalVpnGateways.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  externalVpnGateways.  get</code></li>
<li><code dir="ltr" translate="no">compute.  externalVpnGateways.  list</code></li>
<li><code dir="ltr" translate="no">compute.  externalVpnGateways.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  externalVpnGateways.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  externalVpnGateways.  setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  externalVpnGateways.  use</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  cloneRules</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  copyRules</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.firewallPolicies.get</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.firewallPolicies.list</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.firewallPolicies.move</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  firewallPolicies.  update</code></li>
<li><code dir="ltr" translate="no">compute.firewallPolicies.use</code></li>
<li><code dir="ltr" translate="no">compute.firewalls.create</code></li>
<li><code dir="ltr" translate="no">compute.  firewalls.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.firewalls.delete</code></li>
<li><code dir="ltr" translate="no">compute.  firewalls.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.firewalls.get</code></li>
<li><code dir="ltr" translate="no">compute.firewalls.list</code></li>
<li><code dir="ltr" translate="no">compute.  firewalls.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  firewalls.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.firewalls.update</code></li>
<li><code dir="ltr" translate="no">compute.forwardingRules.create</code></li>
<li><code dir="ltr" translate="no">compute.  forwardingRules.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.forwardingRules.delete</code></li>
<li><code dir="ltr" translate="no">compute.  forwardingRules.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.forwardingRules.get</code></li>
<li><code dir="ltr" translate="no">compute.forwardingRules.list</code></li>
<li><code dir="ltr" translate="no">compute.  forwardingRules.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  forwardingRules.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  forwardingRules.  pscCreate</code></li>
<li><code dir="ltr" translate="no">compute.  forwardingRules.  pscDelete</code></li>
<li><code dir="ltr" translate="no">compute.  forwardingRules.  pscSetLabels</code></li>
<li><code dir="ltr" translate="no">compute.  forwardingRules.  pscUpdate</code></li>
<li><code dir="ltr" translate="no">compute.  forwardingRules.  setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  forwardingRules.  setTarget</code></li>
<li><code dir="ltr" translate="no">compute.forwardingRules.update</code></li>
<li><code dir="ltr" translate="no">compute.forwardingRules.use</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  cancel</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  create</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.futureReservations.get</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  list</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  futureReservations.  update</code></li>
<li><code dir="ltr" translate="no">compute.globalAddresses.create</code></li>
<li><code dir="ltr" translate="no">compute.  globalAddresses.  createInternal</code></li>
<li><code dir="ltr" translate="no">compute.  globalAddresses.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.globalAddresses.delete</code></li>
<li><code dir="ltr" translate="no">compute.  globalAddresses.  deleteInternal</code></li>
<li><code dir="ltr" translate="no">compute.  globalAddresses.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.globalAddresses.get</code></li>
<li><code dir="ltr" translate="no">compute.globalAddresses.list</code></li>
<li><code dir="ltr" translate="no">compute.  globalAddresses.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  globalAddresses.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  globalAddresses.  setLabels</code></li>
<li><code dir="ltr" translate="no">compute.globalAddresses.use</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  create</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  get</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  list</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  pscCreate</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  pscDelete</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  pscSetLabels</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  pscUpdate</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  setTarget</code></li>
<li><code dir="ltr" translate="no">compute.  globalForwardingRules.  update</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  attachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  create</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  detachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  get</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  list</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  use</code></li>
<li><code dir="ltr" translate="no">compute.  globalOperations.  delete</code></li>
<li><code dir="ltr" translate="no">compute.globalOperations.get</code></li>
<li><code dir="ltr" translate="no">compute.  globalOperations.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.globalOperations.list</code></li>
<li><code dir="ltr" translate="no">compute.  globalOperations.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  create</code></li>
<li><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  get</code></li>
<li><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  list</code></li>
<li><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  updatePolicy</code></li>
<li><code dir="ltr" translate="no">compute.healthChecks.create</code></li>
<li><code dir="ltr" translate="no">compute.  healthChecks.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.healthChecks.delete</code></li>
<li><code dir="ltr" translate="no">compute.  healthChecks.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.healthChecks.get</code></li>
<li><code dir="ltr" translate="no">compute.healthChecks.list</code></li>
<li><code dir="ltr" translate="no">compute.  healthChecks.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  healthChecks.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.healthChecks.update</code></li>
<li><code dir="ltr" translate="no">compute.healthChecks.use</code></li>
<li><code dir="ltr" translate="no">compute.  healthChecks.  useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.hosts.get</code></li>
<li><code dir="ltr" translate="no">compute.hosts.getVersion</code></li>
<li><code dir="ltr" translate="no">compute.hosts.list</code></li>
<li><code dir="ltr" translate="no">compute.  httpHealthChecks.  create</code></li>
<li><code dir="ltr" translate="no">compute.  httpHealthChecks.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  httpHealthChecks.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  httpHealthChecks.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.httpHealthChecks.get</code></li>
<li><code dir="ltr" translate="no">compute.httpHealthChecks.list</code></li>
<li><code dir="ltr" translate="no">compute.  httpHealthChecks.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  httpHealthChecks.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  httpHealthChecks.  update</code></li>
<li><code dir="ltr" translate="no">compute.httpHealthChecks.use</code></li>
<li><code dir="ltr" translate="no">compute.  httpHealthChecks.  useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.  httpsHealthChecks.  create</code></li>
<li><code dir="ltr" translate="no">compute.  httpsHealthChecks.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  httpsHealthChecks.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  httpsHealthChecks.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.httpsHealthChecks.get</code></li>
<li><code dir="ltr" translate="no">compute.httpsHealthChecks.list</code></li>
<li><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  httpsHealthChecks.  update</code></li>
<li><code dir="ltr" translate="no">compute.httpsHealthChecks.use</code></li>
<li><code dir="ltr" translate="no">compute.  httpsHealthChecks.  useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.images.create</code></li>
<li><code dir="ltr" translate="no">compute.  images.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.images.delete</code></li>
<li><code dir="ltr" translate="no">compute.  images.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.images.deprecate</code></li>
<li><code dir="ltr" translate="no">compute.images.get</code></li>
<li><code dir="ltr" translate="no">compute.images.getFromFamily</code></li>
<li><code dir="ltr" translate="no">compute.images.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.images.list</code></li>
<li><code dir="ltr" translate="no">compute.  images.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.images.listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.images.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.images.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.images.update</code></li>
<li><code dir="ltr" translate="no">compute.images.useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  create</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  get</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  list</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  update</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  use</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.create</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroups.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.delete</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroups.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.get</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.list</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroups.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroups.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.update</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.use</code></li>
<li><code dir="ltr" translate="no">compute.instanceSettings.get</code></li>
<li><code dir="ltr" translate="no">compute.  instanceSettings.  update</code></li>
<li><code dir="ltr" translate="no">compute.  instanceTemplates.  create</code></li>
<li><code dir="ltr" translate="no">compute.  instanceTemplates.  delete</code></li>
<li><code dir="ltr" translate="no">compute.instanceTemplates.get</code></li>
<li><code dir="ltr" translate="no">compute.  instanceTemplates.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.instanceTemplates.list</code></li>
<li><code dir="ltr" translate="no">compute.  instanceTemplates.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instanceTemplates.  useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  addAccessConfig</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  addNetworkInterface</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  addResourcePolicies</code></li>
<li><code dir="ltr" translate="no">compute.instances.attachDisk</code></li>
<li><code dir="ltr" translate="no">compute.instances.create</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.instances.delete</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  deleteAccessConfig</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  deleteNetworkInterface</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.instances.detachDisk</code></li>
<li><code dir="ltr" translate="no">compute.instances.get</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getEffectiveFirewalls</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getGuestAttributes</code></li>
<li><code dir="ltr" translate="no">compute.instances.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getScreenshot</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getSerialPortOutput</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getShieldedInstanceIdentity</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getShieldedVmIdentity</code></li>
<li><code dir="ltr" translate="no">compute.instances.list</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  listReferrers</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.instances.osAdminLogin</code></li>
<li><code dir="ltr" translate="no">compute.instances.osLogin</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  pscInterfaceCreate</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  removeResourcePolicies</code></li>
<li><code dir="ltr" translate="no">compute.instances.reset</code></li>
<li><code dir="ltr" translate="no">compute.instances.resume</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  sendDiagnosticInterrupt</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setDeletionProtection</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setDiskAutoDelete</code></li>
<li><code dir="ltr" translate="no">compute.instances.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.instances.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setMachineResources</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setMachineType</code></li>
<li><code dir="ltr" translate="no">compute.instances.setMetadata</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setMinCpuPlatform</code></li>
<li><code dir="ltr" translate="no">compute.instances.setName</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setScheduling</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setSecurityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setServiceAccount</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setShieldedInstanceIntegrityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setShieldedVmIntegrityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.instances.setTags</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  simulateMaintenanceEvent</code></li>
<li><code dir="ltr" translate="no">compute.instances.start</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  startWithEncryptionKey</code></li>
<li><code dir="ltr" translate="no">compute.instances.stop</code></li>
<li><code dir="ltr" translate="no">compute.instances.suspend</code></li>
<li><code dir="ltr" translate="no">compute.instances.update</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateAccessConfig</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateDisplayDevice</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateNetworkInterface</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateSecurity</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateShieldedInstanceConfig</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateShieldedVmConfig</code></li>
<li><code dir="ltr" translate="no">compute.instances.use</code></li>
<li><code dir="ltr" translate="no">compute.instances.useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  create</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  get</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  list</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  create</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  export</code></li>
<li><code dir="ltr" translate="no">compute.instantSnapshots.get</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.instantSnapshots.list</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshots.  useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  create</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  list</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  patch</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  create</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  list</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  update</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectAttachments.  use</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectGroups.  create</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectGroups.  delete</code></li>
<li><code dir="ltr" translate="no">compute.interconnectGroups.get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectGroups.  list</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectGroups.  patch</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  list</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  list</code></li>
<li><code dir="ltr" translate="no">compute.interconnects.create</code></li>
<li><code dir="ltr" translate="no">compute.  interconnects.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.interconnects.delete</code></li>
<li><code dir="ltr" translate="no">compute.  interconnects.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.interconnects.get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnects.  getMacsecConfig</code></li>
<li><code dir="ltr" translate="no">compute.interconnects.list</code></li>
<li><code dir="ltr" translate="no">compute.  interconnects.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  interconnects.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  interconnects.  setLabels</code></li>
<li><code dir="ltr" translate="no">compute.interconnects.update</code></li>
<li><code dir="ltr" translate="no">compute.interconnects.use</code></li>
<li><code dir="ltr" translate="no">compute.licenseCodes.get</code></li>
<li><code dir="ltr" translate="no">compute.  licenseCodes.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.licenseCodes.list</code></li>
<li><code dir="ltr" translate="no">compute.  licenseCodes.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.licenses.create</code></li>
<li><code dir="ltr" translate="no">compute.  licenses.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.licenses.delete</code></li>
<li><code dir="ltr" translate="no">compute.  licenses.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.licenses.get</code></li>
<li><code dir="ltr" translate="no">compute.licenses.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.licenses.list</code></li>
<li><code dir="ltr" translate="no">compute.  licenses.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  licenses.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.licenses.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.licenses.update</code></li>
<li><code dir="ltr" translate="no">compute.machineImages.create</code></li>
<li><code dir="ltr" translate="no">compute.  machineImages.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.machineImages.delete</code></li>
<li><code dir="ltr" translate="no">compute.  machineImages.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.machineImages.get</code></li>
<li><code dir="ltr" translate="no">compute.  machineImages.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.machineImages.list</code></li>
<li><code dir="ltr" translate="no">compute.  machineImages.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  machineImages.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  machineImages.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  machineImages.  setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  machineImages.  useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.machineTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.machineTypes.list</code></li>
<li><code dir="ltr" translate="no">compute.multiMig.create</code></li>
<li><code dir="ltr" translate="no">compute.multiMig.delete</code></li>
<li><code dir="ltr" translate="no">compute.multiMig.get</code></li>
<li><code dir="ltr" translate="no">compute.multiMig.list</code></li>
<li><code dir="ltr" translate="no">compute.multiMigMembers.get</code></li>
<li><code dir="ltr" translate="no">compute.multiMigMembers.list</code></li>
<li><code dir="ltr" translate="no">compute.  networkAttachments.  create</code></li>
<li><code dir="ltr" translate="no">compute.  networkAttachments.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  networkAttachments.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  networkAttachments.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.networkAttachments.get</code></li>
<li><code dir="ltr" translate="no">compute.  networkAttachments.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  networkAttachments.  list</code></li>
<li><code dir="ltr" translate="no">compute.  networkAttachments.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  networkAttachments.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  networkAttachments.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  networkAttachments.  update</code></li>
<li><code dir="ltr" translate="no">compute.networkAttachments.use</code></li>
<li><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  create</code></li>
<li><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  get</code></li>
<li><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  list</code></li>
<li><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  update</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  attachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  create</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  detachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  get</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  list</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  use</code></li>
<li><code dir="ltr" translate="no">compute.networkProfiles.get</code></li>
<li><code dir="ltr" translate="no">compute.networkProfiles.list</code></li>
<li><code dir="ltr" translate="no">compute.networks.access</code></li>
<li><code dir="ltr" translate="no">compute.networks.addPeering</code></li>
<li><code dir="ltr" translate="no">compute.networks.create</code></li>
<li><code dir="ltr" translate="no">compute.  networks.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.networks.delete</code></li>
<li><code dir="ltr" translate="no">compute.  networks.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.networks.get</code></li>
<li><code dir="ltr" translate="no">compute.  networks.  getEffectiveFirewalls</code></li>
<li><code dir="ltr" translate="no">compute.  networks.  getRegionEffectiveFirewalls</code></li>
<li><code dir="ltr" translate="no">compute.networks.list</code></li>
<li><code dir="ltr" translate="no">compute.  networks.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  networks.  listPeeringRoutes</code></li>
<li><code dir="ltr" translate="no">compute.  networks.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.networks.mirror</code></li>
<li><code dir="ltr" translate="no">compute.networks.removePeering</code></li>
<li><code dir="ltr" translate="no">compute.  networks.  setFirewallPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  networks.  setNetworkPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  networks.  switchToCustomMode</code></li>
<li><code dir="ltr" translate="no">compute.networks.update</code></li>
<li><code dir="ltr" translate="no">compute.networks.updatePeering</code></li>
<li><code dir="ltr" translate="no">compute.networks.updatePolicy</code></li>
<li><code dir="ltr" translate="no">compute.networks.use</code></li>
<li><code dir="ltr" translate="no">compute.networks.useExternalIp</code></li>
<li><code dir="ltr" translate="no">compute.nodeGroups.addNodes</code></li>
<li><code dir="ltr" translate="no">compute.nodeGroups.create</code></li>
<li><code dir="ltr" translate="no">compute.nodeGroups.delete</code></li>
<li><code dir="ltr" translate="no">compute.nodeGroups.deleteNodes</code></li>
<li><code dir="ltr" translate="no">compute.nodeGroups.get</code></li>
<li><code dir="ltr" translate="no">compute.  nodeGroups.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.nodeGroups.list</code></li>
<li><code dir="ltr" translate="no">compute.  nodeGroups.  performMaintenance</code></li>
<li><code dir="ltr" translate="no">compute.  nodeGroups.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  nodeGroups.  setNodeTemplate</code></li>
<li><code dir="ltr" translate="no">compute.  nodeGroups.  simulateMaintenanceEvent</code></li>
<li><code dir="ltr" translate="no">compute.nodeGroups.update</code></li>
<li><code dir="ltr" translate="no">compute.nodeTemplates.create</code></li>
<li><code dir="ltr" translate="no">compute.nodeTemplates.delete</code></li>
<li><code dir="ltr" translate="no">compute.nodeTemplates.get</code></li>
<li><code dir="ltr" translate="no">compute.  nodeTemplates.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.nodeTemplates.list</code></li>
<li><code dir="ltr" translate="no">compute.  nodeTemplates.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.nodeTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.nodeTypes.list</code></li>
<li><code dir="ltr" translate="no">compute.orgRolloutPlans.create</code></li>
<li><code dir="ltr" translate="no">compute.orgRolloutPlans.delete</code></li>
<li><code dir="ltr" translate="no">compute.orgRolloutPlans.get</code></li>
<li><code dir="ltr" translate="no">compute.orgRolloutPlans.list</code></li>
<li><code dir="ltr" translate="no">compute.orgRollouts.cancel</code></li>
<li><code dir="ltr" translate="no">compute.orgRollouts.delete</code></li>
<li><code dir="ltr" translate="no">compute.orgRollouts.get</code></li>
<li><code dir="ltr" translate="no">compute.orgRollouts.list</code></li>
<li><code dir="ltr" translate="no">compute.orgRollouts.pause</code></li>
<li><code dir="ltr" translate="no">compute.orgRollouts.resume</code></li>
<li><code dir="ltr" translate="no">compute.  organizations.  disableXpnHost</code></li>
<li><code dir="ltr" translate="no">compute.  organizations.  disableXpnResource</code></li>
<li><code dir="ltr" translate="no">compute.  organizations.  enableXpnHost</code></li>
<li><code dir="ltr" translate="no">compute.  organizations.  enableXpnResource</code></li>
<li><code dir="ltr" translate="no">compute.  organizations.  listAssociations</code></li>
<li><code dir="ltr" translate="no">compute.  organizations.  setFirewallPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  organizations.  setSecurityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  oslogin.  updateExternalUser</code></li>
<li><code dir="ltr" translate="no">compute.  packetMirrorings.  create</code></li>
<li><code dir="ltr" translate="no">compute.  packetMirrorings.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  packetMirrorings.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  packetMirrorings.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.packetMirrorings.get</code></li>
<li><code dir="ltr" translate="no">compute.packetMirrorings.list</code></li>
<li><code dir="ltr" translate="no">compute.  packetMirrorings.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  packetMirrorings.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  packetMirrorings.  update</code></li>
<li><code dir="ltr" translate="no">compute.previewFeatures.get</code></li>
<li><code dir="ltr" translate="no">compute.previewFeatures.list</code></li>
<li><code dir="ltr" translate="no">compute.previewFeatures.update</code></li>
<li><code dir="ltr" translate="no">compute.projects.get</code></li>
<li><code dir="ltr" translate="no">compute.  projects.  setCloudArmorTier</code></li>
<li><code dir="ltr" translate="no">compute.  projects.  setCommonInstanceMetadata</code></li>
<li><code dir="ltr" translate="no">compute.  projects.  setDefaultNetworkTier</code></li>
<li><code dir="ltr" translate="no">compute.  projects.  setDefaultServiceAccount</code></li>
<li><code dir="ltr" translate="no">compute.  projects.  setManagedProtectionTier</code></li>
<li><code dir="ltr" translate="no">compute.  projects.  setUsageExportBucket</code></li>
<li><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  create</code></li>
<li><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  get</code></li>
<li><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  list</code></li>
<li><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  update</code></li>
<li><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  updatePolicy</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  announce</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  create</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  get</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  list</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  update</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  updatePolicy</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  use</code></li>
<li><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  withdraw</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendBuckets.  use</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  setSecurityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionBackendServices.  use</code></li>
<li><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  cloneRules</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  use</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  use</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthChecks.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthChecks.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthChecks.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthChecks.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.regionHealthChecks.get</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthChecks.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthChecks.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthChecks.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthChecks.  update</code></li>
<li><code dir="ltr" translate="no">compute.regionHealthChecks.use</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthChecks.  useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthSources.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthSources.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthSources.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthSources.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionHealthSources.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  attachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  detachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  use</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  use</code></li>
<li><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  use</code></li>
<li><code dir="ltr" translate="no">compute.  regionOperations.  delete</code></li>
<li><code dir="ltr" translate="no">compute.regionOperations.get</code></li>
<li><code dir="ltr" translate="no">compute.  regionOperations.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.regionOperations.list</code></li>
<li><code dir="ltr" translate="no">compute.  regionOperations.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  use</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslCertificates.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslCertificates.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslCertificates.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslCertificates.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslCertificates.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslCertificates.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslCertificates.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslCertificates.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslPolicies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslPolicies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslPolicies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslPolicies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.regionSslPolicies.get</code></li>
<li><code dir="ltr" translate="no">compute.regionSslPolicies.list</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslPolicies.  listAvailableFeatures</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslPolicies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslPolicies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionSslPolicies.  update</code></li>
<li><code dir="ltr" translate="no">compute.regionSslPolicies.use</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  setUrlMap</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  use</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  setSslCertificates</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  setUrlMap</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  update</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  use</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  attach</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  use</code></li>
<li><code dir="ltr" translate="no">compute.regionUrlMaps.create</code></li>
<li><code dir="ltr" translate="no">compute.  regionUrlMaps.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.regionUrlMaps.delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionUrlMaps.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.regionUrlMaps.get</code></li>
<li><code dir="ltr" translate="no">compute.  regionUrlMaps.  invalidateCache</code></li>
<li><code dir="ltr" translate="no">compute.regionUrlMaps.list</code></li>
<li><code dir="ltr" translate="no">compute.  regionUrlMaps.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionUrlMaps.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.regionUrlMaps.update</code></li>
<li><code dir="ltr" translate="no">compute.regionUrlMaps.use</code></li>
<li><code dir="ltr" translate="no">compute.regionUrlMaps.validate</code></li>
<li><code dir="ltr" translate="no">compute.regions.get</code></li>
<li><code dir="ltr" translate="no">compute.regions.list</code></li>
<li><code dir="ltr" translate="no">compute.reservationBlocks.get</code></li>
<li><code dir="ltr" translate="no">compute.reservationBlocks.list</code></li>
<li><code dir="ltr" translate="no">compute.  reservationBlocks.  performMaintenance</code></li>
<li><code dir="ltr" translate="no">compute.reservationSlots.get</code></li>
<li><code dir="ltr" translate="no">compute.reservationSlots.list</code></li>
<li><code dir="ltr" translate="no">compute.  reservationSlots.  update</code></li>
<li><code dir="ltr" translate="no">compute.  reservationSubBlocks.  get</code></li>
<li><code dir="ltr" translate="no">compute.  reservationSubBlocks.  list</code></li>
<li><code dir="ltr" translate="no">compute.  reservationSubBlocks.  performMaintenance</code></li>
<li><code dir="ltr" translate="no">compute.  reservationSubBlocks.  reportFaulty</code></li>
<li><code dir="ltr" translate="no">compute.reservations.create</code></li>
<li><code dir="ltr" translate="no">compute.  reservations.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.reservations.delete</code></li>
<li><code dir="ltr" translate="no">compute.  reservations.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.reservations.get</code></li>
<li><code dir="ltr" translate="no">compute.reservations.list</code></li>
<li><code dir="ltr" translate="no">compute.  reservations.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  reservations.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  reservations.  performMaintenance</code></li>
<li><code dir="ltr" translate="no">compute.reservations.resize</code></li>
<li><code dir="ltr" translate="no">compute.reservations.update</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.resourcePolicies.get</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.resourcePolicies.list</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  update</code></li>
<li><code dir="ltr" translate="no">compute.resourcePolicies.use</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.rolloutPlans.create</code></li>
<li><code dir="ltr" translate="no">compute.rolloutPlans.delete</code></li>
<li><code dir="ltr" translate="no">compute.rolloutPlans.get</code></li>
<li><code dir="ltr" translate="no">compute.rolloutPlans.list</code></li>
<li><code dir="ltr" translate="no">compute.rollouts.cancel</code></li>
<li><code dir="ltr" translate="no">compute.rollouts.delete</code></li>
<li><code dir="ltr" translate="no">compute.rollouts.get</code></li>
<li><code dir="ltr" translate="no">compute.rollouts.list</code></li>
<li><code dir="ltr" translate="no">compute.routers.create</code></li>
<li><code dir="ltr" translate="no">compute.  routers.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.routers.delete</code></li>
<li><code dir="ltr" translate="no">compute.  routers.  deleteRoutePolicy</code></li>
<li><code dir="ltr" translate="no">compute.  routers.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.routers.get</code></li>
<li><code dir="ltr" translate="no">compute.routers.getRoutePolicy</code></li>
<li><code dir="ltr" translate="no">compute.routers.list</code></li>
<li><code dir="ltr" translate="no">compute.routers.listBgpRoutes</code></li>
<li><code dir="ltr" translate="no">compute.  routers.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  routers.  listRoutePolicies</code></li>
<li><code dir="ltr" translate="no">compute.  routers.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.routers.update</code></li>
<li><code dir="ltr" translate="no">compute.  routers.  updateRoutePolicy</code></li>
<li><code dir="ltr" translate="no">compute.routers.use</code></li>
<li><code dir="ltr" translate="no">compute.routes.create</code></li>
<li><code dir="ltr" translate="no">compute.  routes.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.routes.delete</code></li>
<li><code dir="ltr" translate="no">compute.  routes.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.routes.get</code></li>
<li><code dir="ltr" translate="no">compute.routes.list</code></li>
<li><code dir="ltr" translate="no">compute.  routes.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.routes.listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  addAssociation</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  copyRules</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.securityPolicies.get</code></li>
<li><code dir="ltr" translate="no">compute.securityPolicies.list</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.securityPolicies.move</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  removeAssociation</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  securityPolicies.  update</code></li>
<li><code dir="ltr" translate="no">compute.securityPolicies.use</code></li>
<li><code dir="ltr" translate="no">compute.  serviceAttachments.  create</code></li>
<li><code dir="ltr" translate="no">compute.  serviceAttachments.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  serviceAttachments.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  serviceAttachments.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.serviceAttachments.get</code></li>
<li><code dir="ltr" translate="no">compute.  serviceAttachments.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  serviceAttachments.  list</code></li>
<li><code dir="ltr" translate="no">compute.  serviceAttachments.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  serviceAttachments.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  serviceAttachments.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  serviceAttachments.  update</code></li>
<li><code dir="ltr" translate="no">compute.serviceAttachments.use</code></li>
<li><code dir="ltr" translate="no">compute.snapshotGroups.create</code></li>
<li><code dir="ltr" translate="no">compute.snapshotGroups.delete</code></li>
<li><code dir="ltr" translate="no">compute.snapshotGroups.get</code></li>
<li><code dir="ltr" translate="no">compute.  snapshotGroups.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.snapshotGroups.list</code></li>
<li><code dir="ltr" translate="no">compute.  snapshotGroups.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  snapshotGroups.  useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.snapshotSettings.get</code></li>
<li><code dir="ltr" translate="no">compute.  snapshotSettings.  update</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.create</code></li>
<li><code dir="ltr" translate="no">compute.  snapshots.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.delete</code></li>
<li><code dir="ltr" translate="no">compute.  snapshots.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.get</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.list</code></li>
<li><code dir="ltr" translate="no">compute.  snapshots.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  snapshots.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.updateKmsKey</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.useReadOnly</code></li>
<li><code dir="ltr" translate="no">compute.spotAssistants.get</code></li>
<li><code dir="ltr" translate="no">compute.sslCertificates.create</code></li>
<li><code dir="ltr" translate="no">compute.  sslCertificates.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.sslCertificates.delete</code></li>
<li><code dir="ltr" translate="no">compute.  sslCertificates.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.sslCertificates.get</code></li>
<li><code dir="ltr" translate="no">compute.sslCertificates.list</code></li>
<li><code dir="ltr" translate="no">compute.  sslCertificates.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  sslCertificates.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.sslPolicies.create</code></li>
<li><code dir="ltr" translate="no">compute.  sslPolicies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.sslPolicies.delete</code></li>
<li><code dir="ltr" translate="no">compute.  sslPolicies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.sslPolicies.get</code></li>
<li><code dir="ltr" translate="no">compute.sslPolicies.list</code></li>
<li><code dir="ltr" translate="no">compute.  sslPolicies.  listAvailableFeatures</code></li>
<li><code dir="ltr" translate="no">compute.  sslPolicies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  sslPolicies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.sslPolicies.update</code></li>
<li><code dir="ltr" translate="no">compute.sslPolicies.use</code></li>
<li><code dir="ltr" translate="no">compute.storagePools.create</code></li>
<li><code dir="ltr" translate="no">compute.  storagePools.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.storagePools.delete</code></li>
<li><code dir="ltr" translate="no">compute.  storagePools.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.storagePools.get</code></li>
<li><code dir="ltr" translate="no">compute.  storagePools.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.storagePools.list</code></li>
<li><code dir="ltr" translate="no">compute.  storagePools.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  storagePools.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  storagePools.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.storagePools.update</code></li>
<li><code dir="ltr" translate="no">compute.storagePools.use</code></li>
<li><code dir="ltr" translate="no">compute.subnetworks.create</code></li>
<li><code dir="ltr" translate="no">compute.  subnetworks.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.subnetworks.delete</code></li>
<li><code dir="ltr" translate="no">compute.  subnetworks.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  subnetworks.  expandIpCidrRange</code></li>
<li><code dir="ltr" translate="no">compute.subnetworks.get</code></li>
<li><code dir="ltr" translate="no">compute.  subnetworks.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.subnetworks.list</code></li>
<li><code dir="ltr" translate="no">compute.  subnetworks.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  subnetworks.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.subnetworks.mirror</code></li>
<li><code dir="ltr" translate="no">compute.  subnetworks.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  subnetworks.  setPrivateIpGoogleAccess</code></li>
<li><code dir="ltr" translate="no">compute.subnetworks.update</code></li>
<li><code dir="ltr" translate="no">compute.subnetworks.use</code></li>
<li><code dir="ltr" translate="no">compute.  subnetworks.  useExternalIp</code></li>
<li><code dir="ltr" translate="no">compute.  subnetworks.  usePeerMigration</code></li>
<li><code dir="ltr" translate="no">compute.  targetGrpcProxies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  targetGrpcProxies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  targetGrpcProxies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  targetGrpcProxies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.targetGrpcProxies.get</code></li>
<li><code dir="ltr" translate="no">compute.targetGrpcProxies.list</code></li>
<li><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  targetGrpcProxies.  update</code></li>
<li><code dir="ltr" translate="no">compute.targetGrpcProxies.use</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpProxies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpProxies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpProxies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpProxies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.targetHttpProxies.get</code></li>
<li><code dir="ltr" translate="no">compute.targetHttpProxies.list</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpProxies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpProxies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpProxies.  setUrlMap</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpProxies.  update</code></li>
<li><code dir="ltr" translate="no">compute.targetHttpProxies.use</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.targetHttpsProxies.get</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  list</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  setCertificateMap</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  setQuicOverride</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  setSslCertificates</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  setSslPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  setUrlMap</code></li>
<li><code dir="ltr" translate="no">compute.  targetHttpsProxies.  update</code></li>
<li><code dir="ltr" translate="no">compute.targetHttpsProxies.use</code></li>
<li><code dir="ltr" translate="no">compute.targetInstances.create</code></li>
<li><code dir="ltr" translate="no">compute.  targetInstances.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.targetInstances.delete</code></li>
<li><code dir="ltr" translate="no">compute.  targetInstances.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.targetInstances.get</code></li>
<li><code dir="ltr" translate="no">compute.targetInstances.list</code></li>
<li><code dir="ltr" translate="no">compute.  targetInstances.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  targetInstances.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  targetInstances.  setSecurityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.targetInstances.use</code></li>
<li><code dir="ltr" translate="no">compute.  targetPools.  addHealthCheck</code></li>
<li><code dir="ltr" translate="no">compute.  targetPools.  addInstance</code></li>
<li><code dir="ltr" translate="no">compute.targetPools.create</code></li>
<li><code dir="ltr" translate="no">compute.  targetPools.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.targetPools.delete</code></li>
<li><code dir="ltr" translate="no">compute.  targetPools.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.targetPools.get</code></li>
<li><code dir="ltr" translate="no">compute.targetPools.list</code></li>
<li><code dir="ltr" translate="no">compute.  targetPools.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  targetPools.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  targetPools.  removeHealthCheck</code></li>
<li><code dir="ltr" translate="no">compute.  targetPools.  removeInstance</code></li>
<li><code dir="ltr" translate="no">compute.  targetPools.  setSecurityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.targetPools.update</code></li>
<li><code dir="ltr" translate="no">compute.targetPools.use</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.targetSslProxies.get</code></li>
<li><code dir="ltr" translate="no">compute.targetSslProxies.list</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  setBackendService</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  setCertificateMap</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  setProxyHeader</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  setSslCertificates</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  setSslPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  targetSslProxies.  update</code></li>
<li><code dir="ltr" translate="no">compute.targetSslProxies.use</code></li>
<li><code dir="ltr" translate="no">compute.  targetTcpProxies.  attach</code></li>
<li><code dir="ltr" translate="no">compute.  targetTcpProxies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  targetTcpProxies.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  targetTcpProxies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  targetTcpProxies.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.targetTcpProxies.get</code></li>
<li><code dir="ltr" translate="no">compute.targetTcpProxies.list</code></li>
<li><code dir="ltr" translate="no">compute.  targetTcpProxies.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  targetTcpProxies.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  targetTcpProxies.  update</code></li>
<li><code dir="ltr" translate="no">compute.targetTcpProxies.use</code></li>
<li><code dir="ltr" translate="no">compute.  targetVpnGateways.  create</code></li>
<li><code dir="ltr" translate="no">compute.  targetVpnGateways.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  targetVpnGateways.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  targetVpnGateways.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.targetVpnGateways.get</code></li>
<li><code dir="ltr" translate="no">compute.targetVpnGateways.list</code></li>
<li><code dir="ltr" translate="no">compute.  targetVpnGateways.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  targetVpnGateways.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  targetVpnGateways.  setLabels</code></li>
<li><code dir="ltr" translate="no">compute.targetVpnGateways.use</code></li>
<li><code dir="ltr" translate="no">compute.urlMaps.create</code></li>
<li><code dir="ltr" translate="no">compute.  urlMaps.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.urlMaps.delete</code></li>
<li><code dir="ltr" translate="no">compute.  urlMaps.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.urlMaps.get</code></li>
<li><code dir="ltr" translate="no">compute.  urlMaps.  invalidateCache</code></li>
<li><code dir="ltr" translate="no">compute.urlMaps.list</code></li>
<li><code dir="ltr" translate="no">compute.  urlMaps.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  urlMaps.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.urlMaps.update</code></li>
<li><code dir="ltr" translate="no">compute.urlMaps.use</code></li>
<li><code dir="ltr" translate="no">compute.urlMaps.validate</code></li>
<li><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  get</code></li>
<li><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  list</code></li>
<li><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  update</code></li>
<li><code dir="ltr" translate="no">compute.vpnGateways.create</code></li>
<li><code dir="ltr" translate="no">compute.  vpnGateways.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.vpnGateways.delete</code></li>
<li><code dir="ltr" translate="no">compute.  vpnGateways.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.vpnGateways.get</code></li>
<li><code dir="ltr" translate="no">compute.vpnGateways.list</code></li>
<li><code dir="ltr" translate="no">compute.  vpnGateways.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  vpnGateways.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.vpnGateways.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.vpnGateways.use</code></li>
<li><code dir="ltr" translate="no">compute.vpnTunnels.create</code></li>
<li><code dir="ltr" translate="no">compute.  vpnTunnels.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.vpnTunnels.delete</code></li>
<li><code dir="ltr" translate="no">compute.  vpnTunnels.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.vpnTunnels.get</code></li>
<li><code dir="ltr" translate="no">compute.vpnTunnels.list</code></li>
<li><code dir="ltr" translate="no">compute.  vpnTunnels.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  vpnTunnels.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.vpnTunnels.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.wireGroups.create</code></li>
<li><code dir="ltr" translate="no">compute.wireGroups.delete</code></li>
<li><code dir="ltr" translate="no">compute.wireGroups.get</code></li>
<li><code dir="ltr" translate="no">compute.wireGroups.list</code></li>
<li><code dir="ltr" translate="no">compute.wireGroups.update</code></li>
<li><code dir="ltr" translate="no">compute.zoneOperations.delete</code></li>
<li><code dir="ltr" translate="no">compute.zoneOperations.get</code></li>
<li><code dir="ltr" translate="no">compute.  zoneOperations.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.zoneOperations.list</code></li>
<li><code dir="ltr" translate="no">compute.  zoneOperations.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.zones.get</code></li>
<li><code dir="ltr" translate="no">compute.zones.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.*</code></p>
<ul>
<li><code dir="ltr" translate="no">notebooks.environments.create</code></li>
<li><code dir="ltr" translate="no">notebooks.environments.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.environments.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  environments.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.environments.list</code></li>
<li><code dir="ltr" translate="no">notebooks.  environments.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.create</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  executions.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.list</code></li>
<li><code dir="ltr" translate="no">notebooks.  executions.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  checkUpgradability</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.create</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.diagnose</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.get</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.getHealth</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.list</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.reset</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  setAccelerator</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.setLabels</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  setMachineType</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.start</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.stop</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.update</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  updateConfig</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  updateShieldInstanceConfig</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.upgrade</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.use</code></li>
<li><code dir="ltr" translate="no">notebooks.locations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.locations.list</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.cancel</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.list</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.create</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.diagnose</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  runtimes.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.list</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.reset</code></li>
<li><code dir="ltr" translate="no">notebooks.  runtimes.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.start</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.stop</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.switch</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.update</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.upgrade</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.create</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  schedules.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.list</code></li>
<li><code dir="ltr" translate="no">notebooks.  schedules.  setIamPolicy</code></li>
</ul>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  analyze</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.  effectivepolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.groups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">serviceusage.groups.list</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listExpandedMembers</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listMembers</code></li>
</ul>
<p><code dir="ltr" translate="no">serviceusage.quotas.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.values.test</code></p></td>
</tr>
<tr class="odd">
<td><h4 id="notebooks.legacyViewer" class="role-title add-link" data-text="Notebooks Legacy Viewer" tabindex="-1">Notebooks Legacy Viewer</h4>
<p>( <code dir="ltr" translate="no">roles/  notebooks.legacyViewer</code> )</p>
<p>Read-only access to Notebooks all resources through compute API.</p></td>
<td><p><code dir="ltr" translate="no">compute.acceleratorTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.addresses.get</code></p>
<p><code dir="ltr" translate="no">compute.addresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacity</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacityHistory</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.get</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.list</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.commitments.get</code></p>
<p><code dir="ltr" translate="no">compute.commitments.list</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.diskSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.diskTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.diskTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.diskTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.disks.get</code></p>
<p><code dir="ltr" translate="no">compute.disks.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.disks.list</code></p>
<p><code dir="ltr" translate="no">compute.  disks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.disks.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  get</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  list</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.get</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.get</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.list</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.futureReservations.get</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  list</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.get</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  globalOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.hosts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.hosts.get</code></li>
<li><code dir="ltr" translate="no">compute.hosts.getVersion</code></li>
<li><code dir="ltr" translate="no">compute.hosts.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.images.get</code></p>
<p><code dir="ltr" translate="no">compute.images.getFromFamily</code></p>
<p><code dir="ltr" translate="no">compute.images.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.images.list</code></p>
<p><code dir="ltr" translate="no">compute.  images.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.images.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  get</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  list</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.instanceGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.instanceGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.instanceSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.instanceTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  instanceTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instanceTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.instances.get</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getGuestAttributes</code></p>
<p><code dir="ltr" translate="no">compute.instances.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getScreenshot</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getSerialPortOutput</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getShieldedInstanceIdentity</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getShieldedVmIdentity</code></p>
<p><code dir="ltr" translate="no">compute.instances.list</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listReferrers</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.interconnectGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.interconnects.get</code></p>
<p><code dir="ltr" translate="no">compute.interconnects.list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.get</code></p>
<p><code dir="ltr" translate="no">compute.  licenseCodes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.list</code></p>
<p><code dir="ltr" translate="no">compute.licenses.get</code></p>
<p><code dir="ltr" translate="no">compute.licenses.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenses.list</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.get</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.list</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.machineTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.machineTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.machineTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.multiMig.get</code></p>
<p><code dir="ltr" translate="no">compute.multiMig.list</code></p>
<p><code dir="ltr" translate="no">compute.multiMigMembers.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.multiMigMembers.get</code></li>
<li><code dir="ltr" translate="no">compute.multiMigMembers.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networkAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.networkProfiles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.networkProfiles.get</code></li>
<li><code dir="ltr" translate="no">compute.networkProfiles.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networks.get</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getRegionEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.networks.list</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listPeeringRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.nodeTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.nodeTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.  organizations.  listAssociations</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.get</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.list</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.get</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.list</code></p>
<p><code dir="ltr" translate="no">compute.projects.get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.regions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.regions.get</code></li>
<li><code dir="ltr" translate="no">compute.regions.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.reservationBlocks.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationBlocks.list</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  list</code></p>
<p><code dir="ltr" translate="no">compute.reservations.get</code></p>
<p><code dir="ltr" translate="no">compute.reservations.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  resourcePolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.get</code></p>
<p><code dir="ltr" translate="no">compute.routers.getRoutePolicy</code></p>
<p><code dir="ltr" translate="no">compute.routers.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.listBgpRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listRoutePolicies</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.routes.get</code></p>
<p><code dir="ltr" translate="no">compute.routes.list</code></p>
<p><code dir="ltr" translate="no">compute.  routes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.routes.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.serviceAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  snapshotGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.snapshotSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  snapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  snapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.spotAssistants.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.get</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.list</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpsProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.get</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.get</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  zoneOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.zones.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.zones.get</code></li>
<li><code dir="ltr" translate="no">compute.zones.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.environments.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  environments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.environments.list</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  executions.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.list</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  checkUpgradability</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.get</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.getHealth</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.list</code></p>
<p><code dir="ltr" translate="no">notebooks.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">notebooks.locations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.operations.get</code></p>
<p><code dir="ltr" translate="no">notebooks.operations.list</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  runtimes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.list</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  schedules.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.list</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  analyze</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.  effectivepolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.groups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">serviceusage.groups.list</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listExpandedMembers</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listMembers</code></li>
</ul>
<p><code dir="ltr" translate="no">serviceusage.quotas.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.values.test</code></p></td>
</tr>
<tr class="even">
<td><h4 id="notebooks.runner" class="role-title add-link" data-text="Notebooks Runner" tabindex="-1">Notebooks Runner</h4>
<p>( <code dir="ltr" translate="no">roles/  notebooks.runner</code> )</p>
<p>Restricted access for running scheduled Notebooks.</p></td>
<td><p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.acceleratorTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.addresses.get</code></p>
<p><code dir="ltr" translate="no">compute.addresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacity</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacityHistory</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.get</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.list</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.commitments.get</code></p>
<p><code dir="ltr" translate="no">compute.commitments.list</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.diskSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.diskTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.diskTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.diskTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.disks.get</code></p>
<p><code dir="ltr" translate="no">compute.disks.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.disks.list</code></p>
<p><code dir="ltr" translate="no">compute.  disks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.disks.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  get</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  list</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.get</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.get</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.list</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.futureReservations.get</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  list</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.get</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  globalOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.hosts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.hosts.get</code></li>
<li><code dir="ltr" translate="no">compute.hosts.getVersion</code></li>
<li><code dir="ltr" translate="no">compute.hosts.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.images.get</code></p>
<p><code dir="ltr" translate="no">compute.images.getFromFamily</code></p>
<p><code dir="ltr" translate="no">compute.images.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.images.list</code></p>
<p><code dir="ltr" translate="no">compute.  images.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.images.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  get</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  list</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.instanceGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.instanceGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instanceGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.instanceSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.instanceTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  instanceTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instanceTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.instances.get</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getGuestAttributes</code></p>
<p><code dir="ltr" translate="no">compute.instances.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getScreenshot</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getSerialPortOutput</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getShieldedInstanceIdentity</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  getShieldedVmIdentity</code></p>
<p><code dir="ltr" translate="no">compute.instances.list</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listReferrers</code></p>
<p><code dir="ltr" translate="no">compute.  instances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.interconnectGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.interconnects.get</code></p>
<p><code dir="ltr" translate="no">compute.interconnects.list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.get</code></p>
<p><code dir="ltr" translate="no">compute.  licenseCodes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.list</code></p>
<p><code dir="ltr" translate="no">compute.licenses.get</code></p>
<p><code dir="ltr" translate="no">compute.licenses.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenses.list</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.get</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.list</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.machineTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.machineTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.machineTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.multiMig.get</code></p>
<p><code dir="ltr" translate="no">compute.multiMig.list</code></p>
<p><code dir="ltr" translate="no">compute.multiMigMembers.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.multiMigMembers.get</code></li>
<li><code dir="ltr" translate="no">compute.multiMigMembers.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networkAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.networkProfiles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.networkProfiles.get</code></li>
<li><code dir="ltr" translate="no">compute.networkProfiles.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networks.get</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getRegionEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.networks.list</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listPeeringRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.nodeTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.nodeTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.  organizations.  listAssociations</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.get</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.list</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.get</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.list</code></p>
<p><code dir="ltr" translate="no">compute.projects.get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.regions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.regions.get</code></li>
<li><code dir="ltr" translate="no">compute.regions.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.reservationBlocks.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationBlocks.list</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  list</code></p>
<p><code dir="ltr" translate="no">compute.reservations.get</code></p>
<p><code dir="ltr" translate="no">compute.reservations.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  resourcePolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.get</code></p>
<p><code dir="ltr" translate="no">compute.routers.getRoutePolicy</code></p>
<p><code dir="ltr" translate="no">compute.routers.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.listBgpRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listRoutePolicies</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.routes.get</code></p>
<p><code dir="ltr" translate="no">compute.routes.list</code></p>
<p><code dir="ltr" translate="no">compute.  routes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.routes.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.serviceAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  snapshotGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.snapshotSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  snapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  snapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.spotAssistants.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.get</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.list</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpsProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.get</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.get</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  zoneOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.zones.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.zones.get</code></li>
<li><code dir="ltr" translate="no">compute.zones.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.environments.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  environments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.environments.list</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.create</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  executions.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.executions.list</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  checkUpgradability</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.create</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.get</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.getHealth</code></p>
<p><code dir="ltr" translate="no">notebooks.  instances.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.instances.list</code></p>
<p><code dir="ltr" translate="no">notebooks.locations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">notebooks.locations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.locations.list</code></li>
</ul>
<p><code dir="ltr" translate="no">notebooks.operations.get</code></p>
<p><code dir="ltr" translate="no">notebooks.operations.list</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.create</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  runtimes.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.runtimes.list</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.create</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.get</code></p>
<p><code dir="ltr" translate="no">notebooks.  schedules.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">notebooks.schedules.list</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  analyze</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.  effectivepolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.groups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">serviceusage.groups.list</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listExpandedMembers</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listMembers</code></li>
</ul>
<p><code dir="ltr" translate="no">serviceusage.quotas.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.values.test</code></p></td>
</tr>
</tbody>
</table>

### Service agent roles

Service agent roles should only be granted to [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><h4 id="notebooks.serviceAgent" class="role-title add-link" data-text="AI Platform Notebooks Service Agent" tabindex="-1">AI Platform Notebooks Service Agent</h4>
<p>( <code dir="ltr" translate="no">roles/  notebooks.serviceAgent</code> )</p>
<p>Provide access for notebooks service agent to manage notebook instances in user projects</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code dir="ltr" translate="no">aiplatform.customJobs.cancel</code></p>
<p><code dir="ltr" translate="no">aiplatform.customJobs.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.customJobs.get</code></p>
<p><code dir="ltr" translate="no">aiplatform.customJobs.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  create</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  get</code></li>
<li><code dir="ltr" translate="no">aiplatform.  notebookExecutionJobs.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">aiplatform.  notebookRuntimes.  get</code></p>
<p><code dir="ltr" translate="no">aiplatform.operations.list</code></p>
<p><code dir="ltr" translate="no">aiplatform.pipelineJobs.create</code></p>
<p><code dir="ltr" translate="no">aiplatform.schedules.*</code></p>
<ul>
<li><code dir="ltr" translate="no">aiplatform.schedules.create</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.delete</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.get</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.list</code></li>
<li><code dir="ltr" translate="no">aiplatform.schedules.update</code></li>
</ul>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  createForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  createForComputeInstance</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  deleteForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  deleteForComputeInstance</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  fetchForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  getForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  list</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  triggerBackupForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  triggerBackupForComputeInstance</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  updateForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlanAssociations.  updateForComputeInstance</code></p>
<p><code dir="ltr" translate="no">backupdr.backupPlans.get</code></p>
<p><code dir="ltr" translate="no">backupdr.backupPlans.list</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlans.  useForComputeDisk</code></p>
<p><code dir="ltr" translate="no">backupdr.  backupPlans.  useForComputeInstance</code></p>
<p><code dir="ltr" translate="no">backupdr.backupVaults.get</code></p>
<p><code dir="ltr" translate="no">backupdr.backupVaults.list</code></p>
<p><code dir="ltr" translate="no">backupdr.locations.list</code></p>
<p><code dir="ltr" translate="no">backupdr.operations.get</code></p>
<p><code dir="ltr" translate="no">backupdr.operations.list</code></p>
<p><code dir="ltr" translate="no">backupdr.  serviceConfig.  initialize</code></p>
<p><code dir="ltr" translate="no">compute.acceleratorTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.acceleratorTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  addresses.  createInternal</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  deleteInternal</code></p>
<p><code dir="ltr" translate="no">compute.addresses.get</code></p>
<p><code dir="ltr" translate="no">compute.addresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  addresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.addresses.use</code></p>
<p><code dir="ltr" translate="no">compute.addresses.useInternal</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacity</code></p>
<p><code dir="ltr" translate="no">compute.advice.capacityHistory</code></p>
<p><code dir="ltr" translate="no">compute.autoscalers.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.autoscalers.create</code></li>
<li><code dir="ltr" translate="no">compute.autoscalers.delete</code></li>
<li><code dir="ltr" translate="no">compute.autoscalers.get</code></li>
<li><code dir="ltr" translate="no">compute.autoscalers.list</code></li>
<li><code dir="ltr" translate="no">compute.autoscalers.update</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.backendBuckets.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendBuckets.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.get</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.backendServices.list</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  backendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.commitments.get</code></p>
<p><code dir="ltr" translate="no">compute.commitments.list</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  commitments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.crossSiteNetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.diskSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.diskTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.diskTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.diskTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.disks.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  disks.  addResourcePolicies</code></li>
<li><code dir="ltr" translate="no">compute.disks.create</code></li>
<li><code dir="ltr" translate="no">compute.disks.createSnapshot</code></li>
<li><code dir="ltr" translate="no">compute.disks.createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.disks.delete</code></li>
<li><code dir="ltr" translate="no">compute.disks.deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.disks.get</code></li>
<li><code dir="ltr" translate="no">compute.disks.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.disks.list</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.disks.listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  removeResourcePolicies</code></li>
<li><code dir="ltr" translate="no">compute.disks.resize</code></li>
<li><code dir="ltr" translate="no">compute.disks.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.disks.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  startAsyncReplication</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  stopAsyncReplication</code></li>
<li><code dir="ltr" translate="no">compute.  disks.  stopGroupAsyncReplication</code></li>
<li><code dir="ltr" translate="no">compute.disks.update</code></li>
<li><code dir="ltr" translate="no">compute.disks.updateKmsKey</code></li>
<li><code dir="ltr" translate="no">compute.disks.use</code></li>
<li><code dir="ltr" translate="no">compute.disks.useReadOnly</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  get</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  list</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  externalVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.firewallPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.get</code></p>
<p><code dir="ltr" translate="no">compute.firewalls.list</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  firewalls.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.get</code></p>
<p><code dir="ltr" translate="no">compute.forwardingRules.list</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  forwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.futureReservations.get</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  list</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  futureReservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.get</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalAddresses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.globalAddresses.use</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  list</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  globalForwardingRules.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  attachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  create</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  detachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  get</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  list</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  globalNetworkEndpointGroups.  use</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.globalOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  globalOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.globalOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  globalPublicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.healthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  healthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.hosts.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.hosts.get</code></li>
<li><code dir="ltr" translate="no">compute.hosts.getVersion</code></li>
<li><code dir="ltr" translate="no">compute.hosts.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.httpsHealthChecks.list</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  httpsHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.images.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.images.create</code></li>
<li><code dir="ltr" translate="no">compute.  images.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.images.delete</code></li>
<li><code dir="ltr" translate="no">compute.  images.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.images.deprecate</code></li>
<li><code dir="ltr" translate="no">compute.images.get</code></li>
<li><code dir="ltr" translate="no">compute.images.getFromFamily</code></li>
<li><code dir="ltr" translate="no">compute.images.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.images.list</code></li>
<li><code dir="ltr" translate="no">compute.  images.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.images.listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.images.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.images.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.images.update</code></li>
<li><code dir="ltr" translate="no">compute.images.useReadOnly</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  instanceGroupManagers.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  create</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  get</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  list</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  update</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroupManagers.  use</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.instanceGroups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.instanceGroups.create</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroups.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.delete</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroups.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.get</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.list</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroups.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  instanceGroups.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.update</code></li>
<li><code dir="ltr" translate="no">compute.instanceGroups.use</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.instanceSettings.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.instanceSettings.get</code></li>
<li><code dir="ltr" translate="no">compute.  instanceSettings.  update</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.instanceTemplates.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  instanceTemplates.  create</code></li>
<li><code dir="ltr" translate="no">compute.  instanceTemplates.  delete</code></li>
<li><code dir="ltr" translate="no">compute.instanceTemplates.get</code></li>
<li><code dir="ltr" translate="no">compute.  instanceTemplates.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.instanceTemplates.list</code></li>
<li><code dir="ltr" translate="no">compute.  instanceTemplates.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instanceTemplates.  useReadOnly</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.instances.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  instances.  addAccessConfig</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  addNetworkInterface</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  addResourcePolicies</code></li>
<li><code dir="ltr" translate="no">compute.instances.attachDisk</code></li>
<li><code dir="ltr" translate="no">compute.instances.create</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.instances.delete</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  deleteAccessConfig</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  deleteNetworkInterface</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.instances.detachDisk</code></li>
<li><code dir="ltr" translate="no">compute.instances.get</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getEffectiveFirewalls</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getGuestAttributes</code></li>
<li><code dir="ltr" translate="no">compute.instances.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getScreenshot</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getSerialPortOutput</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getShieldedInstanceIdentity</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  getShieldedVmIdentity</code></li>
<li><code dir="ltr" translate="no">compute.instances.list</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  listReferrers</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.instances.osAdminLogin</code></li>
<li><code dir="ltr" translate="no">compute.instances.osLogin</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  pscInterfaceCreate</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  removeResourcePolicies</code></li>
<li><code dir="ltr" translate="no">compute.instances.reset</code></li>
<li><code dir="ltr" translate="no">compute.instances.resume</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  sendDiagnosticInterrupt</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setDeletionProtection</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setDiskAutoDelete</code></li>
<li><code dir="ltr" translate="no">compute.instances.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.instances.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setMachineResources</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setMachineType</code></li>
<li><code dir="ltr" translate="no">compute.instances.setMetadata</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setMinCpuPlatform</code></li>
<li><code dir="ltr" translate="no">compute.instances.setName</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setScheduling</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setSecurityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setServiceAccount</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setShieldedInstanceIntegrityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  setShieldedVmIntegrityPolicy</code></li>
<li><code dir="ltr" translate="no">compute.instances.setTags</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  simulateMaintenanceEvent</code></li>
<li><code dir="ltr" translate="no">compute.instances.start</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  startWithEncryptionKey</code></li>
<li><code dir="ltr" translate="no">compute.instances.stop</code></li>
<li><code dir="ltr" translate="no">compute.instances.suspend</code></li>
<li><code dir="ltr" translate="no">compute.instances.update</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateAccessConfig</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateDisplayDevice</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateNetworkInterface</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateSecurity</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateShieldedInstanceConfig</code></li>
<li><code dir="ltr" translate="no">compute.  instances.  updateShieldedVmConfig</code></li>
<li><code dir="ltr" translate="no">compute.instances.use</code></li>
<li><code dir="ltr" translate="no">compute.instances.useReadOnly</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  instantSnapshotGroups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  create</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  get</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  list</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  instantSnapshotGroups.  useReadOnly</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  create</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  delete</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  export</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.get</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.instantSnapshots.list</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  setIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  setLabels</code></p>
<p><code dir="ltr" translate="no">compute.  instantSnapshots.  useReadOnly</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachmentGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.interconnectGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectGroups.  list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnectLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  get</code></li>
<li><code dir="ltr" translate="no">compute.  interconnectRemoteLocations.  list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.interconnects.get</code></p>
<p><code dir="ltr" translate="no">compute.interconnects.list</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  interconnects.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.licenseCodes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.licenseCodes.get</code></li>
<li><code dir="ltr" translate="no">compute.  licenseCodes.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.licenseCodes.list</code></li>
<li><code dir="ltr" translate="no">compute.  licenseCodes.  setIamPolicy</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.licenses.create</code></p>
<p><code dir="ltr" translate="no">compute.licenses.delete</code></p>
<p><code dir="ltr" translate="no">compute.licenses.get</code></p>
<p><code dir="ltr" translate="no">compute.licenses.getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenses.list</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  licenses.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.licenses.setIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.licenses.update</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.create</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.delete</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.get</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.machineImages.list</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  setIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  setLabels</code></p>
<p><code dir="ltr" translate="no">compute.  machineImages.  useReadOnly</code></p>
<p><code dir="ltr" translate="no">compute.machineTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.machineTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.machineTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.multiMig.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.multiMig.create</code></li>
<li><code dir="ltr" translate="no">compute.multiMig.delete</code></li>
<li><code dir="ltr" translate="no">compute.multiMig.get</code></li>
<li><code dir="ltr" translate="no">compute.multiMig.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.multiMigMembers.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.multiMigMembers.get</code></li>
<li><code dir="ltr" translate="no">compute.multiMigMembers.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networkAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networkEdgeSecurityServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  networkEndpointGroups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  attachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  create</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  detachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  get</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  list</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  networkEndpointGroups.  use</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networkProfiles.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.networkProfiles.get</code></li>
<li><code dir="ltr" translate="no">compute.networkProfiles.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.networks.get</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  getRegionEffectiveFirewalls</code></p>
<p><code dir="ltr" translate="no">compute.networks.list</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listPeeringRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  networks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.networks.use</code></p>
<p><code dir="ltr" translate="no">compute.networks.useExternalIp</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeGroups.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.get</code></p>
<p><code dir="ltr" translate="no">compute.  nodeTemplates.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.nodeTemplates.list</code></p>
<p><code dir="ltr" translate="no">compute.nodeTypes.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.nodeTypes.get</code></li>
<li><code dir="ltr" translate="no">compute.nodeTypes.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.orgRollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.  organizations.  listAssociations</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.get</code></p>
<p><code dir="ltr" translate="no">compute.packetMirrorings.list</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  packetMirrorings.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.get</code></p>
<p><code dir="ltr" translate="no">compute.previewFeatures.list</code></p>
<p><code dir="ltr" translate="no">compute.projects.get</code></p>
<p><code dir="ltr" translate="no">compute.  projects.  setCommonInstanceMetadata</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicAdvertisedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  get</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  list</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  publicDelegatedPrefixes.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendBuckets.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionBackendServices.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionCompositeHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionFirewallPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthAggregationPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthCheckServices.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionHealthChecks.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthChecks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionHealthSources.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  attachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  create</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  delete</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  detachNetworkEndpoints</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  get</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  list</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.  regionNetworkEndpointGroups.  use</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNetworkPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionNotificationEndpoints.  list</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  regionOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.regionOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSecurityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.regionSslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionSslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionTargetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  regionUrlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.regionUrlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.regions.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.regions.get</code></li>
<li><code dir="ltr" translate="no">compute.regions.list</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.reservationBlocks.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationBlocks.list</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.get</code></p>
<p><code dir="ltr" translate="no">compute.reservationSlots.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  get</code></p>
<p><code dir="ltr" translate="no">compute.  reservationSubBlocks.  list</code></p>
<p><code dir="ltr" translate="no">compute.reservations.get</code></p>
<p><code dir="ltr" translate="no">compute.reservations.list</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  reservations.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.resourcePolicies.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  create</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  delete</code></li>
<li><code dir="ltr" translate="no">compute.resourcePolicies.get</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.resourcePolicies.list</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  update</code></li>
<li><code dir="ltr" translate="no">compute.resourcePolicies.use</code></li>
<li><code dir="ltr" translate="no">compute.  resourcePolicies.  useReadOnly</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.rolloutPlans.get</code></p>
<p><code dir="ltr" translate="no">compute.rolloutPlans.list</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.get</code></p>
<p><code dir="ltr" translate="no">compute.rollouts.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.get</code></p>
<p><code dir="ltr" translate="no">compute.routers.getRoutePolicy</code></p>
<p><code dir="ltr" translate="no">compute.routers.list</code></p>
<p><code dir="ltr" translate="no">compute.routers.listBgpRoutes</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listRoutePolicies</code></p>
<p><code dir="ltr" translate="no">compute.  routers.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.routes.get</code></p>
<p><code dir="ltr" translate="no">compute.routes.list</code></p>
<p><code dir="ltr" translate="no">compute.  routes.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.routes.listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.securityPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  securityPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.serviceAttachments.get</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  list</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  serviceAttachments.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.snapshotGroups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.snapshotGroups.create</code></li>
<li><code dir="ltr" translate="no">compute.snapshotGroups.delete</code></li>
<li><code dir="ltr" translate="no">compute.snapshotGroups.get</code></li>
<li><code dir="ltr" translate="no">compute.  snapshotGroups.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.snapshotGroups.list</code></li>
<li><code dir="ltr" translate="no">compute.  snapshotGroups.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.  snapshotGroups.  useReadOnly</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.snapshotSettings.get</code></p>
<p><code dir="ltr" translate="no">compute.snapshots.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.snapshots.create</code></li>
<li><code dir="ltr" translate="no">compute.  snapshots.  createTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.delete</code></li>
<li><code dir="ltr" translate="no">compute.  snapshots.  deleteTagBinding</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.get</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.getIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.list</code></li>
<li><code dir="ltr" translate="no">compute.  snapshots.  listEffectiveTags</code></li>
<li><code dir="ltr" translate="no">compute.  snapshots.  listTagBindings</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.setIamPolicy</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.setLabels</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.updateKmsKey</code></li>
<li><code dir="ltr" translate="no">compute.snapshots.useReadOnly</code></li>
</ul>
<p><code dir="ltr" translate="no">compute.spotAssistants.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.get</code></p>
<p><code dir="ltr" translate="no">compute.sslCertificates.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslCertificates.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.get</code></p>
<p><code dir="ltr" translate="no">compute.sslPolicies.list</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listAvailableFeatures</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  sslPolicies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.get</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.list</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  storagePools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.storagePools.use</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.get</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.list</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.subnetworks.use</code></p>
<p><code dir="ltr" translate="no">compute.  subnetworks.  useExternalIp</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetGrpcProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetGrpcProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetHttpsProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  list</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetHttpsProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.get</code></p>
<p><code dir="ltr" translate="no">compute.targetInstances.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetInstances.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.get</code></p>
<p><code dir="ltr" translate="no">compute.targetPools.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetPools.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetSslProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetSslProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.get</code></p>
<p><code dir="ltr" translate="no">compute.targetTcpProxies.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetTcpProxies.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.targetVpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  targetVpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.get</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.list</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  urlMaps.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.urlMaps.validate</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  get</code></p>
<p><code dir="ltr" translate="no">compute.  vmExtensionPolicies.  list</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnGateways.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnGateways.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.get</code></p>
<p><code dir="ltr" translate="no">compute.vpnTunnels.list</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listEffectiveTags</code></p>
<p><code dir="ltr" translate="no">compute.  vpnTunnels.  listTagBindings</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.get</code></p>
<p><code dir="ltr" translate="no">compute.wireGroups.list</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.get</code></p>
<p><code dir="ltr" translate="no">compute.  zoneOperations.  getIamPolicy</code></p>
<p><code dir="ltr" translate="no">compute.zoneOperations.list</code></p>
<p><code dir="ltr" translate="no">compute.zones.*</code></p>
<ul>
<li><code dir="ltr" translate="no">compute.zones.get</code></li>
<li><code dir="ltr" translate="no">compute.zones.list</code></li>
</ul>
<p><code dir="ltr" translate="no">dataproc.clusters.get</code></p>
<p><code dir="ltr" translate="no">dataproc.clusters.use</code></p>
<p><code dir="ltr" translate="no">dataproc.jobs.cancel</code></p>
<p><code dir="ltr" translate="no">dataproc.jobs.create</code></p>
<p><code dir="ltr" translate="no">dataproc.jobs.delete</code></p>
<p><code dir="ltr" translate="no">dataproc.jobs.get</code></p>
<p><code dir="ltr" translate="no">dataproc.jobs.list</code></p>
<p><code dir="ltr" translate="no">dataproc.jobs.update</code></p>
<p><code dir="ltr" translate="no">iam.serviceAccounts.actAs</code></p>
<p><code dir="ltr" translate="no">iam.serviceAccounts.get</code></p>
<p><code dir="ltr" translate="no">iam.  serviceAccounts.  getAccessToken</code></p>
<p><code dir="ltr" translate="no">iam.serviceAccounts.list</code></p>
<p><code dir="ltr" translate="no">ml.jobs.create</code></p>
<p><code dir="ltr" translate="no">ml.jobs.get</code></p>
<p><code dir="ltr" translate="no">ml.jobs.list</code></p>
<p><code dir="ltr" translate="no">notebooks.*</code></p>
<ul>
<li><code dir="ltr" translate="no">notebooks.environments.create</code></li>
<li><code dir="ltr" translate="no">notebooks.environments.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.environments.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  environments.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.environments.list</code></li>
<li><code dir="ltr" translate="no">notebooks.  environments.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.create</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  executions.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.executions.list</code></li>
<li><code dir="ltr" translate="no">notebooks.  executions.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  checkUpgradability</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.create</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.diagnose</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.get</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.getHealth</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.list</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.reset</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  setAccelerator</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.setLabels</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  setMachineType</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.start</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.stop</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.update</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  updateConfig</code></li>
<li><code dir="ltr" translate="no">notebooks.  instances.  updateShieldInstanceConfig</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.upgrade</code></li>
<li><code dir="ltr" translate="no">notebooks.instances.use</code></li>
<li><code dir="ltr" translate="no">notebooks.locations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.locations.list</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.cancel</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.get</code></li>
<li><code dir="ltr" translate="no">notebooks.operations.list</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.create</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.diagnose</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  runtimes.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.list</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.reset</code></li>
<li><code dir="ltr" translate="no">notebooks.  runtimes.  setIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.start</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.stop</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.switch</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.update</code></li>
<li><code dir="ltr" translate="no">notebooks.runtimes.upgrade</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.create</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.delete</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.get</code></li>
<li><code dir="ltr" translate="no">notebooks.  schedules.  getIamPolicy</code></li>
<li><code dir="ltr" translate="no">notebooks.schedules.list</code></li>
<li><code dir="ltr" translate="no">notebooks.  schedules.  setIamPolicy</code></li>
</ul>
<p><code dir="ltr" translate="no">resourcemanager.projects.get</code></p>
<p><code dir="ltr" translate="no">resourcemanager.projects.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  analyze</code></p>
<p><code dir="ltr" translate="no">serviceusage.  consumerpolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.  effectivepolicy.  get</code></p>
<p><code dir="ltr" translate="no">serviceusage.groups.*</code></p>
<ul>
<li><code dir="ltr" translate="no">serviceusage.groups.list</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listExpandedMembers</code></li>
<li><code dir="ltr" translate="no">serviceusage.  groups.  listMembers</code></li>
</ul>
<p><code dir="ltr" translate="no">serviceusage.quotas.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.get</code></p>
<p><code dir="ltr" translate="no">serviceusage.services.list</code></p>
<p><code dir="ltr" translate="no">serviceusage.values.test</code></p></td>
</tr>
</tbody>
</table>

## Basic roles

The older Google Cloud [basic roles](https://docs.cloud.google.com/iam/docs/roles-overview#basic) are common to all Google Cloud services. These roles are Owner, Editor, and Viewer.

The basic roles provide permissions across Google Cloud, not just for Agent Platform Workbench. For this reason, you should use Agent Platform Workbench roles whenever possible.

## Custom roles

If the predefined IAM roles for Agent Platform Workbench don't meet your needs, you can define custom roles. Custom roles enable you to choose a specific set of permissions, create your own role with those permissions, and grant the role to users in your organization. For more information, see [Understanding IAM custom roles](https://docs.cloud.google.com/iam/docs/understanding-custom-roles) .

## Project-level access versus resource-level policies

A resource inherits all policies from its [ancestry](https://docs.cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy) . A [policy](https://docs.cloud.google.com/iam/docs/policies#structure) set at the resource level doesn't affect project-level policies. You can use project-level access and resource-level policies to customize permissions. For example, you can grant users `roles/notebooks.viewer` permissions at the project level so that they can view all Agent Platform Workbench resources in the project, and then you can grant each user `roles/notebooks.admin` permissions on a specific Agent Platform Workbench instance so that they have all of the `admin` abilities to administer that instance.

Not all Agent Platform Workbench predefined roles and resources support resource-level policies. To see which roles can be used on which resources, [view the descriptions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/iam#iam-roles) for each role.

Changes to the ability to access a resource take time to propagate. For more information, see [Access change propagation](https://docs.cloud.google.com/iam/docs/access-change-propagation) .

## What's next

  - [Grant a principal access to a Agent Platform Workbench instance.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access)

  - [Grant a principal access to JupyterLab.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-access-jupyterlab)

  - Learn more about [IAM](https://docs.cloud.google.com/iam/docs) .

  - Learn how to [create and manage custom IAM roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) .
