---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/iam
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/iam
title: Agent Platform Workbench instances access control
description: Grant a principal access to a Agent Platform Workbench instance and JupyterLab interface
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
<td>Notebooks Admin
<p>( <code>roles/ notebooks.admin</code> )</p>
<p>Full access to Notebooks, all resources.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Instance</li>
</ul></td>
<td><p><code>aiplatform. notebookExecutionJobs.*</code></p>
<ul>
<li><code>aiplatform. notebookExecutionJobs. create</code></li>
<li><code>aiplatform. notebookExecutionJobs. delete</code></li>
<li><code>aiplatform. notebookExecutionJobs. get</code></li>
<li><code>aiplatform. notebookExecutionJobs. list</code></li>
</ul>
<p><code>aiplatform.operations.list</code></p>
<p><code>aiplatform.pipelineJobs.create</code></p>
<p><code>aiplatform.schedules.*</code></p>
<ul>
<li><code>aiplatform.schedules.create</code></li>
<li><code>aiplatform.schedules.delete</code></li>
<li><code>aiplatform.schedules.get</code></li>
<li><code>aiplatform.schedules.list</code></li>
<li><code>aiplatform.schedules.update</code></li>
</ul>
<p><code>compute.acceleratorTypes.*</code></p>
<ul>
<li><code>compute.acceleratorTypes.get</code></li>
<li><code>compute.acceleratorTypes.list</code></li>
</ul>
<p><code>compute.addresses.get</code></p>
<p><code>compute.addresses.list</code></p>
<p><code>compute. addresses. listEffectiveTags</code></p>
<p><code>compute. addresses. listTagBindings</code></p>
<p><code>compute.advice.capacity</code></p>
<p><code>compute.advice.capacityHistory</code></p>
<p><code>compute.autoscalers.get</code></p>
<p><code>compute.autoscalers.list</code></p>
<p><code>compute.backendBuckets.get</code></p>
<p><code>compute. backendBuckets. getIamPolicy</code></p>
<p><code>compute.backendBuckets.list</code></p>
<p><code>compute. backendBuckets. listEffectiveTags</code></p>
<p><code>compute. backendBuckets. listTagBindings</code></p>
<p><code>compute.backendServices.get</code></p>
<p><code>compute. backendServices. getIamPolicy</code></p>
<p><code>compute.backendServices.list</code></p>
<p><code>compute. backendServices. listEffectiveTags</code></p>
<p><code>compute. backendServices. listTagBindings</code></p>
<p><code>compute.commitments.get</code></p>
<p><code>compute.commitments.list</code></p>
<p><code>compute. commitments. listEffectiveTags</code></p>
<p><code>compute. commitments. listTagBindings</code></p>
<p><code>compute.crossSiteNetworks.get</code></p>
<p><code>compute.crossSiteNetworks.list</code></p>
<p><code>compute.diskSettings.get</code></p>
<p><code>compute.diskTypes.*</code></p>
<ul>
<li><code>compute.diskTypes.get</code></li>
<li><code>compute.diskTypes.list</code></li>
</ul>
<p><code>compute.disks.get</code></p>
<p><code>compute.disks.getIamPolicy</code></p>
<p><code>compute.disks.list</code></p>
<p><code>compute. disks. listEffectiveTags</code></p>
<p><code>compute.disks.listTagBindings</code></p>
<p><code>compute. externalVpnGateways. get</code></p>
<p><code>compute. externalVpnGateways. list</code></p>
<p><code>compute. externalVpnGateways. listEffectiveTags</code></p>
<p><code>compute. externalVpnGateways. listTagBindings</code></p>
<p><code>compute.firewallPolicies.get</code></p>
<p><code>compute. firewallPolicies. getIamPolicy</code></p>
<p><code>compute.firewallPolicies.list</code></p>
<p><code>compute. firewallPolicies. listEffectiveTags</code></p>
<p><code>compute. firewallPolicies. listTagBindings</code></p>
<p><code>compute.firewalls.get</code></p>
<p><code>compute.firewalls.list</code></p>
<p><code>compute. firewalls. listEffectiveTags</code></p>
<p><code>compute. firewalls. listTagBindings</code></p>
<p><code>compute.forwardingRules.get</code></p>
<p><code>compute.forwardingRules.list</code></p>
<p><code>compute. forwardingRules. listEffectiveTags</code></p>
<p><code>compute. forwardingRules. listTagBindings</code></p>
<p><code>compute.futureReservations.get</code></p>
<p><code>compute. futureReservations. getIamPolicy</code></p>
<p><code>compute. futureReservations. list</code></p>
<p><code>compute. futureReservations. listEffectiveTags</code></p>
<p><code>compute. futureReservations. listTagBindings</code></p>
<p><code>compute.globalAddresses.get</code></p>
<p><code>compute.globalAddresses.list</code></p>
<p><code>compute. globalAddresses. listEffectiveTags</code></p>
<p><code>compute. globalAddresses. listTagBindings</code></p>
<p><code>compute. globalForwardingRules. get</code></p>
<p><code>compute. globalForwardingRules. list</code></p>
<p><code>compute. globalForwardingRules. listEffectiveTags</code></p>
<p><code>compute. globalForwardingRules. listTagBindings</code></p>
<p><code>compute. globalFrontendSettings. get</code></p>
<p><code>compute. globalNetworkEndpointGroups. get</code></p>
<p><code>compute. globalNetworkEndpointGroups. list</code></p>
<p><code>compute. globalNetworkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. globalNetworkEndpointGroups. listTagBindings</code></p>
<p><code>compute.globalOperations.get</code></p>
<p><code>compute. globalOperations. getIamPolicy</code></p>
<p><code>compute.globalOperations.list</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. get</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. list</code></p>
<p><code>compute.healthChecks.get</code></p>
<p><code>compute.healthChecks.list</code></p>
<p><code>compute. healthChecks. listEffectiveTags</code></p>
<p><code>compute. healthChecks. listTagBindings</code></p>
<p><code>compute.hosts.*</code></p>
<ul>
<li><code>compute.hosts.get</code></li>
<li><code>compute.hosts.getVersion</code></li>
<li><code>compute.hosts.list</code></li>
</ul>
<p><code>compute.httpHealthChecks.get</code></p>
<p><code>compute.httpHealthChecks.list</code></p>
<p><code>compute. httpHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpHealthChecks. listTagBindings</code></p>
<p><code>compute.httpsHealthChecks.get</code></p>
<p><code>compute.httpsHealthChecks.list</code></p>
<p><code>compute. httpsHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpsHealthChecks. listTagBindings</code></p>
<p><code>compute.images.get</code></p>
<p><code>compute.images.getFromFamily</code></p>
<p><code>compute.images.getIamPolicy</code></p>
<p><code>compute.images.list</code></p>
<p><code>compute. images. listEffectiveTags</code></p>
<p><code>compute.images.listTagBindings</code></p>
<p><code>compute. instanceGroupManagers. get</code></p>
<p><code>compute. instanceGroupManagers. list</code></p>
<p><code>compute. instanceGroupManagers. listEffectiveTags</code></p>
<p><code>compute. instanceGroupManagers. listTagBindings</code></p>
<p><code>compute.instanceGroups.get</code></p>
<p><code>compute.instanceGroups.list</code></p>
<p><code>compute. instanceGroups. listEffectiveTags</code></p>
<p><code>compute. instanceGroups. listTagBindings</code></p>
<p><code>compute.instanceSettings.get</code></p>
<p><code>compute.instanceTemplates.get</code></p>
<p><code>compute. instanceTemplates. getIamPolicy</code></p>
<p><code>compute.instanceTemplates.list</code></p>
<p><code>compute.instances.get</code></p>
<p><code>compute. instances. getEffectiveFirewalls</code></p>
<p><code>compute. instances. getGuestAttributes</code></p>
<p><code>compute.instances.getIamPolicy</code></p>
<p><code>compute. instances. getScreenshot</code></p>
<p><code>compute. instances. getSerialPortOutput</code></p>
<p><code>compute. instances. getShieldedInstanceIdentity</code></p>
<p><code>compute. instances. getShieldedVmIdentity</code></p>
<p><code>compute. instances. getVmExtensionState</code></p>
<p><code>compute.instances.list</code></p>
<p><code>compute. instances. listEffectiveTags</code></p>
<p><code>compute. instances. listReferrers</code></p>
<p><code>compute. instances. listTagBindings</code></p>
<p><code>compute. instances. listVmExtensionStates</code></p>
<p><code>compute.instances.troubleshoot</code></p>
<p><code>compute. instantSnapshotGroups. get</code></p>
<p><code>compute. instantSnapshotGroups. getIamPolicy</code></p>
<p><code>compute. instantSnapshotGroups. list</code></p>
<p><code>compute.instantSnapshots.get</code></p>
<p><code>compute. instantSnapshots. getIamPolicy</code></p>
<p><code>compute.instantSnapshots.list</code></p>
<p><code>compute. instantSnapshots. listEffectiveTags</code></p>
<p><code>compute. instantSnapshots. listTagBindings</code></p>
<p><code>compute. interconnectAttachmentGroups. get</code></p>
<p><code>compute. interconnectAttachmentGroups. list</code></p>
<p><code>compute. interconnectAttachments. get</code></p>
<p><code>compute. interconnectAttachments. list</code></p>
<p><code>compute. interconnectAttachments. listEffectiveTags</code></p>
<p><code>compute. interconnectAttachments. listTagBindings</code></p>
<p><code>compute.interconnectGroups.get</code></p>
<p><code>compute. interconnectGroups. list</code></p>
<p><code>compute. interconnectLocations.*</code></p>
<ul>
<li><code>compute. interconnectLocations. get</code></li>
<li><code>compute. interconnectLocations. list</code></li>
</ul>
<p><code>compute. interconnectRemoteLocations.*</code></p>
<ul>
<li><code>compute. interconnectRemoteLocations. get</code></li>
<li><code>compute. interconnectRemoteLocations. list</code></li>
</ul>
<p><code>compute.interconnects.get</code></p>
<p><code>compute.interconnects.list</code></p>
<p><code>compute. interconnects. listEffectiveTags</code></p>
<p><code>compute. interconnects. listTagBindings</code></p>
<p><code>compute.licenseCodes.get</code></p>
<p><code>compute. licenseCodes. getIamPolicy</code></p>
<p><code>compute.licenseCodes.list</code></p>
<p><code>compute.licenses.get</code></p>
<p><code>compute.licenses.getIamPolicy</code></p>
<p><code>compute.licenses.list</code></p>
<p><code>compute. licenses. listEffectiveTags</code></p>
<p><code>compute. licenses. listTagBindings</code></p>
<p><code>compute.machineImages.get</code></p>
<p><code>compute. machineImages. getIamPolicy</code></p>
<p><code>compute.machineImages.list</code></p>
<p><code>compute. machineImages. listEffectiveTags</code></p>
<p><code>compute. machineImages. listTagBindings</code></p>
<p><code>compute.machineTypes.*</code></p>
<ul>
<li><code>compute.machineTypes.get</code></li>
<li><code>compute.machineTypes.list</code></li>
</ul>
<p><code>compute.managedRulesets.*</code></p>
<ul>
<li><code>compute.managedRulesets.get</code></li>
<li><code>compute.managedRulesets.list</code></li>
</ul>
<p><code>compute.multiMig.get</code></p>
<p><code>compute.multiMig.list</code></p>
<p><code>compute.multiMigMembers.*</code></p>
<ul>
<li><code>compute.multiMigMembers.get</code></li>
<li><code>compute.multiMigMembers.list</code></li>
</ul>
<p><code>compute.networkAttachments.get</code></p>
<p><code>compute. networkAttachments. getIamPolicy</code></p>
<p><code>compute. networkAttachments. list</code></p>
<p><code>compute. networkAttachments. listEffectiveTags</code></p>
<p><code>compute. networkAttachments. listTagBindings</code></p>
<p><code>compute. networkEdgeSecurityServices. get</code></p>
<p><code>compute. networkEdgeSecurityServices. list</code></p>
<p><code>compute. networkEdgeSecurityServices. listEffectiveTags</code></p>
<p><code>compute. networkEdgeSecurityServices. listTagBindings</code></p>
<p><code>compute. networkEndpointGroups. get</code></p>
<p><code>compute. networkEndpointGroups. list</code></p>
<p><code>compute. networkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. networkEndpointGroups. listTagBindings</code></p>
<p><code>compute.networkProfiles.*</code></p>
<ul>
<li><code>compute.networkProfiles.get</code></li>
<li><code>compute.networkProfiles.list</code></li>
</ul>
<p><code>compute.networks.get</code></p>
<p><code>compute. networks. getEffectiveFirewalls</code></p>
<p><code>compute. networks. getRegionEffectiveFirewalls</code></p>
<p><code>compute.networks.list</code></p>
<p><code>compute. networks. listEffectiveTags</code></p>
<p><code>compute. networks. listPeeringRoutes</code></p>
<p><code>compute. networks. listTagBindings</code></p>
<p><code>compute.nodeGroups.get</code></p>
<p><code>compute. nodeGroups. getIamPolicy</code></p>
<p><code>compute.nodeGroups.list</code></p>
<p><code>compute.nodeTemplates.get</code></p>
<p><code>compute. nodeTemplates. getIamPolicy</code></p>
<p><code>compute.nodeTemplates.list</code></p>
<p><code>compute.nodeTypes.*</code></p>
<ul>
<li><code>compute.nodeTypes.get</code></li>
<li><code>compute.nodeTypes.list</code></li>
</ul>
<p><code>compute.orgRolloutPlans.get</code></p>
<p><code>compute.orgRolloutPlans.list</code></p>
<p><code>compute.orgRollouts.get</code></p>
<p><code>compute.orgRollouts.list</code></p>
<p><code>compute. organizations. listAssociations</code></p>
<p><code>compute.packetMirrorings.get</code></p>
<p><code>compute.packetMirrorings.list</code></p>
<p><code>compute. packetMirrorings. listEffectiveTags</code></p>
<p><code>compute. packetMirrorings. listTagBindings</code></p>
<p><code>compute.previewFeatures.get</code></p>
<p><code>compute.previewFeatures.list</code></p>
<p><code>compute.projects.get</code></p>
<p><code>compute. publicAdvertisedPrefixes. get</code></p>
<p><code>compute. publicAdvertisedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. get</code></p>
<p><code>compute. publicDelegatedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. listEffectiveTags</code></p>
<p><code>compute. publicDelegatedPrefixes. listTagBindings</code></p>
<p><code>compute. recoverableSnapshots. get</code></p>
<p><code>compute. recoverableSnapshots. getIamPolicy</code></p>
<p><code>compute. recoverableSnapshots. list</code></p>
<p><code>compute. regionBackendBuckets. get</code></p>
<p><code>compute. regionBackendBuckets. getIamPolicy</code></p>
<p><code>compute. regionBackendBuckets. list</code></p>
<p><code>compute. regionBackendBuckets. listEffectiveTags</code></p>
<p><code>compute. regionBackendBuckets. listTagBindings</code></p>
<p><code>compute. regionBackendServices. get</code></p>
<p><code>compute. regionBackendServices. getIamPolicy</code></p>
<p><code>compute. regionBackendServices. list</code></p>
<p><code>compute. regionBackendServices. listEffectiveTags</code></p>
<p><code>compute. regionBackendServices. listTagBindings</code></p>
<p><code>compute. regionCompositeHealthChecks. get</code></p>
<p><code>compute. regionCompositeHealthChecks. list</code></p>
<p><code>compute. regionFirewallPolicies. get</code></p>
<p><code>compute. regionFirewallPolicies. getIamPolicy</code></p>
<p><code>compute. regionFirewallPolicies. list</code></p>
<p><code>compute. regionFirewallPolicies. listEffectiveTags</code></p>
<p><code>compute. regionFirewallPolicies. listTagBindings</code></p>
<p><code>compute. regionHealthAggregationPolicies. get</code></p>
<p><code>compute. regionHealthAggregationPolicies. list</code></p>
<p><code>compute. regionHealthCheckServices. get</code></p>
<p><code>compute. regionHealthCheckServices. list</code></p>
<p><code>compute.regionHealthChecks.get</code></p>
<p><code>compute. regionHealthChecks. list</code></p>
<p><code>compute. regionHealthChecks. listEffectiveTags</code></p>
<p><code>compute. regionHealthChecks. listTagBindings</code></p>
<p><code>compute. regionHealthSources. get</code></p>
<p><code>compute. regionHealthSources. list</code></p>
<p><code>compute. regionNetworkEndpointGroups. get</code></p>
<p><code>compute. regionNetworkEndpointGroups. list</code></p>
<p><code>compute. regionNetworkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. regionNetworkEndpointGroups. listTagBindings</code></p>
<p><code>compute. regionNetworkPolicies. get</code></p>
<p><code>compute. regionNetworkPolicies. list</code></p>
<p><code>compute. regionNotificationEndpoints. get</code></p>
<p><code>compute. regionNotificationEndpoints. list</code></p>
<p><code>compute.regionOperations.get</code></p>
<p><code>compute. regionOperations. getIamPolicy</code></p>
<p><code>compute.regionOperations.list</code></p>
<p><code>compute. regionSecurityPolicies. get</code></p>
<p><code>compute. regionSecurityPolicies. list</code></p>
<p><code>compute. regionSecurityPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSecurityPolicies. listTagBindings</code></p>
<p><code>compute. regionSslCertificates. get</code></p>
<p><code>compute. regionSslCertificates. list</code></p>
<p><code>compute. regionSslCertificates. listEffectiveTags</code></p>
<p><code>compute. regionSslCertificates. listTagBindings</code></p>
<p><code>compute.regionSslPolicies.get</code></p>
<p><code>compute. regionSslPolicies. getIamPolicy</code></p>
<p><code>compute.regionSslPolicies.list</code></p>
<p><code>compute. regionSslPolicies. listAvailableFeatures</code></p>
<p><code>compute. regionSslPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSslPolicies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpProxies. get</code></p>
<p><code>compute. regionTargetHttpProxies. list</code></p>
<p><code>compute. regionTargetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpProxies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpsProxies. get</code></p>
<p><code>compute. regionTargetHttpsProxies. list</code></p>
<p><code>compute. regionTargetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpsProxies. listTagBindings</code></p>
<p><code>compute. regionTargetTcpProxies. get</code></p>
<p><code>compute. regionTargetTcpProxies. list</code></p>
<p><code>compute. regionTargetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetTcpProxies. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.get</code></p>
<p><code>compute.regionUrlMaps.list</code></p>
<p><code>compute. regionUrlMaps. listEffectiveTags</code></p>
<p><code>compute. regionUrlMaps. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.validate</code></p>
<p><code>compute.regions.*</code></p>
<ul>
<li><code>compute.regions.get</code></li>
<li><code>compute.regions.list</code></li>
</ul>
<p><code>compute.reliabilityRisks.*</code></p>
<ul>
<li><code>compute.reliabilityRisks.get</code></li>
<li><code>compute.reliabilityRisks.list</code></li>
</ul>
<p><code>compute.reservationBlocks.get</code></p>
<p><code>compute.reservationBlocks.list</code></p>
<p><code>compute. reservationConsumedInstances. list</code></p>
<p><code>compute.reservationSlots.get</code></p>
<p><code>compute.reservationSlots.list</code></p>
<p><code>compute. reservationSubBlocks. get</code></p>
<p><code>compute. reservationSubBlocks. list</code></p>
<p><code>compute.reservations.get</code></p>
<p><code>compute.reservations.list</code></p>
<p><code>compute. reservations. listEffectiveTags</code></p>
<p><code>compute. reservations. listTagBindings</code></p>
<p><code>compute.resourcePolicies.get</code></p>
<p><code>compute. resourcePolicies. getIamPolicy</code></p>
<p><code>compute.resourcePolicies.list</code></p>
<p><code>compute.rolloutPlans.get</code></p>
<p><code>compute.rolloutPlans.list</code></p>
<p><code>compute.rollouts.get</code></p>
<p><code>compute.rollouts.list</code></p>
<p><code>compute.routers.get</code></p>
<p><code>compute.routers.getRoutePolicy</code></p>
<p><code>compute.routers.list</code></p>
<p><code>compute.routers.listBgpRoutes</code></p>
<p><code>compute. routers. listEffectiveTags</code></p>
<p><code>compute. routers. listRoutePolicies</code></p>
<p><code>compute. routers. listTagBindings</code></p>
<p><code>compute.routes.get</code></p>
<p><code>compute.routes.list</code></p>
<p><code>compute. routes. listEffectiveTags</code></p>
<p><code>compute.routes.listTagBindings</code></p>
<p><code>compute.securityPolicies.get</code></p>
<p><code>compute.securityPolicies.list</code></p>
<p><code>compute. securityPolicies. listEffectiveTags</code></p>
<p><code>compute. securityPolicies. listTagBindings</code></p>
<p><code>compute.serviceAttachments.get</code></p>
<p><code>compute. serviceAttachments. getIamPolicy</code></p>
<p><code>compute. serviceAttachments. list</code></p>
<p><code>compute. serviceAttachments. listEffectiveTags</code></p>
<p><code>compute. serviceAttachments. listTagBindings</code></p>
<p><code>compute.snapshotGroups.get</code></p>
<p><code>compute. snapshotGroups. getIamPolicy</code></p>
<p><code>compute.snapshotGroups.list</code></p>
<p><code>compute. snapshotRecycleBinPolicy. get</code></p>
<p><code>compute.snapshotSettings.get</code></p>
<p><code>compute.snapshots.get</code></p>
<p><code>compute. snapshots. getEffectiveRecycleBinRule</code></p>
<p><code>compute.snapshots.getIamPolicy</code></p>
<p><code>compute.snapshots.list</code></p>
<p><code>compute. snapshots. listEffectiveTags</code></p>
<p><code>compute. snapshots. listTagBindings</code></p>
<p><code>compute.spotAssistants.get</code></p>
<p><code>compute.sslCertificates.get</code></p>
<p><code>compute.sslCertificates.list</code></p>
<p><code>compute. sslCertificates. listEffectiveTags</code></p>
<p><code>compute. sslCertificates. listTagBindings</code></p>
<p><code>compute.sslPolicies.get</code></p>
<p><code>compute. sslPolicies. getIamPolicy</code></p>
<p><code>compute.sslPolicies.list</code></p>
<p><code>compute. sslPolicies. listAvailableFeatures</code></p>
<p><code>compute. sslPolicies. listEffectiveTags</code></p>
<p><code>compute. sslPolicies. listTagBindings</code></p>
<p><code>compute.storagePools.get</code></p>
<p><code>compute. storagePools. getIamPolicy</code></p>
<p><code>compute.storagePools.list</code></p>
<p><code>compute. storagePools. listEffectiveTags</code></p>
<p><code>compute. storagePools. listTagBindings</code></p>
<p><code>compute.subnetworks.get</code></p>
<p><code>compute. subnetworks. getIamPolicy</code></p>
<p><code>compute.subnetworks.list</code></p>
<p><code>compute. subnetworks. listEffectiveTags</code></p>
<p><code>compute. subnetworks. listTagBindings</code></p>
<p><code>compute.targetGrpcProxies.get</code></p>
<p><code>compute.targetGrpcProxies.list</code></p>
<p><code>compute. targetGrpcProxies. listEffectiveTags</code></p>
<p><code>compute. targetGrpcProxies. listTagBindings</code></p>
<p><code>compute.targetHttpProxies.get</code></p>
<p><code>compute.targetHttpProxies.list</code></p>
<p><code>compute. targetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpProxies. listTagBindings</code></p>
<p><code>compute.targetHttpsProxies.get</code></p>
<p><code>compute. targetHttpsProxies. list</code></p>
<p><code>compute. targetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpsProxies. listTagBindings</code></p>
<p><code>compute.targetInstances.get</code></p>
<p><code>compute.targetInstances.list</code></p>
<p><code>compute. targetInstances. listEffectiveTags</code></p>
<p><code>compute. targetInstances. listTagBindings</code></p>
<p><code>compute.targetPools.get</code></p>
<p><code>compute.targetPools.list</code></p>
<p><code>compute. targetPools. listEffectiveTags</code></p>
<p><code>compute. targetPools. listTagBindings</code></p>
<p><code>compute.targetSslProxies.get</code></p>
<p><code>compute.targetSslProxies.list</code></p>
<p><code>compute. targetSslProxies. listEffectiveTags</code></p>
<p><code>compute. targetSslProxies. listTagBindings</code></p>
<p><code>compute.targetTcpProxies.get</code></p>
<p><code>compute.targetTcpProxies.list</code></p>
<p><code>compute. targetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. targetTcpProxies. listTagBindings</code></p>
<p><code>compute.targetVpnGateways.get</code></p>
<p><code>compute.targetVpnGateways.list</code></p>
<p><code>compute. targetVpnGateways. listEffectiveTags</code></p>
<p><code>compute. targetVpnGateways. listTagBindings</code></p>
<p><code>compute.urlMaps.get</code></p>
<p><code>compute.urlMaps.list</code></p>
<p><code>compute. urlMaps. listEffectiveTags</code></p>
<p><code>compute. urlMaps. listTagBindings</code></p>
<p><code>compute.urlMaps.validate</code></p>
<p><code>compute. vmExtensionPolicies. get</code></p>
<p><code>compute. vmExtensionPolicies. list</code></p>
<p><code>compute.vpnGateways.get</code></p>
<p><code>compute.vpnGateways.list</code></p>
<p><code>compute. vpnGateways. listEffectiveTags</code></p>
<p><code>compute. vpnGateways. listTagBindings</code></p>
<p><code>compute.vpnTunnels.get</code></p>
<p><code>compute.vpnTunnels.list</code></p>
<p><code>compute. vpnTunnels. listEffectiveTags</code></p>
<p><code>compute. vpnTunnels. listTagBindings</code></p>
<p><code>compute.wireGroups.get</code></p>
<p><code>compute.wireGroups.list</code></p>
<p><code>compute.zoneOperations.get</code></p>
<p><code>compute. zoneOperations. getIamPolicy</code></p>
<p><code>compute.zoneOperations.list</code></p>
<p><code>compute.zones.*</code></p>
<ul>
<li><code>compute.zones.get</code></li>
<li><code>compute.zones.list</code></li>
</ul>
<p><code>notebooks.*</code></p>
<ul>
<li><code>notebooks.environments.create</code></li>
<li><code>notebooks.environments.delete</code></li>
<li><code>notebooks.environments.get</code></li>
<li><code>notebooks. environments. getIamPolicy</code></li>
<li><code>notebooks.environments.list</code></li>
<li><code>notebooks. environments. setIamPolicy</code></li>
<li><code>notebooks.executions.create</code></li>
<li><code>notebooks.executions.delete</code></li>
<li><code>notebooks.executions.get</code></li>
<li><code>notebooks. executions. getIamPolicy</code></li>
<li><code>notebooks.executions.list</code></li>
<li><code>notebooks. executions. setIamPolicy</code></li>
<li><code>notebooks. instances. checkUpgradability</code></li>
<li><code>notebooks.instances.create</code></li>
<li><code>notebooks. instances. createTagBinding</code></li>
<li><code>notebooks.instances.delete</code></li>
<li><code>notebooks. instances. deleteTagBinding</code></li>
<li><code>notebooks.instances.diagnose</code></li>
<li><code>notebooks.instances.get</code></li>
<li><code>notebooks.instances.getHealth</code></li>
<li><code>notebooks. instances. getIamPolicy</code></li>
<li><code>notebooks.instances.list</code></li>
<li><code>notebooks. instances. listEffectiveTags</code></li>
<li><code>notebooks. instances. listTagBindings</code></li>
<li><code>notebooks.instances.reset</code></li>
<li><code>notebooks. instances. setAccelerator</code></li>
<li><code>notebooks. instances. setIamPolicy</code></li>
<li><code>notebooks.instances.setLabels</code></li>
<li><code>notebooks. instances. setMachineType</code></li>
<li><code>notebooks.instances.start</code></li>
<li><code>notebooks.instances.stop</code></li>
<li><code>notebooks.instances.update</code></li>
<li><code>notebooks. instances. updateConfig</code></li>
<li><code>notebooks. instances. updateShieldInstanceConfig</code></li>
<li><code>notebooks.instances.upgrade</code></li>
<li><code>notebooks.instances.use</code></li>
<li><code>notebooks.locations.get</code></li>
<li><code>notebooks.locations.list</code></li>
<li><code>notebooks.operations.cancel</code></li>
<li><code>notebooks.operations.delete</code></li>
<li><code>notebooks.operations.get</code></li>
<li><code>notebooks.operations.list</code></li>
<li><code>notebooks.runtimes.create</code></li>
<li><code>notebooks.runtimes.delete</code></li>
<li><code>notebooks.runtimes.diagnose</code></li>
<li><code>notebooks.runtimes.get</code></li>
<li><code>notebooks. runtimes. getIamPolicy</code></li>
<li><code>notebooks.runtimes.list</code></li>
<li><code>notebooks.runtimes.reset</code></li>
<li><code>notebooks. runtimes. setIamPolicy</code></li>
<li><code>notebooks.runtimes.start</code></li>
<li><code>notebooks.runtimes.stop</code></li>
<li><code>notebooks.runtimes.switch</code></li>
<li><code>notebooks.runtimes.update</code></li>
<li><code>notebooks.runtimes.upgrade</code></li>
<li><code>notebooks.schedules.create</code></li>
<li><code>notebooks.schedules.delete</code></li>
<li><code>notebooks.schedules.get</code></li>
<li><code>notebooks. schedules. getIamPolicy</code></li>
<li><code>notebooks.schedules.list</code></li>
<li><code>notebooks. schedules. setIamPolicy</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p>
<p><code>serviceusage. consumerpolicy. analyze</code></p>
<p><code>serviceusage. consumerpolicy. get</code></p>
<p><code>serviceusage. effectivepolicy. get</code></p>
<p><code>serviceusage.groups.*</code></p>
<ul>
<li><code>serviceusage.groups.list</code></li>
<li><code>serviceusage. groups. listExpandedMembers</code></li>
<li><code>serviceusage. groups. listMembers</code></li>
</ul>
<p><code>serviceusage.quotas.get</code></p>
<p><code>serviceusage.services.get</code></p>
<p><code>serviceusage.services.list</code></p>
<p><code>serviceusage.values.test</code></p></td>
</tr>
<tr class="even">
<td>Notebooks Editor
<p>( <code>roles/ notebooks.editor</code> )</p>
<p>Editor role for notebooks</p></td>
<td><p><code>aiplatform. notebookExecutionJobs. get</code></p>
<p><code>aiplatform. notebookExecutionJobs. list</code></p>
<p><code>aiplatform.schedules.get</code></p>
<p><code>aiplatform.schedules.list</code></p>
<p><code>compute.acceleratorTypes.*</code></p>
<ul>
<li><code>compute.acceleratorTypes.get</code></li>
<li><code>compute.acceleratorTypes.list</code></li>
</ul>
<p><code>compute.addresses.get</code></p>
<p><code>compute.addresses.list</code></p>
<p><code>compute. addresses. listEffectiveTags</code></p>
<p><code>compute. addresses. listTagBindings</code></p>
<p><code>compute.advice.capacity</code></p>
<p><code>compute.advice.capacityHistory</code></p>
<p><code>compute.autoscalers.get</code></p>
<p><code>compute.autoscalers.list</code></p>
<p><code>compute.backendBuckets.get</code></p>
<p><code>compute. backendBuckets. getIamPolicy</code></p>
<p><code>compute.backendBuckets.list</code></p>
<p><code>compute. backendBuckets. listEffectiveTags</code></p>
<p><code>compute. backendBuckets. listTagBindings</code></p>
<p><code>compute.backendServices.get</code></p>
<p><code>compute. backendServices. getIamPolicy</code></p>
<p><code>compute.backendServices.list</code></p>
<p><code>compute. backendServices. listEffectiveTags</code></p>
<p><code>compute. backendServices. listTagBindings</code></p>
<p><code>compute.commitments.get</code></p>
<p><code>compute.commitments.list</code></p>
<p><code>compute. commitments. listEffectiveTags</code></p>
<p><code>compute. commitments. listTagBindings</code></p>
<p><code>compute.crossSiteNetworks.get</code></p>
<p><code>compute.crossSiteNetworks.list</code></p>
<p><code>compute.diskSettings.get</code></p>
<p><code>compute.diskTypes.*</code></p>
<ul>
<li><code>compute.diskTypes.get</code></li>
<li><code>compute.diskTypes.list</code></li>
</ul>
<p><code>compute.disks.get</code></p>
<p><code>compute.disks.getIamPolicy</code></p>
<p><code>compute.disks.list</code></p>
<p><code>compute. disks. listEffectiveTags</code></p>
<p><code>compute.disks.listTagBindings</code></p>
<p><code>compute. externalVpnGateways. get</code></p>
<p><code>compute. externalVpnGateways. list</code></p>
<p><code>compute. externalVpnGateways. listEffectiveTags</code></p>
<p><code>compute. externalVpnGateways. listTagBindings</code></p>
<p><code>compute.firewallPolicies.get</code></p>
<p><code>compute. firewallPolicies. getIamPolicy</code></p>
<p><code>compute.firewallPolicies.list</code></p>
<p><code>compute. firewallPolicies. listEffectiveTags</code></p>
<p><code>compute. firewallPolicies. listTagBindings</code></p>
<p><code>compute.firewalls.get</code></p>
<p><code>compute.firewalls.list</code></p>
<p><code>compute. firewalls. listEffectiveTags</code></p>
<p><code>compute. firewalls. listTagBindings</code></p>
<p><code>compute.forwardingRules.get</code></p>
<p><code>compute.forwardingRules.list</code></p>
<p><code>compute. forwardingRules. listEffectiveTags</code></p>
<p><code>compute. forwardingRules. listTagBindings</code></p>
<p><code>compute.futureReservations.get</code></p>
<p><code>compute. futureReservations. getIamPolicy</code></p>
<p><code>compute. futureReservations. list</code></p>
<p><code>compute. futureReservations. listEffectiveTags</code></p>
<p><code>compute. futureReservations. listTagBindings</code></p>
<p><code>compute.globalAddresses.get</code></p>
<p><code>compute.globalAddresses.list</code></p>
<p><code>compute. globalAddresses. listEffectiveTags</code></p>
<p><code>compute. globalAddresses. listTagBindings</code></p>
<p><code>compute. globalForwardingRules. get</code></p>
<p><code>compute. globalForwardingRules. list</code></p>
<p><code>compute. globalForwardingRules. listEffectiveTags</code></p>
<p><code>compute. globalForwardingRules. listTagBindings</code></p>
<p><code>compute. globalFrontendSettings. get</code></p>
<p><code>compute. globalNetworkEndpointGroups. get</code></p>
<p><code>compute. globalNetworkEndpointGroups. list</code></p>
<p><code>compute. globalNetworkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. globalNetworkEndpointGroups. listTagBindings</code></p>
<p><code>compute.globalOperations.get</code></p>
<p><code>compute. globalOperations. getIamPolicy</code></p>
<p><code>compute.globalOperations.list</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. get</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. list</code></p>
<p><code>compute.healthChecks.get</code></p>
<p><code>compute.healthChecks.list</code></p>
<p><code>compute. healthChecks. listEffectiveTags</code></p>
<p><code>compute. healthChecks. listTagBindings</code></p>
<p><code>compute.hosts.*</code></p>
<ul>
<li><code>compute.hosts.get</code></li>
<li><code>compute.hosts.getVersion</code></li>
<li><code>compute.hosts.list</code></li>
</ul>
<p><code>compute.httpHealthChecks.get</code></p>
<p><code>compute.httpHealthChecks.list</code></p>
<p><code>compute. httpHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpHealthChecks. listTagBindings</code></p>
<p><code>compute.httpsHealthChecks.get</code></p>
<p><code>compute.httpsHealthChecks.list</code></p>
<p><code>compute. httpsHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpsHealthChecks. listTagBindings</code></p>
<p><code>compute.images.get</code></p>
<p><code>compute.images.getFromFamily</code></p>
<p><code>compute.images.getIamPolicy</code></p>
<p><code>compute.images.list</code></p>
<p><code>compute. images. listEffectiveTags</code></p>
<p><code>compute.images.listTagBindings</code></p>
<p><code>compute. instanceGroupManagers. get</code></p>
<p><code>compute. instanceGroupManagers. list</code></p>
<p><code>compute. instanceGroupManagers. listEffectiveTags</code></p>
<p><code>compute. instanceGroupManagers. listTagBindings</code></p>
<p><code>compute.instanceGroups.get</code></p>
<p><code>compute.instanceGroups.list</code></p>
<p><code>compute. instanceGroups. listEffectiveTags</code></p>
<p><code>compute. instanceGroups. listTagBindings</code></p>
<p><code>compute.instanceSettings.get</code></p>
<p><code>compute.instanceTemplates.get</code></p>
<p><code>compute. instanceTemplates. getIamPolicy</code></p>
<p><code>compute.instanceTemplates.list</code></p>
<p><code>compute.instances.get</code></p>
<p><code>compute. instances. getEffectiveFirewalls</code></p>
<p><code>compute. instances. getGuestAttributes</code></p>
<p><code>compute.instances.getIamPolicy</code></p>
<p><code>compute. instances. getScreenshot</code></p>
<p><code>compute. instances. getSerialPortOutput</code></p>
<p><code>compute. instances. getShieldedInstanceIdentity</code></p>
<p><code>compute. instances. getShieldedVmIdentity</code></p>
<p><code>compute. instances. getVmExtensionState</code></p>
<p><code>compute.instances.list</code></p>
<p><code>compute. instances. listEffectiveTags</code></p>
<p><code>compute. instances. listReferrers</code></p>
<p><code>compute. instances. listTagBindings</code></p>
<p><code>compute. instances. listVmExtensionStates</code></p>
<p><code>compute.instances.troubleshoot</code></p>
<p><code>compute. instantSnapshotGroups. get</code></p>
<p><code>compute. instantSnapshotGroups. getIamPolicy</code></p>
<p><code>compute. instantSnapshotGroups. list</code></p>
<p><code>compute.instantSnapshots.get</code></p>
<p><code>compute. instantSnapshots. getIamPolicy</code></p>
<p><code>compute.instantSnapshots.list</code></p>
<p><code>compute. instantSnapshots. listEffectiveTags</code></p>
<p><code>compute. instantSnapshots. listTagBindings</code></p>
<p><code>compute. interconnectAttachmentGroups. get</code></p>
<p><code>compute. interconnectAttachmentGroups. list</code></p>
<p><code>compute. interconnectAttachments. get</code></p>
<p><code>compute. interconnectAttachments. list</code></p>
<p><code>compute. interconnectAttachments. listEffectiveTags</code></p>
<p><code>compute. interconnectAttachments. listTagBindings</code></p>
<p><code>compute.interconnectGroups.get</code></p>
<p><code>compute. interconnectGroups. list</code></p>
<p><code>compute. interconnectLocations.*</code></p>
<ul>
<li><code>compute. interconnectLocations. get</code></li>
<li><code>compute. interconnectLocations. list</code></li>
</ul>
<p><code>compute. interconnectRemoteLocations.*</code></p>
<ul>
<li><code>compute. interconnectRemoteLocations. get</code></li>
<li><code>compute. interconnectRemoteLocations. list</code></li>
</ul>
<p><code>compute.interconnects.get</code></p>
<p><code>compute.interconnects.list</code></p>
<p><code>compute. interconnects. listEffectiveTags</code></p>
<p><code>compute. interconnects. listTagBindings</code></p>
<p><code>compute.licenseCodes.get</code></p>
<p><code>compute. licenseCodes. getIamPolicy</code></p>
<p><code>compute.licenseCodes.list</code></p>
<p><code>compute.licenses.get</code></p>
<p><code>compute.licenses.getIamPolicy</code></p>
<p><code>compute.licenses.list</code></p>
<p><code>compute. licenses. listEffectiveTags</code></p>
<p><code>compute. licenses. listTagBindings</code></p>
<p><code>compute.machineImages.get</code></p>
<p><code>compute. machineImages. getIamPolicy</code></p>
<p><code>compute.machineImages.list</code></p>
<p><code>compute. machineImages. listEffectiveTags</code></p>
<p><code>compute. machineImages. listTagBindings</code></p>
<p><code>compute.machineTypes.*</code></p>
<ul>
<li><code>compute.machineTypes.get</code></li>
<li><code>compute.machineTypes.list</code></li>
</ul>
<p><code>compute.managedRulesets.*</code></p>
<ul>
<li><code>compute.managedRulesets.get</code></li>
<li><code>compute.managedRulesets.list</code></li>
</ul>
<p><code>compute.multiMig.get</code></p>
<p><code>compute.multiMig.list</code></p>
<p><code>compute.multiMigMembers.*</code></p>
<ul>
<li><code>compute.multiMigMembers.get</code></li>
<li><code>compute.multiMigMembers.list</code></li>
</ul>
<p><code>compute.networkAttachments.get</code></p>
<p><code>compute. networkAttachments. getIamPolicy</code></p>
<p><code>compute. networkAttachments. list</code></p>
<p><code>compute. networkAttachments. listEffectiveTags</code></p>
<p><code>compute. networkAttachments. listTagBindings</code></p>
<p><code>compute. networkEdgeSecurityServices. get</code></p>
<p><code>compute. networkEdgeSecurityServices. list</code></p>
<p><code>compute. networkEdgeSecurityServices. listEffectiveTags</code></p>
<p><code>compute. networkEdgeSecurityServices. listTagBindings</code></p>
<p><code>compute. networkEndpointGroups. get</code></p>
<p><code>compute. networkEndpointGroups. list</code></p>
<p><code>compute. networkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. networkEndpointGroups. listTagBindings</code></p>
<p><code>compute.networkProfiles.*</code></p>
<ul>
<li><code>compute.networkProfiles.get</code></li>
<li><code>compute.networkProfiles.list</code></li>
</ul>
<p><code>compute.networks.get</code></p>
<p><code>compute. networks. getEffectiveFirewalls</code></p>
<p><code>compute. networks. getRegionEffectiveFirewalls</code></p>
<p><code>compute.networks.list</code></p>
<p><code>compute. networks. listEffectiveTags</code></p>
<p><code>compute. networks. listPeeringRoutes</code></p>
<p><code>compute. networks. listTagBindings</code></p>
<p><code>compute.nodeGroups.get</code></p>
<p><code>compute. nodeGroups. getIamPolicy</code></p>
<p><code>compute.nodeGroups.list</code></p>
<p><code>compute.nodeTemplates.get</code></p>
<p><code>compute. nodeTemplates. getIamPolicy</code></p>
<p><code>compute.nodeTemplates.list</code></p>
<p><code>compute.nodeTypes.*</code></p>
<ul>
<li><code>compute.nodeTypes.get</code></li>
<li><code>compute.nodeTypes.list</code></li>
</ul>
<p><code>compute.orgRolloutPlans.get</code></p>
<p><code>compute.orgRolloutPlans.list</code></p>
<p><code>compute.orgRollouts.get</code></p>
<p><code>compute.orgRollouts.list</code></p>
<p><code>compute. organizations. listAssociations</code></p>
<p><code>compute.packetMirrorings.get</code></p>
<p><code>compute.packetMirrorings.list</code></p>
<p><code>compute. packetMirrorings. listEffectiveTags</code></p>
<p><code>compute. packetMirrorings. listTagBindings</code></p>
<p><code>compute.previewFeatures.get</code></p>
<p><code>compute.previewFeatures.list</code></p>
<p><code>compute.projects.get</code></p>
<p><code>compute. publicAdvertisedPrefixes. get</code></p>
<p><code>compute. publicAdvertisedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. get</code></p>
<p><code>compute. publicDelegatedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. listEffectiveTags</code></p>
<p><code>compute. publicDelegatedPrefixes. listTagBindings</code></p>
<p><code>compute. recoverableSnapshots. get</code></p>
<p><code>compute. recoverableSnapshots. getIamPolicy</code></p>
<p><code>compute. recoverableSnapshots. list</code></p>
<p><code>compute. regionBackendBuckets. get</code></p>
<p><code>compute. regionBackendBuckets. getIamPolicy</code></p>
<p><code>compute. regionBackendBuckets. list</code></p>
<p><code>compute. regionBackendBuckets. listEffectiveTags</code></p>
<p><code>compute. regionBackendBuckets. listTagBindings</code></p>
<p><code>compute. regionBackendServices. get</code></p>
<p><code>compute. regionBackendServices. getIamPolicy</code></p>
<p><code>compute. regionBackendServices. list</code></p>
<p><code>compute. regionBackendServices. listEffectiveTags</code></p>
<p><code>compute. regionBackendServices. listTagBindings</code></p>
<p><code>compute. regionCompositeHealthChecks. get</code></p>
<p><code>compute. regionCompositeHealthChecks. list</code></p>
<p><code>compute. regionFirewallPolicies. get</code></p>
<p><code>compute. regionFirewallPolicies. getIamPolicy</code></p>
<p><code>compute. regionFirewallPolicies. list</code></p>
<p><code>compute. regionFirewallPolicies. listEffectiveTags</code></p>
<p><code>compute. regionFirewallPolicies. listTagBindings</code></p>
<p><code>compute. regionHealthAggregationPolicies. get</code></p>
<p><code>compute. regionHealthAggregationPolicies. list</code></p>
<p><code>compute. regionHealthCheckServices. get</code></p>
<p><code>compute. regionHealthCheckServices. list</code></p>
<p><code>compute.regionHealthChecks.get</code></p>
<p><code>compute. regionHealthChecks. list</code></p>
<p><code>compute. regionHealthChecks. listEffectiveTags</code></p>
<p><code>compute. regionHealthChecks. listTagBindings</code></p>
<p><code>compute. regionHealthSources. get</code></p>
<p><code>compute. regionHealthSources. list</code></p>
<p><code>compute. regionNetworkEndpointGroups. get</code></p>
<p><code>compute. regionNetworkEndpointGroups. list</code></p>
<p><code>compute. regionNetworkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. regionNetworkEndpointGroups. listTagBindings</code></p>
<p><code>compute. regionNetworkPolicies. get</code></p>
<p><code>compute. regionNetworkPolicies. list</code></p>
<p><code>compute. regionNotificationEndpoints. get</code></p>
<p><code>compute. regionNotificationEndpoints. list</code></p>
<p><code>compute.regionOperations.get</code></p>
<p><code>compute. regionOperations. getIamPolicy</code></p>
<p><code>compute.regionOperations.list</code></p>
<p><code>compute. regionSecurityPolicies. get</code></p>
<p><code>compute. regionSecurityPolicies. list</code></p>
<p><code>compute. regionSecurityPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSecurityPolicies. listTagBindings</code></p>
<p><code>compute. regionSslCertificates. get</code></p>
<p><code>compute. regionSslCertificates. list</code></p>
<p><code>compute. regionSslCertificates. listEffectiveTags</code></p>
<p><code>compute. regionSslCertificates. listTagBindings</code></p>
<p><code>compute.regionSslPolicies.get</code></p>
<p><code>compute. regionSslPolicies. getIamPolicy</code></p>
<p><code>compute.regionSslPolicies.list</code></p>
<p><code>compute. regionSslPolicies. listAvailableFeatures</code></p>
<p><code>compute. regionSslPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSslPolicies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpProxies. get</code></p>
<p><code>compute. regionTargetHttpProxies. list</code></p>
<p><code>compute. regionTargetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpProxies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpsProxies. get</code></p>
<p><code>compute. regionTargetHttpsProxies. list</code></p>
<p><code>compute. regionTargetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpsProxies. listTagBindings</code></p>
<p><code>compute. regionTargetTcpProxies. get</code></p>
<p><code>compute. regionTargetTcpProxies. list</code></p>
<p><code>compute. regionTargetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetTcpProxies. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.get</code></p>
<p><code>compute.regionUrlMaps.list</code></p>
<p><code>compute. regionUrlMaps. listEffectiveTags</code></p>
<p><code>compute. regionUrlMaps. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.validate</code></p>
<p><code>compute.regions.*</code></p>
<ul>
<li><code>compute.regions.get</code></li>
<li><code>compute.regions.list</code></li>
</ul>
<p><code>compute.reliabilityRisks.*</code></p>
<ul>
<li><code>compute.reliabilityRisks.get</code></li>
<li><code>compute.reliabilityRisks.list</code></li>
</ul>
<p><code>compute.reservationBlocks.get</code></p>
<p><code>compute.reservationBlocks.list</code></p>
<p><code>compute. reservationConsumedInstances. list</code></p>
<p><code>compute.reservationSlots.get</code></p>
<p><code>compute.reservationSlots.list</code></p>
<p><code>compute. reservationSubBlocks. get</code></p>
<p><code>compute. reservationSubBlocks. list</code></p>
<p><code>compute.reservations.get</code></p>
<p><code>compute.reservations.list</code></p>
<p><code>compute. reservations. listEffectiveTags</code></p>
<p><code>compute. reservations. listTagBindings</code></p>
<p><code>compute.resourcePolicies.get</code></p>
<p><code>compute. resourcePolicies. getIamPolicy</code></p>
<p><code>compute.resourcePolicies.list</code></p>
<p><code>compute.rolloutPlans.get</code></p>
<p><code>compute.rolloutPlans.list</code></p>
<p><code>compute.rollouts.get</code></p>
<p><code>compute.rollouts.list</code></p>
<p><code>compute.routers.get</code></p>
<p><code>compute.routers.getRoutePolicy</code></p>
<p><code>compute.routers.list</code></p>
<p><code>compute.routers.listBgpRoutes</code></p>
<p><code>compute. routers. listEffectiveTags</code></p>
<p><code>compute. routers. listRoutePolicies</code></p>
<p><code>compute. routers. listTagBindings</code></p>
<p><code>compute.routes.get</code></p>
<p><code>compute.routes.list</code></p>
<p><code>compute. routes. listEffectiveTags</code></p>
<p><code>compute.routes.listTagBindings</code></p>
<p><code>compute.securityPolicies.get</code></p>
<p><code>compute.securityPolicies.list</code></p>
<p><code>compute. securityPolicies. listEffectiveTags</code></p>
<p><code>compute. securityPolicies. listTagBindings</code></p>
<p><code>compute.serviceAttachments.get</code></p>
<p><code>compute. serviceAttachments. getIamPolicy</code></p>
<p><code>compute. serviceAttachments. list</code></p>
<p><code>compute. serviceAttachments. listEffectiveTags</code></p>
<p><code>compute. serviceAttachments. listTagBindings</code></p>
<p><code>compute.snapshotGroups.get</code></p>
<p><code>compute. snapshotGroups. getIamPolicy</code></p>
<p><code>compute.snapshotGroups.list</code></p>
<p><code>compute. snapshotRecycleBinPolicy. get</code></p>
<p><code>compute.snapshotSettings.get</code></p>
<p><code>compute.snapshots.get</code></p>
<p><code>compute. snapshots. getEffectiveRecycleBinRule</code></p>
<p><code>compute.snapshots.getIamPolicy</code></p>
<p><code>compute.snapshots.list</code></p>
<p><code>compute. snapshots. listEffectiveTags</code></p>
<p><code>compute. snapshots. listTagBindings</code></p>
<p><code>compute.spotAssistants.get</code></p>
<p><code>compute.sslCertificates.get</code></p>
<p><code>compute.sslCertificates.list</code></p>
<p><code>compute. sslCertificates. listEffectiveTags</code></p>
<p><code>compute. sslCertificates. listTagBindings</code></p>
<p><code>compute.sslPolicies.get</code></p>
<p><code>compute. sslPolicies. getIamPolicy</code></p>
<p><code>compute.sslPolicies.list</code></p>
<p><code>compute. sslPolicies. listAvailableFeatures</code></p>
<p><code>compute. sslPolicies. listEffectiveTags</code></p>
<p><code>compute. sslPolicies. listTagBindings</code></p>
<p><code>compute.storagePools.get</code></p>
<p><code>compute. storagePools. getIamPolicy</code></p>
<p><code>compute.storagePools.list</code></p>
<p><code>compute. storagePools. listEffectiveTags</code></p>
<p><code>compute. storagePools. listTagBindings</code></p>
<p><code>compute.subnetworks.get</code></p>
<p><code>compute. subnetworks. getIamPolicy</code></p>
<p><code>compute.subnetworks.list</code></p>
<p><code>compute. subnetworks. listEffectiveTags</code></p>
<p><code>compute. subnetworks. listTagBindings</code></p>
<p><code>compute.targetGrpcProxies.get</code></p>
<p><code>compute.targetGrpcProxies.list</code></p>
<p><code>compute. targetGrpcProxies. listEffectiveTags</code></p>
<p><code>compute. targetGrpcProxies. listTagBindings</code></p>
<p><code>compute.targetHttpProxies.get</code></p>
<p><code>compute.targetHttpProxies.list</code></p>
<p><code>compute. targetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpProxies. listTagBindings</code></p>
<p><code>compute.targetHttpsProxies.get</code></p>
<p><code>compute. targetHttpsProxies. list</code></p>
<p><code>compute. targetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpsProxies. listTagBindings</code></p>
<p><code>compute.targetInstances.get</code></p>
<p><code>compute.targetInstances.list</code></p>
<p><code>compute. targetInstances. listEffectiveTags</code></p>
<p><code>compute. targetInstances. listTagBindings</code></p>
<p><code>compute.targetPools.get</code></p>
<p><code>compute.targetPools.list</code></p>
<p><code>compute. targetPools. listEffectiveTags</code></p>
<p><code>compute. targetPools. listTagBindings</code></p>
<p><code>compute.targetSslProxies.get</code></p>
<p><code>compute.targetSslProxies.list</code></p>
<p><code>compute. targetSslProxies. listEffectiveTags</code></p>
<p><code>compute. targetSslProxies. listTagBindings</code></p>
<p><code>compute.targetTcpProxies.get</code></p>
<p><code>compute.targetTcpProxies.list</code></p>
<p><code>compute. targetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. targetTcpProxies. listTagBindings</code></p>
<p><code>compute.targetVpnGateways.get</code></p>
<p><code>compute.targetVpnGateways.list</code></p>
<p><code>compute. targetVpnGateways. listEffectiveTags</code></p>
<p><code>compute. targetVpnGateways. listTagBindings</code></p>
<p><code>compute.urlMaps.get</code></p>
<p><code>compute.urlMaps.list</code></p>
<p><code>compute. urlMaps. listEffectiveTags</code></p>
<p><code>compute. urlMaps. listTagBindings</code></p>
<p><code>compute.urlMaps.validate</code></p>
<p><code>compute. vmExtensionPolicies. get</code></p>
<p><code>compute. vmExtensionPolicies. list</code></p>
<p><code>compute.vpnGateways.get</code></p>
<p><code>compute.vpnGateways.list</code></p>
<p><code>compute. vpnGateways. listEffectiveTags</code></p>
<p><code>compute. vpnGateways. listTagBindings</code></p>
<p><code>compute.vpnTunnels.get</code></p>
<p><code>compute.vpnTunnels.list</code></p>
<p><code>compute. vpnTunnels. listEffectiveTags</code></p>
<p><code>compute. vpnTunnels. listTagBindings</code></p>
<p><code>compute.wireGroups.get</code></p>
<p><code>compute.wireGroups.list</code></p>
<p><code>compute.zoneOperations.get</code></p>
<p><code>compute. zoneOperations. getIamPolicy</code></p>
<p><code>compute.zoneOperations.list</code></p>
<p><code>compute.zones.*</code></p>
<ul>
<li><code>compute.zones.get</code></li>
<li><code>compute.zones.list</code></li>
</ul>
<p><code>notebooks.environments.create</code></p>
<p><code>notebooks.environments.delete</code></p>
<p><code>notebooks.environments.get</code></p>
<p><code>notebooks. environments. getIamPolicy</code></p>
<p><code>notebooks.environments.list</code></p>
<p><code>notebooks.executions.create</code></p>
<p><code>notebooks.executions.delete</code></p>
<p><code>notebooks.executions.get</code></p>
<p><code>notebooks. executions. getIamPolicy</code></p>
<p><code>notebooks.executions.list</code></p>
<p><code>notebooks. instances. checkUpgradability</code></p>
<p><code>notebooks.instances.create</code></p>
<p><code>notebooks.instances.delete</code></p>
<p><code>notebooks.instances.diagnose</code></p>
<p><code>notebooks.instances.get</code></p>
<p><code>notebooks.instances.getHealth</code></p>
<p><code>notebooks. instances. getIamPolicy</code></p>
<p><code>notebooks.instances.list</code></p>
<p><code>notebooks. instances. listEffectiveTags</code></p>
<p><code>notebooks. instances. listTagBindings</code></p>
<p><code>notebooks.instances.reset</code></p>
<p><code>notebooks. instances. setAccelerator</code></p>
<p><code>notebooks.instances.setLabels</code></p>
<p><code>notebooks. instances. setMachineType</code></p>
<p><code>notebooks.instances.start</code></p>
<p><code>notebooks.instances.stop</code></p>
<p><code>notebooks.instances.update</code></p>
<p><code>notebooks. instances. updateConfig</code></p>
<p><code>notebooks. instances. updateShieldInstanceConfig</code></p>
<p><code>notebooks.instances.upgrade</code></p>
<p><code>notebooks.instances.use</code></p>
<p><code>notebooks.locations.*</code></p>
<ul>
<li><code>notebooks.locations.get</code></li>
<li><code>notebooks.locations.list</code></li>
</ul>
<p><code>notebooks.operations.*</code></p>
<ul>
<li><code>notebooks.operations.cancel</code></li>
<li><code>notebooks.operations.delete</code></li>
<li><code>notebooks.operations.get</code></li>
<li><code>notebooks.operations.list</code></li>
</ul>
<p><code>notebooks.runtimes.create</code></p>
<p><code>notebooks.runtimes.delete</code></p>
<p><code>notebooks.runtimes.diagnose</code></p>
<p><code>notebooks.runtimes.get</code></p>
<p><code>notebooks. runtimes. getIamPolicy</code></p>
<p><code>notebooks.runtimes.list</code></p>
<p><code>notebooks.runtimes.reset</code></p>
<p><code>notebooks.runtimes.start</code></p>
<p><code>notebooks.runtimes.stop</code></p>
<p><code>notebooks.runtimes.switch</code></p>
<p><code>notebooks.runtimes.update</code></p>
<p><code>notebooks.runtimes.upgrade</code></p>
<p><code>notebooks.schedules.create</code></p>
<p><code>notebooks.schedules.delete</code></p>
<p><code>notebooks.schedules.get</code></p>
<p><code>notebooks. schedules. getIamPolicy</code></p>
<p><code>notebooks.schedules.list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p>
<p><code>serviceusage. consumerpolicy. analyze</code></p>
<p><code>serviceusage. consumerpolicy. get</code></p>
<p><code>serviceusage. effectivepolicy. get</code></p>
<p><code>serviceusage.groups.*</code></p>
<ul>
<li><code>serviceusage.groups.list</code></li>
<li><code>serviceusage. groups. listExpandedMembers</code></li>
<li><code>serviceusage. groups. listMembers</code></li>
</ul>
<p><code>serviceusage.quotas.get</code></p>
<p><code>serviceusage.services.get</code></p>
<p><code>serviceusage.services.list</code></p>
<p><code>serviceusage.values.test</code></p></td>
</tr>
<tr class="odd">
<td>Notebooks Viewer
<p>( <code>roles/ notebooks.viewer</code> )</p>
<p>Read-only access to Notebooks, all resources.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Instance</li>
</ul></td>
<td><p><code>aiplatform. notebookExecutionJobs. get</code></p>
<p><code>aiplatform. notebookExecutionJobs. list</code></p>
<p><code>aiplatform.schedules.get</code></p>
<p><code>aiplatform.schedules.list</code></p>
<p><code>compute.acceleratorTypes.*</code></p>
<ul>
<li><code>compute.acceleratorTypes.get</code></li>
<li><code>compute.acceleratorTypes.list</code></li>
</ul>
<p><code>compute.addresses.get</code></p>
<p><code>compute.addresses.list</code></p>
<p><code>compute. addresses. listEffectiveTags</code></p>
<p><code>compute. addresses. listTagBindings</code></p>
<p><code>compute.advice.capacity</code></p>
<p><code>compute.advice.capacityHistory</code></p>
<p><code>compute.autoscalers.get</code></p>
<p><code>compute.autoscalers.list</code></p>
<p><code>compute.backendBuckets.get</code></p>
<p><code>compute. backendBuckets. getIamPolicy</code></p>
<p><code>compute.backendBuckets.list</code></p>
<p><code>compute. backendBuckets. listEffectiveTags</code></p>
<p><code>compute. backendBuckets. listTagBindings</code></p>
<p><code>compute.backendServices.get</code></p>
<p><code>compute. backendServices. getIamPolicy</code></p>
<p><code>compute.backendServices.list</code></p>
<p><code>compute. backendServices. listEffectiveTags</code></p>
<p><code>compute. backendServices. listTagBindings</code></p>
<p><code>compute.commitments.get</code></p>
<p><code>compute.commitments.list</code></p>
<p><code>compute. commitments. listEffectiveTags</code></p>
<p><code>compute. commitments. listTagBindings</code></p>
<p><code>compute.crossSiteNetworks.get</code></p>
<p><code>compute.crossSiteNetworks.list</code></p>
<p><code>compute.diskSettings.get</code></p>
<p><code>compute.diskTypes.*</code></p>
<ul>
<li><code>compute.diskTypes.get</code></li>
<li><code>compute.diskTypes.list</code></li>
</ul>
<p><code>compute.disks.get</code></p>
<p><code>compute.disks.getIamPolicy</code></p>
<p><code>compute.disks.list</code></p>
<p><code>compute. disks. listEffectiveTags</code></p>
<p><code>compute.disks.listTagBindings</code></p>
<p><code>compute. externalVpnGateways. get</code></p>
<p><code>compute. externalVpnGateways. list</code></p>
<p><code>compute. externalVpnGateways. listEffectiveTags</code></p>
<p><code>compute. externalVpnGateways. listTagBindings</code></p>
<p><code>compute.firewallPolicies.get</code></p>
<p><code>compute. firewallPolicies. getIamPolicy</code></p>
<p><code>compute.firewallPolicies.list</code></p>
<p><code>compute. firewallPolicies. listEffectiveTags</code></p>
<p><code>compute. firewallPolicies. listTagBindings</code></p>
<p><code>compute.firewalls.get</code></p>
<p><code>compute.firewalls.list</code></p>
<p><code>compute. firewalls. listEffectiveTags</code></p>
<p><code>compute. firewalls. listTagBindings</code></p>
<p><code>compute.forwardingRules.get</code></p>
<p><code>compute.forwardingRules.list</code></p>
<p><code>compute. forwardingRules. listEffectiveTags</code></p>
<p><code>compute. forwardingRules. listTagBindings</code></p>
<p><code>compute.futureReservations.get</code></p>
<p><code>compute. futureReservations. getIamPolicy</code></p>
<p><code>compute. futureReservations. list</code></p>
<p><code>compute. futureReservations. listEffectiveTags</code></p>
<p><code>compute. futureReservations. listTagBindings</code></p>
<p><code>compute.globalAddresses.get</code></p>
<p><code>compute.globalAddresses.list</code></p>
<p><code>compute. globalAddresses. listEffectiveTags</code></p>
<p><code>compute. globalAddresses. listTagBindings</code></p>
<p><code>compute. globalForwardingRules. get</code></p>
<p><code>compute. globalForwardingRules. list</code></p>
<p><code>compute. globalForwardingRules. listEffectiveTags</code></p>
<p><code>compute. globalForwardingRules. listTagBindings</code></p>
<p><code>compute. globalFrontendSettings. get</code></p>
<p><code>compute. globalNetworkEndpointGroups. get</code></p>
<p><code>compute. globalNetworkEndpointGroups. list</code></p>
<p><code>compute. globalNetworkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. globalNetworkEndpointGroups. listTagBindings</code></p>
<p><code>compute.globalOperations.get</code></p>
<p><code>compute. globalOperations. getIamPolicy</code></p>
<p><code>compute.globalOperations.list</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. get</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. list</code></p>
<p><code>compute.healthChecks.get</code></p>
<p><code>compute.healthChecks.list</code></p>
<p><code>compute. healthChecks. listEffectiveTags</code></p>
<p><code>compute. healthChecks. listTagBindings</code></p>
<p><code>compute.hosts.*</code></p>
<ul>
<li><code>compute.hosts.get</code></li>
<li><code>compute.hosts.getVersion</code></li>
<li><code>compute.hosts.list</code></li>
</ul>
<p><code>compute.httpHealthChecks.get</code></p>
<p><code>compute.httpHealthChecks.list</code></p>
<p><code>compute. httpHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpHealthChecks. listTagBindings</code></p>
<p><code>compute.httpsHealthChecks.get</code></p>
<p><code>compute.httpsHealthChecks.list</code></p>
<p><code>compute. httpsHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpsHealthChecks. listTagBindings</code></p>
<p><code>compute.images.get</code></p>
<p><code>compute.images.getFromFamily</code></p>
<p><code>compute.images.getIamPolicy</code></p>
<p><code>compute.images.list</code></p>
<p><code>compute. images. listEffectiveTags</code></p>
<p><code>compute.images.listTagBindings</code></p>
<p><code>compute. instanceGroupManagers. get</code></p>
<p><code>compute. instanceGroupManagers. list</code></p>
<p><code>compute. instanceGroupManagers. listEffectiveTags</code></p>
<p><code>compute. instanceGroupManagers. listTagBindings</code></p>
<p><code>compute.instanceGroups.get</code></p>
<p><code>compute.instanceGroups.list</code></p>
<p><code>compute. instanceGroups. listEffectiveTags</code></p>
<p><code>compute. instanceGroups. listTagBindings</code></p>
<p><code>compute.instanceSettings.get</code></p>
<p><code>compute.instanceTemplates.get</code></p>
<p><code>compute. instanceTemplates. getIamPolicy</code></p>
<p><code>compute.instanceTemplates.list</code></p>
<p><code>compute.instances.get</code></p>
<p><code>compute. instances. getEffectiveFirewalls</code></p>
<p><code>compute. instances. getGuestAttributes</code></p>
<p><code>compute.instances.getIamPolicy</code></p>
<p><code>compute. instances. getScreenshot</code></p>
<p><code>compute. instances. getSerialPortOutput</code></p>
<p><code>compute. instances. getShieldedInstanceIdentity</code></p>
<p><code>compute. instances. getShieldedVmIdentity</code></p>
<p><code>compute. instances. getVmExtensionState</code></p>
<p><code>compute.instances.list</code></p>
<p><code>compute. instances. listEffectiveTags</code></p>
<p><code>compute. instances. listReferrers</code></p>
<p><code>compute. instances. listTagBindings</code></p>
<p><code>compute. instances. listVmExtensionStates</code></p>
<p><code>compute.instances.troubleshoot</code></p>
<p><code>compute. instantSnapshotGroups. get</code></p>
<p><code>compute. instantSnapshotGroups. getIamPolicy</code></p>
<p><code>compute. instantSnapshotGroups. list</code></p>
<p><code>compute.instantSnapshots.get</code></p>
<p><code>compute. instantSnapshots. getIamPolicy</code></p>
<p><code>compute.instantSnapshots.list</code></p>
<p><code>compute. instantSnapshots. listEffectiveTags</code></p>
<p><code>compute. instantSnapshots. listTagBindings</code></p>
<p><code>compute. interconnectAttachmentGroups. get</code></p>
<p><code>compute. interconnectAttachmentGroups. list</code></p>
<p><code>compute. interconnectAttachments. get</code></p>
<p><code>compute. interconnectAttachments. list</code></p>
<p><code>compute. interconnectAttachments. listEffectiveTags</code></p>
<p><code>compute. interconnectAttachments. listTagBindings</code></p>
<p><code>compute.interconnectGroups.get</code></p>
<p><code>compute. interconnectGroups. list</code></p>
<p><code>compute. interconnectLocations.*</code></p>
<ul>
<li><code>compute. interconnectLocations. get</code></li>
<li><code>compute. interconnectLocations. list</code></li>
</ul>
<p><code>compute. interconnectRemoteLocations.*</code></p>
<ul>
<li><code>compute. interconnectRemoteLocations. get</code></li>
<li><code>compute. interconnectRemoteLocations. list</code></li>
</ul>
<p><code>compute.interconnects.get</code></p>
<p><code>compute.interconnects.list</code></p>
<p><code>compute. interconnects. listEffectiveTags</code></p>
<p><code>compute. interconnects. listTagBindings</code></p>
<p><code>compute.licenseCodes.get</code></p>
<p><code>compute. licenseCodes. getIamPolicy</code></p>
<p><code>compute.licenseCodes.list</code></p>
<p><code>compute.licenses.get</code></p>
<p><code>compute.licenses.getIamPolicy</code></p>
<p><code>compute.licenses.list</code></p>
<p><code>compute. licenses. listEffectiveTags</code></p>
<p><code>compute. licenses. listTagBindings</code></p>
<p><code>compute.machineImages.get</code></p>
<p><code>compute. machineImages. getIamPolicy</code></p>
<p><code>compute.machineImages.list</code></p>
<p><code>compute. machineImages. listEffectiveTags</code></p>
<p><code>compute. machineImages. listTagBindings</code></p>
<p><code>compute.machineTypes.*</code></p>
<ul>
<li><code>compute.machineTypes.get</code></li>
<li><code>compute.machineTypes.list</code></li>
</ul>
<p><code>compute.managedRulesets.*</code></p>
<ul>
<li><code>compute.managedRulesets.get</code></li>
<li><code>compute.managedRulesets.list</code></li>
</ul>
<p><code>compute.multiMig.get</code></p>
<p><code>compute.multiMig.list</code></p>
<p><code>compute.multiMigMembers.*</code></p>
<ul>
<li><code>compute.multiMigMembers.get</code></li>
<li><code>compute.multiMigMembers.list</code></li>
</ul>
<p><code>compute.networkAttachments.get</code></p>
<p><code>compute. networkAttachments. getIamPolicy</code></p>
<p><code>compute. networkAttachments. list</code></p>
<p><code>compute. networkAttachments. listEffectiveTags</code></p>
<p><code>compute. networkAttachments. listTagBindings</code></p>
<p><code>compute. networkEdgeSecurityServices. get</code></p>
<p><code>compute. networkEdgeSecurityServices. list</code></p>
<p><code>compute. networkEdgeSecurityServices. listEffectiveTags</code></p>
<p><code>compute. networkEdgeSecurityServices. listTagBindings</code></p>
<p><code>compute. networkEndpointGroups. get</code></p>
<p><code>compute. networkEndpointGroups. list</code></p>
<p><code>compute. networkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. networkEndpointGroups. listTagBindings</code></p>
<p><code>compute.networkProfiles.*</code></p>
<ul>
<li><code>compute.networkProfiles.get</code></li>
<li><code>compute.networkProfiles.list</code></li>
</ul>
<p><code>compute.networks.get</code></p>
<p><code>compute. networks. getEffectiveFirewalls</code></p>
<p><code>compute. networks. getRegionEffectiveFirewalls</code></p>
<p><code>compute.networks.list</code></p>
<p><code>compute. networks. listEffectiveTags</code></p>
<p><code>compute. networks. listPeeringRoutes</code></p>
<p><code>compute. networks. listTagBindings</code></p>
<p><code>compute.nodeGroups.get</code></p>
<p><code>compute. nodeGroups. getIamPolicy</code></p>
<p><code>compute.nodeGroups.list</code></p>
<p><code>compute.nodeTemplates.get</code></p>
<p><code>compute. nodeTemplates. getIamPolicy</code></p>
<p><code>compute.nodeTemplates.list</code></p>
<p><code>compute.nodeTypes.*</code></p>
<ul>
<li><code>compute.nodeTypes.get</code></li>
<li><code>compute.nodeTypes.list</code></li>
</ul>
<p><code>compute.orgRolloutPlans.get</code></p>
<p><code>compute.orgRolloutPlans.list</code></p>
<p><code>compute.orgRollouts.get</code></p>
<p><code>compute.orgRollouts.list</code></p>
<p><code>compute. organizations. listAssociations</code></p>
<p><code>compute.packetMirrorings.get</code></p>
<p><code>compute.packetMirrorings.list</code></p>
<p><code>compute. packetMirrorings. listEffectiveTags</code></p>
<p><code>compute. packetMirrorings. listTagBindings</code></p>
<p><code>compute.previewFeatures.get</code></p>
<p><code>compute.previewFeatures.list</code></p>
<p><code>compute.projects.get</code></p>
<p><code>compute. publicAdvertisedPrefixes. get</code></p>
<p><code>compute. publicAdvertisedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. get</code></p>
<p><code>compute. publicDelegatedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. listEffectiveTags</code></p>
<p><code>compute. publicDelegatedPrefixes. listTagBindings</code></p>
<p><code>compute. recoverableSnapshots. get</code></p>
<p><code>compute. recoverableSnapshots. getIamPolicy</code></p>
<p><code>compute. recoverableSnapshots. list</code></p>
<p><code>compute. regionBackendBuckets. get</code></p>
<p><code>compute. regionBackendBuckets. getIamPolicy</code></p>
<p><code>compute. regionBackendBuckets. list</code></p>
<p><code>compute. regionBackendBuckets. listEffectiveTags</code></p>
<p><code>compute. regionBackendBuckets. listTagBindings</code></p>
<p><code>compute. regionBackendServices. get</code></p>
<p><code>compute. regionBackendServices. getIamPolicy</code></p>
<p><code>compute. regionBackendServices. list</code></p>
<p><code>compute. regionBackendServices. listEffectiveTags</code></p>
<p><code>compute. regionBackendServices. listTagBindings</code></p>
<p><code>compute. regionCompositeHealthChecks. get</code></p>
<p><code>compute. regionCompositeHealthChecks. list</code></p>
<p><code>compute. regionFirewallPolicies. get</code></p>
<p><code>compute. regionFirewallPolicies. getIamPolicy</code></p>
<p><code>compute. regionFirewallPolicies. list</code></p>
<p><code>compute. regionFirewallPolicies. listEffectiveTags</code></p>
<p><code>compute. regionFirewallPolicies. listTagBindings</code></p>
<p><code>compute. regionHealthAggregationPolicies. get</code></p>
<p><code>compute. regionHealthAggregationPolicies. list</code></p>
<p><code>compute. regionHealthCheckServices. get</code></p>
<p><code>compute. regionHealthCheckServices. list</code></p>
<p><code>compute.regionHealthChecks.get</code></p>
<p><code>compute. regionHealthChecks. list</code></p>
<p><code>compute. regionHealthChecks. listEffectiveTags</code></p>
<p><code>compute. regionHealthChecks. listTagBindings</code></p>
<p><code>compute. regionHealthSources. get</code></p>
<p><code>compute. regionHealthSources. list</code></p>
<p><code>compute. regionNetworkEndpointGroups. get</code></p>
<p><code>compute. regionNetworkEndpointGroups. list</code></p>
<p><code>compute. regionNetworkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. regionNetworkEndpointGroups. listTagBindings</code></p>
<p><code>compute. regionNetworkPolicies. get</code></p>
<p><code>compute. regionNetworkPolicies. list</code></p>
<p><code>compute. regionNotificationEndpoints. get</code></p>
<p><code>compute. regionNotificationEndpoints. list</code></p>
<p><code>compute.regionOperations.get</code></p>
<p><code>compute. regionOperations. getIamPolicy</code></p>
<p><code>compute.regionOperations.list</code></p>
<p><code>compute. regionSecurityPolicies. get</code></p>
<p><code>compute. regionSecurityPolicies. list</code></p>
<p><code>compute. regionSecurityPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSecurityPolicies. listTagBindings</code></p>
<p><code>compute. regionSslCertificates. get</code></p>
<p><code>compute. regionSslCertificates. list</code></p>
<p><code>compute. regionSslCertificates. listEffectiveTags</code></p>
<p><code>compute. regionSslCertificates. listTagBindings</code></p>
<p><code>compute.regionSslPolicies.get</code></p>
<p><code>compute. regionSslPolicies. getIamPolicy</code></p>
<p><code>compute.regionSslPolicies.list</code></p>
<p><code>compute. regionSslPolicies. listAvailableFeatures</code></p>
<p><code>compute. regionSslPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSslPolicies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpProxies. get</code></p>
<p><code>compute. regionTargetHttpProxies. list</code></p>
<p><code>compute. regionTargetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpProxies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpsProxies. get</code></p>
<p><code>compute. regionTargetHttpsProxies. list</code></p>
<p><code>compute. regionTargetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpsProxies. listTagBindings</code></p>
<p><code>compute. regionTargetTcpProxies. get</code></p>
<p><code>compute. regionTargetTcpProxies. list</code></p>
<p><code>compute. regionTargetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetTcpProxies. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.get</code></p>
<p><code>compute.regionUrlMaps.list</code></p>
<p><code>compute. regionUrlMaps. listEffectiveTags</code></p>
<p><code>compute. regionUrlMaps. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.validate</code></p>
<p><code>compute.regions.*</code></p>
<ul>
<li><code>compute.regions.get</code></li>
<li><code>compute.regions.list</code></li>
</ul>
<p><code>compute.reliabilityRisks.*</code></p>
<ul>
<li><code>compute.reliabilityRisks.get</code></li>
<li><code>compute.reliabilityRisks.list</code></li>
</ul>
<p><code>compute.reservationBlocks.get</code></p>
<p><code>compute.reservationBlocks.list</code></p>
<p><code>compute. reservationConsumedInstances. list</code></p>
<p><code>compute.reservationSlots.get</code></p>
<p><code>compute.reservationSlots.list</code></p>
<p><code>compute. reservationSubBlocks. get</code></p>
<p><code>compute. reservationSubBlocks. list</code></p>
<p><code>compute.reservations.get</code></p>
<p><code>compute.reservations.list</code></p>
<p><code>compute. reservations. listEffectiveTags</code></p>
<p><code>compute. reservations. listTagBindings</code></p>
<p><code>compute.resourcePolicies.get</code></p>
<p><code>compute. resourcePolicies. getIamPolicy</code></p>
<p><code>compute.resourcePolicies.list</code></p>
<p><code>compute.rolloutPlans.get</code></p>
<p><code>compute.rolloutPlans.list</code></p>
<p><code>compute.rollouts.get</code></p>
<p><code>compute.rollouts.list</code></p>
<p><code>compute.routers.get</code></p>
<p><code>compute.routers.getRoutePolicy</code></p>
<p><code>compute.routers.list</code></p>
<p><code>compute.routers.listBgpRoutes</code></p>
<p><code>compute. routers. listEffectiveTags</code></p>
<p><code>compute. routers. listRoutePolicies</code></p>
<p><code>compute. routers. listTagBindings</code></p>
<p><code>compute.routes.get</code></p>
<p><code>compute.routes.list</code></p>
<p><code>compute. routes. listEffectiveTags</code></p>
<p><code>compute.routes.listTagBindings</code></p>
<p><code>compute.securityPolicies.get</code></p>
<p><code>compute.securityPolicies.list</code></p>
<p><code>compute. securityPolicies. listEffectiveTags</code></p>
<p><code>compute. securityPolicies. listTagBindings</code></p>
<p><code>compute.serviceAttachments.get</code></p>
<p><code>compute. serviceAttachments. getIamPolicy</code></p>
<p><code>compute. serviceAttachments. list</code></p>
<p><code>compute. serviceAttachments. listEffectiveTags</code></p>
<p><code>compute. serviceAttachments. listTagBindings</code></p>
<p><code>compute.snapshotGroups.get</code></p>
<p><code>compute. snapshotGroups. getIamPolicy</code></p>
<p><code>compute.snapshotGroups.list</code></p>
<p><code>compute. snapshotRecycleBinPolicy. get</code></p>
<p><code>compute.snapshotSettings.get</code></p>
<p><code>compute.snapshots.get</code></p>
<p><code>compute. snapshots. getEffectiveRecycleBinRule</code></p>
<p><code>compute.snapshots.getIamPolicy</code></p>
<p><code>compute.snapshots.list</code></p>
<p><code>compute. snapshots. listEffectiveTags</code></p>
<p><code>compute. snapshots. listTagBindings</code></p>
<p><code>compute.spotAssistants.get</code></p>
<p><code>compute.sslCertificates.get</code></p>
<p><code>compute.sslCertificates.list</code></p>
<p><code>compute. sslCertificates. listEffectiveTags</code></p>
<p><code>compute. sslCertificates. listTagBindings</code></p>
<p><code>compute.sslPolicies.get</code></p>
<p><code>compute. sslPolicies. getIamPolicy</code></p>
<p><code>compute.sslPolicies.list</code></p>
<p><code>compute. sslPolicies. listAvailableFeatures</code></p>
<p><code>compute. sslPolicies. listEffectiveTags</code></p>
<p><code>compute. sslPolicies. listTagBindings</code></p>
<p><code>compute.storagePools.get</code></p>
<p><code>compute. storagePools. getIamPolicy</code></p>
<p><code>compute.storagePools.list</code></p>
<p><code>compute. storagePools. listEffectiveTags</code></p>
<p><code>compute. storagePools. listTagBindings</code></p>
<p><code>compute.subnetworks.get</code></p>
<p><code>compute. subnetworks. getIamPolicy</code></p>
<p><code>compute.subnetworks.list</code></p>
<p><code>compute. subnetworks. listEffectiveTags</code></p>
<p><code>compute. subnetworks. listTagBindings</code></p>
<p><code>compute.targetGrpcProxies.get</code></p>
<p><code>compute.targetGrpcProxies.list</code></p>
<p><code>compute. targetGrpcProxies. listEffectiveTags</code></p>
<p><code>compute. targetGrpcProxies. listTagBindings</code></p>
<p><code>compute.targetHttpProxies.get</code></p>
<p><code>compute.targetHttpProxies.list</code></p>
<p><code>compute. targetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpProxies. listTagBindings</code></p>
<p><code>compute.targetHttpsProxies.get</code></p>
<p><code>compute. targetHttpsProxies. list</code></p>
<p><code>compute. targetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpsProxies. listTagBindings</code></p>
<p><code>compute.targetInstances.get</code></p>
<p><code>compute.targetInstances.list</code></p>
<p><code>compute. targetInstances. listEffectiveTags</code></p>
<p><code>compute. targetInstances. listTagBindings</code></p>
<p><code>compute.targetPools.get</code></p>
<p><code>compute.targetPools.list</code></p>
<p><code>compute. targetPools. listEffectiveTags</code></p>
<p><code>compute. targetPools. listTagBindings</code></p>
<p><code>compute.targetSslProxies.get</code></p>
<p><code>compute.targetSslProxies.list</code></p>
<p><code>compute. targetSslProxies. listEffectiveTags</code></p>
<p><code>compute. targetSslProxies. listTagBindings</code></p>
<p><code>compute.targetTcpProxies.get</code></p>
<p><code>compute.targetTcpProxies.list</code></p>
<p><code>compute. targetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. targetTcpProxies. listTagBindings</code></p>
<p><code>compute.targetVpnGateways.get</code></p>
<p><code>compute.targetVpnGateways.list</code></p>
<p><code>compute. targetVpnGateways. listEffectiveTags</code></p>
<p><code>compute. targetVpnGateways. listTagBindings</code></p>
<p><code>compute.urlMaps.get</code></p>
<p><code>compute.urlMaps.list</code></p>
<p><code>compute. urlMaps. listEffectiveTags</code></p>
<p><code>compute. urlMaps. listTagBindings</code></p>
<p><code>compute.urlMaps.validate</code></p>
<p><code>compute. vmExtensionPolicies. get</code></p>
<p><code>compute. vmExtensionPolicies. list</code></p>
<p><code>compute.vpnGateways.get</code></p>
<p><code>compute.vpnGateways.list</code></p>
<p><code>compute. vpnGateways. listEffectiveTags</code></p>
<p><code>compute. vpnGateways. listTagBindings</code></p>
<p><code>compute.vpnTunnels.get</code></p>
<p><code>compute.vpnTunnels.list</code></p>
<p><code>compute. vpnTunnels. listEffectiveTags</code></p>
<p><code>compute. vpnTunnels. listTagBindings</code></p>
<p><code>compute.wireGroups.get</code></p>
<p><code>compute.wireGroups.list</code></p>
<p><code>compute.zoneOperations.get</code></p>
<p><code>compute. zoneOperations. getIamPolicy</code></p>
<p><code>compute.zoneOperations.list</code></p>
<p><code>compute.zones.*</code></p>
<ul>
<li><code>compute.zones.get</code></li>
<li><code>compute.zones.list</code></li>
</ul>
<p><code>notebooks.environments.get</code></p>
<p><code>notebooks. environments. getIamPolicy</code></p>
<p><code>notebooks.environments.list</code></p>
<p><code>notebooks.executions.get</code></p>
<p><code>notebooks. executions. getIamPolicy</code></p>
<p><code>notebooks.executions.list</code></p>
<p><code>notebooks. instances. checkUpgradability</code></p>
<p><code>notebooks.instances.get</code></p>
<p><code>notebooks.instances.getHealth</code></p>
<p><code>notebooks. instances. getIamPolicy</code></p>
<p><code>notebooks.instances.list</code></p>
<p><code>notebooks. instances. listEffectiveTags</code></p>
<p><code>notebooks. instances. listTagBindings</code></p>
<p><code>notebooks.locations.*</code></p>
<ul>
<li><code>notebooks.locations.get</code></li>
<li><code>notebooks.locations.list</code></li>
</ul>
<p><code>notebooks.operations.get</code></p>
<p><code>notebooks.operations.list</code></p>
<p><code>notebooks.runtimes.get</code></p>
<p><code>notebooks. runtimes. getIamPolicy</code></p>
<p><code>notebooks.runtimes.list</code></p>
<p><code>notebooks.schedules.get</code></p>
<p><code>notebooks. schedules. getIamPolicy</code></p>
<p><code>notebooks.schedules.list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p>
<p><code>serviceusage. consumerpolicy. analyze</code></p>
<p><code>serviceusage. consumerpolicy. get</code></p>
<p><code>serviceusage. effectivepolicy. get</code></p>
<p><code>serviceusage.groups.*</code></p>
<ul>
<li><code>serviceusage.groups.list</code></li>
<li><code>serviceusage. groups. listExpandedMembers</code></li>
<li><code>serviceusage. groups. listMembers</code></li>
</ul>
<p><code>serviceusage.quotas.get</code></p>
<p><code>serviceusage.services.get</code></p>
<p><code>serviceusage.services.list</code></p>
<p><code>serviceusage.values.test</code></p></td>
</tr>
<tr class="even">
<td>Notebooks Legacy Admin
<p>( <code>roles/ notebooks.legacyAdmin</code> )</p>
<p>Full access to Notebooks all resources through compute API.</p></td>
<td><p><code>backupdr. backupPlanAssociations. createForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. createForComputeInstance</code></p>
<p><code>backupdr. backupPlanAssociations. deleteForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. deleteForComputeInstance</code></p>
<p><code>backupdr. backupPlanAssociations. fetchForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. getForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. list</code></p>
<p><code>backupdr. backupPlanAssociations. triggerBackupForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. triggerBackupForComputeInstance</code></p>
<p><code>backupdr. backupPlanAssociations. updateForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. updateForComputeInstance</code></p>
<p><code>backupdr.backupPlans.get</code></p>
<p><code>backupdr.backupPlans.list</code></p>
<p><code>backupdr. backupPlans. useForComputeDisk</code></p>
<p><code>backupdr. backupPlans. useForComputeInstance</code></p>
<p><code>backupdr.backupVaults.get</code></p>
<p><code>backupdr.backupVaults.list</code></p>
<p><code>backupdr.locations.list</code></p>
<p><code>backupdr.operations.get</code></p>
<p><code>backupdr.operations.list</code></p>
<p><code>backupdr. serviceConfig. initialize</code></p>
<p><code>cloudkms.keyHandles.*</code></p>
<ul>
<li><code>cloudkms.keyHandles.create</code></li>
<li><code>cloudkms.keyHandles.get</code></li>
<li><code>cloudkms.keyHandles.list</code></li>
</ul>
<p><code>cloudkms.operations.get</code></p>
<p><code>cloudkms. projects. showEffectiveAutokeyConfig</code></p>
<p><code>compute.*</code></p>
<ul>
<li><code>compute.acceleratorTypes.get</code></li>
<li><code>compute.acceleratorTypes.list</code></li>
<li><code>compute.addresses.create</code></li>
<li><code>compute. addresses. createInternal</code></li>
<li><code>compute. addresses. createTagBinding</code></li>
<li><code>compute.addresses.delete</code></li>
<li><code>compute. addresses. deleteInternal</code></li>
<li><code>compute. addresses. deleteTagBinding</code></li>
<li><code>compute.addresses.get</code></li>
<li><code>compute.addresses.list</code></li>
<li><code>compute. addresses. listEffectiveTags</code></li>
<li><code>compute. addresses. listTagBindings</code></li>
<li><code>compute.addresses.setLabels</code></li>
<li><code>compute.addresses.use</code></li>
<li><code>compute.addresses.useInternal</code></li>
<li><code>compute.advice.calendarMode</code></li>
<li><code>compute.advice.capacity</code></li>
<li><code>compute.advice.capacityHistory</code></li>
<li><code>compute.autoscalers.create</code></li>
<li><code>compute.autoscalers.delete</code></li>
<li><code>compute.autoscalers.get</code></li>
<li><code>compute.autoscalers.list</code></li>
<li><code>compute.autoscalers.update</code></li>
<li><code>compute. backendBuckets. addSignedUrlKey</code></li>
<li><code>compute.backendBuckets.create</code></li>
<li><code>compute. backendBuckets. createTagBinding</code></li>
<li><code>compute.backendBuckets.delete</code></li>
<li><code>compute. backendBuckets. deleteSignedUrlKey</code></li>
<li><code>compute. backendBuckets. deleteTagBinding</code></li>
<li><code>compute.backendBuckets.get</code></li>
<li><code>compute. backendBuckets. getIamPolicy</code></li>
<li><code>compute.backendBuckets.list</code></li>
<li><code>compute. backendBuckets. listEffectiveTags</code></li>
<li><code>compute. backendBuckets. listTagBindings</code></li>
<li><code>compute. backendBuckets. setIamPolicy</code></li>
<li><code>compute. backendBuckets. setSecurityPolicy</code></li>
<li><code>compute.backendBuckets.update</code></li>
<li><code>compute.backendBuckets.use</code></li>
<li><code>compute. backendServices. addSignedUrlKey</code></li>
<li><code>compute.backendServices.create</code></li>
<li><code>compute. backendServices. createTagBinding</code></li>
<li><code>compute.backendServices.delete</code></li>
<li><code>compute. backendServices. deleteSignedUrlKey</code></li>
<li><code>compute. backendServices. deleteTagBinding</code></li>
<li><code>compute.backendServices.get</code></li>
<li><code>compute. backendServices. getIamPolicy</code></li>
<li><code>compute.backendServices.list</code></li>
<li><code>compute. backendServices. listEffectiveTags</code></li>
<li><code>compute. backendServices. listTagBindings</code></li>
<li><code>compute. backendServices. setIamPolicy</code></li>
<li><code>compute. backendServices. setSecurityPolicy</code></li>
<li><code>compute.backendServices.update</code></li>
<li><code>compute.backendServices.use</code></li>
<li><code>compute.commitments.create</code></li>
<li><code>compute. commitments. createTagBinding</code></li>
<li><code>compute. commitments. deleteTagBinding</code></li>
<li><code>compute.commitments.get</code></li>
<li><code>compute.commitments.list</code></li>
<li><code>compute. commitments. listEffectiveTags</code></li>
<li><code>compute. commitments. listTagBindings</code></li>
<li><code>compute.commitments.update</code></li>
<li><code>compute. commitments. updateReservations</code></li>
<li><code>compute. crossSiteNetworks. create</code></li>
<li><code>compute. crossSiteNetworks. delete</code></li>
<li><code>compute.crossSiteNetworks.get</code></li>
<li><code>compute.crossSiteNetworks.list</code></li>
<li><code>compute. crossSiteNetworks. update</code></li>
<li><code>compute.diskSettings.get</code></li>
<li><code>compute.diskSettings.update</code></li>
<li><code>compute.diskTypes.get</code></li>
<li><code>compute.diskTypes.list</code></li>
<li><code>compute. disks. addResourcePolicies</code></li>
<li><code>compute.disks.create</code></li>
<li><code>compute.disks.createSnapshot</code></li>
<li><code>compute.disks.createTagBinding</code></li>
<li><code>compute.disks.delete</code></li>
<li><code>compute.disks.deleteTagBinding</code></li>
<li><code>compute.disks.get</code></li>
<li><code>compute.disks.getIamPolicy</code></li>
<li><code>compute.disks.list</code></li>
<li><code>compute. disks. listEffectiveTags</code></li>
<li><code>compute.disks.listTagBindings</code></li>
<li><code>compute. disks. removeResourcePolicies</code></li>
<li><code>compute.disks.resize</code></li>
<li><code>compute.disks.setIamPolicy</code></li>
<li><code>compute.disks.setLabels</code></li>
<li><code>compute. disks. startAsyncReplication</code></li>
<li><code>compute. disks. stopAsyncReplication</code></li>
<li><code>compute. disks. stopGroupAsyncReplication</code></li>
<li><code>compute.disks.update</code></li>
<li><code>compute.disks.updateKmsKey</code></li>
<li><code>compute.disks.use</code></li>
<li><code>compute.disks.useReadOnly</code></li>
<li><code>compute. externalVpnGateways. create</code></li>
<li><code>compute. externalVpnGateways. createTagBinding</code></li>
<li><code>compute. externalVpnGateways. delete</code></li>
<li><code>compute. externalVpnGateways. deleteTagBinding</code></li>
<li><code>compute. externalVpnGateways. get</code></li>
<li><code>compute. externalVpnGateways. list</code></li>
<li><code>compute. externalVpnGateways. listEffectiveTags</code></li>
<li><code>compute. externalVpnGateways. listTagBindings</code></li>
<li><code>compute. externalVpnGateways. setLabels</code></li>
<li><code>compute. externalVpnGateways. use</code></li>
<li><code>compute. firewallPolicies. cloneRules</code></li>
<li><code>compute. firewallPolicies. copyRules</code></li>
<li><code>compute. firewallPolicies. create</code></li>
<li><code>compute. firewallPolicies. createTagBinding</code></li>
<li><code>compute. firewallPolicies. delete</code></li>
<li><code>compute. firewallPolicies. deleteTagBinding</code></li>
<li><code>compute.firewallPolicies.get</code></li>
<li><code>compute. firewallPolicies. getIamPolicy</code></li>
<li><code>compute.firewallPolicies.list</code></li>
<li><code>compute. firewallPolicies. listEffectiveTags</code></li>
<li><code>compute. firewallPolicies. listTagBindings</code></li>
<li><code>compute.firewallPolicies.move</code></li>
<li><code>compute. firewallPolicies. setIamPolicy</code></li>
<li><code>compute. firewallPolicies. update</code></li>
<li><code>compute.firewallPolicies.use</code></li>
<li><code>compute.firewalls.create</code></li>
<li><code>compute. firewalls. createTagBinding</code></li>
<li><code>compute.firewalls.delete</code></li>
<li><code>compute. firewalls. deleteTagBinding</code></li>
<li><code>compute.firewalls.get</code></li>
<li><code>compute.firewalls.list</code></li>
<li><code>compute. firewalls. listEffectiveTags</code></li>
<li><code>compute. firewalls. listTagBindings</code></li>
<li><code>compute.firewalls.update</code></li>
<li><code>compute.forwardingRules.create</code></li>
<li><code>compute. forwardingRules. createTagBinding</code></li>
<li><code>compute.forwardingRules.delete</code></li>
<li><code>compute. forwardingRules. deleteTagBinding</code></li>
<li><code>compute.forwardingRules.get</code></li>
<li><code>compute.forwardingRules.list</code></li>
<li><code>compute. forwardingRules. listEffectiveTags</code></li>
<li><code>compute. forwardingRules. listTagBindings</code></li>
<li><code>compute. forwardingRules. pscCreate</code></li>
<li><code>compute. forwardingRules. pscDelete</code></li>
<li><code>compute. forwardingRules. pscSetLabels</code></li>
<li><code>compute. forwardingRules. pscUpdate</code></li>
<li><code>compute. forwardingRules. setLabels</code></li>
<li><code>compute. forwardingRules. setTarget</code></li>
<li><code>compute.forwardingRules.update</code></li>
<li><code>compute.forwardingRules.use</code></li>
<li><code>compute. futureReservations. cancel</code></li>
<li><code>compute. futureReservations. create</code></li>
<li><code>compute. futureReservations. createTagBinding</code></li>
<li><code>compute. futureReservations. delete</code></li>
<li><code>compute. futureReservations. deleteTagBinding</code></li>
<li><code>compute.futureReservations.get</code></li>
<li><code>compute. futureReservations. getIamPolicy</code></li>
<li><code>compute. futureReservations. list</code></li>
<li><code>compute. futureReservations. listEffectiveTags</code></li>
<li><code>compute. futureReservations. listTagBindings</code></li>
<li><code>compute. futureReservations. setIamPolicy</code></li>
<li><code>compute. futureReservations. update</code></li>
<li><code>compute.globalAddresses.create</code></li>
<li><code>compute. globalAddresses. createInternal</code></li>
<li><code>compute. globalAddresses. createTagBinding</code></li>
<li><code>compute.globalAddresses.delete</code></li>
<li><code>compute. globalAddresses. deleteInternal</code></li>
<li><code>compute. globalAddresses. deleteTagBinding</code></li>
<li><code>compute.globalAddresses.get</code></li>
<li><code>compute.globalAddresses.list</code></li>
<li><code>compute. globalAddresses. listEffectiveTags</code></li>
<li><code>compute. globalAddresses. listTagBindings</code></li>
<li><code>compute. globalAddresses. setLabels</code></li>
<li><code>compute.globalAddresses.use</code></li>
<li><code>compute. globalForwardingRules. create</code></li>
<li><code>compute. globalForwardingRules. createTagBinding</code></li>
<li><code>compute. globalForwardingRules. delete</code></li>
<li><code>compute. globalForwardingRules. deleteTagBinding</code></li>
<li><code>compute. globalForwardingRules. get</code></li>
<li><code>compute. globalForwardingRules. list</code></li>
<li><code>compute. globalForwardingRules. listEffectiveTags</code></li>
<li><code>compute. globalForwardingRules. listTagBindings</code></li>
<li><code>compute. globalForwardingRules. pscCreate</code></li>
<li><code>compute. globalForwardingRules. pscDelete</code></li>
<li><code>compute. globalForwardingRules. pscSetLabels</code></li>
<li><code>compute. globalForwardingRules. pscUpdate</code></li>
<li><code>compute. globalForwardingRules. setLabels</code></li>
<li><code>compute. globalForwardingRules. setTarget</code></li>
<li><code>compute. globalForwardingRules. update</code></li>
<li><code>compute. globalFrontendSettings. get</code></li>
<li><code>compute. globalFrontendSettings. update</code></li>
<li><code>compute. globalNetworkEndpointGroups. attachNetworkEndpoints</code></li>
<li><code>compute. globalNetworkEndpointGroups. create</code></li>
<li><code>compute. globalNetworkEndpointGroups. createTagBinding</code></li>
<li><code>compute. globalNetworkEndpointGroups. delete</code></li>
<li><code>compute. globalNetworkEndpointGroups. deleteTagBinding</code></li>
<li><code>compute. globalNetworkEndpointGroups. detachNetworkEndpoints</code></li>
<li><code>compute. globalNetworkEndpointGroups. get</code></li>
<li><code>compute. globalNetworkEndpointGroups. list</code></li>
<li><code>compute. globalNetworkEndpointGroups. listEffectiveTags</code></li>
<li><code>compute. globalNetworkEndpointGroups. listTagBindings</code></li>
<li><code>compute. globalNetworkEndpointGroups. use</code></li>
<li><code>compute. globalOperations. delete</code></li>
<li><code>compute.globalOperations.get</code></li>
<li><code>compute. globalOperations. getIamPolicy</code></li>
<li><code>compute.globalOperations.list</code></li>
<li><code>compute. globalOperations. setIamPolicy</code></li>
<li><code>compute. globalPublicDelegatedPrefixes. create</code></li>
<li><code>compute. globalPublicDelegatedPrefixes. delete</code></li>
<li><code>compute. globalPublicDelegatedPrefixes. get</code></li>
<li><code>compute. globalPublicDelegatedPrefixes. list</code></li>
<li><code>compute. globalPublicDelegatedPrefixes. updatePolicy</code></li>
<li><code>compute.healthChecks.create</code></li>
<li><code>compute. healthChecks. createTagBinding</code></li>
<li><code>compute.healthChecks.delete</code></li>
<li><code>compute. healthChecks. deleteTagBinding</code></li>
<li><code>compute.healthChecks.get</code></li>
<li><code>compute.healthChecks.list</code></li>
<li><code>compute. healthChecks. listEffectiveTags</code></li>
<li><code>compute. healthChecks. listTagBindings</code></li>
<li><code>compute.healthChecks.update</code></li>
<li><code>compute.healthChecks.use</code></li>
<li><code>compute. healthChecks. useReadOnly</code></li>
<li><code>compute.hosts.get</code></li>
<li><code>compute.hosts.getVersion</code></li>
<li><code>compute.hosts.list</code></li>
<li><code>compute. httpHealthChecks. create</code></li>
<li><code>compute. httpHealthChecks. createTagBinding</code></li>
<li><code>compute. httpHealthChecks. delete</code></li>
<li><code>compute. httpHealthChecks. deleteTagBinding</code></li>
<li><code>compute.httpHealthChecks.get</code></li>
<li><code>compute.httpHealthChecks.list</code></li>
<li><code>compute. httpHealthChecks. listEffectiveTags</code></li>
<li><code>compute. httpHealthChecks. listTagBindings</code></li>
<li><code>compute. httpHealthChecks. update</code></li>
<li><code>compute.httpHealthChecks.use</code></li>
<li><code>compute. httpHealthChecks. useReadOnly</code></li>
<li><code>compute. httpsHealthChecks. create</code></li>
<li><code>compute. httpsHealthChecks. createTagBinding</code></li>
<li><code>compute. httpsHealthChecks. delete</code></li>
<li><code>compute. httpsHealthChecks. deleteTagBinding</code></li>
<li><code>compute.httpsHealthChecks.get</code></li>
<li><code>compute.httpsHealthChecks.list</code></li>
<li><code>compute. httpsHealthChecks. listEffectiveTags</code></li>
<li><code>compute. httpsHealthChecks. listTagBindings</code></li>
<li><code>compute. httpsHealthChecks. update</code></li>
<li><code>compute.httpsHealthChecks.use</code></li>
<li><code>compute. httpsHealthChecks. useReadOnly</code></li>
<li><code>compute.images.create</code></li>
<li><code>compute. images. createTagBinding</code></li>
<li><code>compute.images.delete</code></li>
<li><code>compute. images. deleteTagBinding</code></li>
<li><code>compute.images.deprecate</code></li>
<li><code>compute.images.get</code></li>
<li><code>compute.images.getFromFamily</code></li>
<li><code>compute.images.getIamPolicy</code></li>
<li><code>compute.images.list</code></li>
<li><code>compute. images. listEffectiveTags</code></li>
<li><code>compute.images.listTagBindings</code></li>
<li><code>compute.images.setIamPolicy</code></li>
<li><code>compute.images.setLabels</code></li>
<li><code>compute.images.update</code></li>
<li><code>compute.images.useReadOnly</code></li>
<li><code>compute. instanceGroupManagers. create</code></li>
<li><code>compute. instanceGroupManagers. createTagBinding</code></li>
<li><code>compute. instanceGroupManagers. delete</code></li>
<li><code>compute. instanceGroupManagers. deleteTagBinding</code></li>
<li><code>compute. instanceGroupManagers. get</code></li>
<li><code>compute. instanceGroupManagers. list</code></li>
<li><code>compute. instanceGroupManagers. listEffectiveTags</code></li>
<li><code>compute. instanceGroupManagers. listTagBindings</code></li>
<li><code>compute. instanceGroupManagers. update</code></li>
<li><code>compute. instanceGroupManagers. use</code></li>
<li><code>compute.instanceGroups.create</code></li>
<li><code>compute. instanceGroups. createTagBinding</code></li>
<li><code>compute.instanceGroups.delete</code></li>
<li><code>compute. instanceGroups. deleteTagBinding</code></li>
<li><code>compute.instanceGroups.get</code></li>
<li><code>compute.instanceGroups.list</code></li>
<li><code>compute. instanceGroups. listEffectiveTags</code></li>
<li><code>compute. instanceGroups. listTagBindings</code></li>
<li><code>compute.instanceGroups.update</code></li>
<li><code>compute.instanceGroups.use</code></li>
<li><code>compute.instanceSettings.get</code></li>
<li><code>compute. instanceSettings. update</code></li>
<li><code>compute. instanceTemplates. create</code></li>
<li><code>compute. instanceTemplates. delete</code></li>
<li><code>compute.instanceTemplates.get</code></li>
<li><code>compute. instanceTemplates. getIamPolicy</code></li>
<li><code>compute.instanceTemplates.list</code></li>
<li><code>compute. instanceTemplates. setIamPolicy</code></li>
<li><code>compute. instanceTemplates. useReadOnly</code></li>
<li><code>compute. instances. addAccessConfig</code></li>
<li><code>compute. instances. addNetworkInterface</code></li>
<li><code>compute. instances. addResourcePolicies</code></li>
<li><code>compute.instances.attachDisk</code></li>
<li><code>compute.instances.create</code></li>
<li><code>compute. instances. createTagBinding</code></li>
<li><code>compute.instances.delete</code></li>
<li><code>compute. instances. deleteAccessConfig</code></li>
<li><code>compute. instances. deleteNetworkInterface</code></li>
<li><code>compute. instances. deleteTagBinding</code></li>
<li><code>compute.instances.detachDisk</code></li>
<li><code>compute.instances.get</code></li>
<li><code>compute. instances. getEffectiveFirewalls</code></li>
<li><code>compute. instances. getGuestAttributes</code></li>
<li><code>compute.instances.getIamPolicy</code></li>
<li><code>compute. instances. getScreenshot</code></li>
<li><code>compute. instances. getSerialPortOutput</code></li>
<li><code>compute. instances. getShieldedInstanceIdentity</code></li>
<li><code>compute. instances. getShieldedVmIdentity</code></li>
<li><code>compute. instances. getVmExtensionState</code></li>
<li><code>compute.instances.list</code></li>
<li><code>compute. instances. listEffectiveTags</code></li>
<li><code>compute. instances. listReferrers</code></li>
<li><code>compute. instances. listTagBindings</code></li>
<li><code>compute. instances. listVmExtensionStates</code></li>
<li><code>compute.instances.osAdminLogin</code></li>
<li><code>compute.instances.osLogin</code></li>
<li><code>compute. instances. pscInterfaceCreate</code></li>
<li><code>compute. instances. removeResourcePolicies</code></li>
<li><code>compute.instances.reset</code></li>
<li><code>compute.instances.resume</code></li>
<li><code>compute. instances. sendDiagnosticInterrupt</code></li>
<li><code>compute. instances. setDeletionProtection</code></li>
<li><code>compute. instances. setDiskAutoDelete</code></li>
<li><code>compute.instances.setIamPolicy</code></li>
<li><code>compute.instances.setLabels</code></li>
<li><code>compute. instances. setMachineResources</code></li>
<li><code>compute. instances. setMachineType</code></li>
<li><code>compute.instances.setMetadata</code></li>
<li><code>compute. instances. setMinCpuPlatform</code></li>
<li><code>compute.instances.setName</code></li>
<li><code>compute. instances. setScheduling</code></li>
<li><code>compute. instances. setSecurityPolicy</code></li>
<li><code>compute. instances. setServiceAccount</code></li>
<li><code>compute. instances. setShieldedInstanceIntegrityPolicy</code></li>
<li><code>compute. instances. setShieldedVmIntegrityPolicy</code></li>
<li><code>compute.instances.setTags</code></li>
<li><code>compute. instances. simulateMaintenanceEvent</code></li>
<li><code>compute.instances.start</code></li>
<li><code>compute. instances. startWithEncryptionKey</code></li>
<li><code>compute.instances.stop</code></li>
<li><code>compute.instances.suspend</code></li>
<li><code>compute.instances.troubleshoot</code></li>
<li><code>compute.instances.update</code></li>
<li><code>compute. instances. updateAccessConfig</code></li>
<li><code>compute. instances. updateDisplayDevice</code></li>
<li><code>compute. instances. updateNetworkInterface</code></li>
<li><code>compute. instances. updateSecurity</code></li>
<li><code>compute. instances. updateShieldedInstanceConfig</code></li>
<li><code>compute. instances. updateShieldedVmConfig</code></li>
<li><code>compute.instances.use</code></li>
<li><code>compute.instances.useReadOnly</code></li>
<li><code>compute. instantSnapshotGroups. create</code></li>
<li><code>compute. instantSnapshotGroups. delete</code></li>
<li><code>compute. instantSnapshotGroups. get</code></li>
<li><code>compute. instantSnapshotGroups. getIamPolicy</code></li>
<li><code>compute. instantSnapshotGroups. list</code></li>
<li><code>compute. instantSnapshotGroups. setIamPolicy</code></li>
<li><code>compute. instantSnapshotGroups. useReadOnly</code></li>
<li><code>compute. instantSnapshots. create</code></li>
<li><code>compute. instantSnapshots. createTagBinding</code></li>
<li><code>compute. instantSnapshots. delete</code></li>
<li><code>compute. instantSnapshots. deleteTagBinding</code></li>
<li><code>compute. instantSnapshots. export</code></li>
<li><code>compute.instantSnapshots.get</code></li>
<li><code>compute. instantSnapshots. getIamPolicy</code></li>
<li><code>compute.instantSnapshots.list</code></li>
<li><code>compute. instantSnapshots. listEffectiveTags</code></li>
<li><code>compute. instantSnapshots. listTagBindings</code></li>
<li><code>compute. instantSnapshots. setIamPolicy</code></li>
<li><code>compute. instantSnapshots. setLabels</code></li>
<li><code>compute. instantSnapshots. useReadOnly</code></li>
<li><code>compute. interconnectAttachmentGroups. create</code></li>
<li><code>compute. interconnectAttachmentGroups. delete</code></li>
<li><code>compute. interconnectAttachmentGroups. get</code></li>
<li><code>compute. interconnectAttachmentGroups. list</code></li>
<li><code>compute. interconnectAttachmentGroups. patch</code></li>
<li><code>compute. interconnectAttachments. create</code></li>
<li><code>compute. interconnectAttachments. createTagBinding</code></li>
<li><code>compute. interconnectAttachments. delete</code></li>
<li><code>compute. interconnectAttachments. deleteTagBinding</code></li>
<li><code>compute. interconnectAttachments. get</code></li>
<li><code>compute. interconnectAttachments. list</code></li>
<li><code>compute. interconnectAttachments. listEffectiveTags</code></li>
<li><code>compute. interconnectAttachments. listTagBindings</code></li>
<li><code>compute. interconnectAttachments. setLabels</code></li>
<li><code>compute. interconnectAttachments. update</code></li>
<li><code>compute. interconnectAttachments. use</code></li>
<li><code>compute. interconnectGroups. create</code></li>
<li><code>compute. interconnectGroups. delete</code></li>
<li><code>compute.interconnectGroups.get</code></li>
<li><code>compute. interconnectGroups. list</code></li>
<li><code>compute. interconnectGroups. patch</code></li>
<li><code>compute. interconnectLocations. get</code></li>
<li><code>compute. interconnectLocations. list</code></li>
<li><code>compute. interconnectRemoteLocations. get</code></li>
<li><code>compute. interconnectRemoteLocations. list</code></li>
<li><code>compute.interconnects.create</code></li>
<li><code>compute. interconnects. createTagBinding</code></li>
<li><code>compute.interconnects.delete</code></li>
<li><code>compute. interconnects. deleteTagBinding</code></li>
<li><code>compute.interconnects.get</code></li>
<li><code>compute. interconnects. getMacsecConfig</code></li>
<li><code>compute.interconnects.list</code></li>
<li><code>compute. interconnects. listEffectiveTags</code></li>
<li><code>compute. interconnects. listTagBindings</code></li>
<li><code>compute. interconnects. setLabels</code></li>
<li><code>compute.interconnects.setName</code></li>
<li><code>compute.interconnects.update</code></li>
<li><code>compute.interconnects.use</code></li>
<li><code>compute.licenseCodes.get</code></li>
<li><code>compute. licenseCodes. getIamPolicy</code></li>
<li><code>compute.licenseCodes.list</code></li>
<li><code>compute. licenseCodes. setIamPolicy</code></li>
<li><code>compute.licenses.create</code></li>
<li><code>compute. licenses. createTagBinding</code></li>
<li><code>compute.licenses.delete</code></li>
<li><code>compute. licenses. deleteTagBinding</code></li>
<li><code>compute.licenses.get</code></li>
<li><code>compute.licenses.getIamPolicy</code></li>
<li><code>compute.licenses.list</code></li>
<li><code>compute. licenses. listEffectiveTags</code></li>
<li><code>compute. licenses. listTagBindings</code></li>
<li><code>compute.licenses.setIamPolicy</code></li>
<li><code>compute.licenses.update</code></li>
<li><code>compute.machineImages.create</code></li>
<li><code>compute. machineImages. createTagBinding</code></li>
<li><code>compute.machineImages.delete</code></li>
<li><code>compute. machineImages. deleteTagBinding</code></li>
<li><code>compute.machineImages.get</code></li>
<li><code>compute. machineImages. getIamPolicy</code></li>
<li><code>compute.machineImages.list</code></li>
<li><code>compute. machineImages. listEffectiveTags</code></li>
<li><code>compute. machineImages. listTagBindings</code></li>
<li><code>compute. machineImages. setIamPolicy</code></li>
<li><code>compute. machineImages. setLabels</code></li>
<li><code>compute. machineImages. useReadOnly</code></li>
<li><code>compute.machineTypes.get</code></li>
<li><code>compute.machineTypes.list</code></li>
<li><code>compute.managedRulesets.get</code></li>
<li><code>compute.managedRulesets.list</code></li>
<li><code>compute.multiMig.create</code></li>
<li><code>compute.multiMig.delete</code></li>
<li><code>compute.multiMig.get</code></li>
<li><code>compute.multiMig.list</code></li>
<li><code>compute.multiMigMembers.get</code></li>
<li><code>compute.multiMigMembers.list</code></li>
<li><code>compute. networkAttachments. create</code></li>
<li><code>compute. networkAttachments. createTagBinding</code></li>
<li><code>compute. networkAttachments. delete</code></li>
<li><code>compute. networkAttachments. deleteTagBinding</code></li>
<li><code>compute.networkAttachments.get</code></li>
<li><code>compute. networkAttachments. getIamPolicy</code></li>
<li><code>compute. networkAttachments. list</code></li>
<li><code>compute. networkAttachments. listEffectiveTags</code></li>
<li><code>compute. networkAttachments. listTagBindings</code></li>
<li><code>compute. networkAttachments. setIamPolicy</code></li>
<li><code>compute. networkAttachments. update</code></li>
<li><code>compute.networkAttachments.use</code></li>
<li><code>compute. networkEdgeSecurityServices. create</code></li>
<li><code>compute. networkEdgeSecurityServices. createTagBinding</code></li>
<li><code>compute. networkEdgeSecurityServices. delete</code></li>
<li><code>compute. networkEdgeSecurityServices. deleteTagBinding</code></li>
<li><code>compute. networkEdgeSecurityServices. get</code></li>
<li><code>compute. networkEdgeSecurityServices. list</code></li>
<li><code>compute. networkEdgeSecurityServices. listEffectiveTags</code></li>
<li><code>compute. networkEdgeSecurityServices. listTagBindings</code></li>
<li><code>compute. networkEdgeSecurityServices. update</code></li>
<li><code>compute. networkEndpointGroups. attachNetworkEndpoints</code></li>
<li><code>compute. networkEndpointGroups. create</code></li>
<li><code>compute. networkEndpointGroups. createTagBinding</code></li>
<li><code>compute. networkEndpointGroups. delete</code></li>
<li><code>compute. networkEndpointGroups. deleteTagBinding</code></li>
<li><code>compute. networkEndpointGroups. detachNetworkEndpoints</code></li>
<li><code>compute. networkEndpointGroups. get</code></li>
<li><code>compute. networkEndpointGroups. list</code></li>
<li><code>compute. networkEndpointGroups. listEffectiveTags</code></li>
<li><code>compute. networkEndpointGroups. listTagBindings</code></li>
<li><code>compute. networkEndpointGroups. use</code></li>
<li><code>compute.networkProfiles.get</code></li>
<li><code>compute.networkProfiles.list</code></li>
<li><code>compute.networks.access</code></li>
<li><code>compute.networks.addPeering</code></li>
<li><code>compute.networks.create</code></li>
<li><code>compute. networks. createTagBinding</code></li>
<li><code>compute.networks.delete</code></li>
<li><code>compute. networks. deleteTagBinding</code></li>
<li><code>compute.networks.get</code></li>
<li><code>compute. networks. getEffectiveFirewalls</code></li>
<li><code>compute. networks. getRegionEffectiveFirewalls</code></li>
<li><code>compute.networks.list</code></li>
<li><code>compute. networks. listEffectiveTags</code></li>
<li><code>compute. networks. listPeeringRoutes</code></li>
<li><code>compute. networks. listTagBindings</code></li>
<li><code>compute.networks.mirror</code></li>
<li><code>compute.networks.removePeering</code></li>
<li><code>compute. networks. setFirewallPolicy</code></li>
<li><code>compute. networks. setNetworkPolicy</code></li>
<li><code>compute. networks. switchToCustomMode</code></li>
<li><code>compute.networks.update</code></li>
<li><code>compute.networks.updatePeering</code></li>
<li><code>compute.networks.updatePolicy</code></li>
<li><code>compute.networks.use</code></li>
<li><code>compute.networks.useExternalIp</code></li>
<li><code>compute.nodeGroups.addNodes</code></li>
<li><code>compute.nodeGroups.create</code></li>
<li><code>compute.nodeGroups.delete</code></li>
<li><code>compute.nodeGroups.deleteNodes</code></li>
<li><code>compute.nodeGroups.get</code></li>
<li><code>compute. nodeGroups. getIamPolicy</code></li>
<li><code>compute.nodeGroups.list</code></li>
<li><code>compute. nodeGroups. performMaintenance</code></li>
<li><code>compute. nodeGroups. setIamPolicy</code></li>
<li><code>compute. nodeGroups. setNodeTemplate</code></li>
<li><code>compute. nodeGroups. simulateMaintenanceEvent</code></li>
<li><code>compute.nodeGroups.update</code></li>
<li><code>compute.nodeTemplates.create</code></li>
<li><code>compute.nodeTemplates.delete</code></li>
<li><code>compute.nodeTemplates.get</code></li>
<li><code>compute. nodeTemplates. getIamPolicy</code></li>
<li><code>compute.nodeTemplates.list</code></li>
<li><code>compute. nodeTemplates. setIamPolicy</code></li>
<li><code>compute.nodeTypes.get</code></li>
<li><code>compute.nodeTypes.list</code></li>
<li><code>compute.orgRolloutPlans.create</code></li>
<li><code>compute.orgRolloutPlans.delete</code></li>
<li><code>compute.orgRolloutPlans.get</code></li>
<li><code>compute.orgRolloutPlans.list</code></li>
<li><code>compute.orgRollouts.cancel</code></li>
<li><code>compute.orgRollouts.delete</code></li>
<li><code>compute.orgRollouts.get</code></li>
<li><code>compute.orgRollouts.list</code></li>
<li><code>compute.orgRollouts.pause</code></li>
<li><code>compute.orgRollouts.resume</code></li>
<li><code>compute. organizations. disableXpnHost</code></li>
<li><code>compute. organizations. disableXpnResource</code></li>
<li><code>compute. organizations. enableXpnHost</code></li>
<li><code>compute. organizations. enableXpnResource</code></li>
<li><code>compute. organizations. listAssociations</code></li>
<li><code>compute. organizations. setFirewallPolicy</code></li>
<li><code>compute. organizations. setSecurityPolicy</code></li>
<li><code>compute. oslogin. updateExternalUser</code></li>
<li><code>compute. packetMirrorings. create</code></li>
<li><code>compute. packetMirrorings. createTagBinding</code></li>
<li><code>compute. packetMirrorings. delete</code></li>
<li><code>compute. packetMirrorings. deleteTagBinding</code></li>
<li><code>compute.packetMirrorings.get</code></li>
<li><code>compute.packetMirrorings.list</code></li>
<li><code>compute. packetMirrorings. listEffectiveTags</code></li>
<li><code>compute. packetMirrorings. listTagBindings</code></li>
<li><code>compute. packetMirrorings. update</code></li>
<li><code>compute.previewFeatures.get</code></li>
<li><code>compute.previewFeatures.list</code></li>
<li><code>compute.previewFeatures.update</code></li>
<li><code>compute.projects.get</code></li>
<li><code>compute. projects. setCloudArmorTier</code></li>
<li><code>compute. projects. setCommonInstanceMetadata</code></li>
<li><code>compute. projects. setDefaultNetworkTier</code></li>
<li><code>compute. projects. setDefaultServiceAccount</code></li>
<li><code>compute. projects. setManagedProtectionTier</code></li>
<li><code>compute. projects. setUsageExportBucket</code></li>
<li><code>compute. publicAdvertisedPrefixes. create</code></li>
<li><code>compute. publicAdvertisedPrefixes. delete</code></li>
<li><code>compute. publicAdvertisedPrefixes. get</code></li>
<li><code>compute. publicAdvertisedPrefixes. list</code></li>
<li><code>compute. publicAdvertisedPrefixes. update</code></li>
<li><code>compute. publicAdvertisedPrefixes. updatePolicy</code></li>
<li><code>compute. publicDelegatedPrefixes. announce</code></li>
<li><code>compute. publicDelegatedPrefixes. create</code></li>
<li><code>compute. publicDelegatedPrefixes. createTagBinding</code></li>
<li><code>compute. publicDelegatedPrefixes. delete</code></li>
<li><code>compute. publicDelegatedPrefixes. deleteTagBinding</code></li>
<li><code>compute. publicDelegatedPrefixes. get</code></li>
<li><code>compute. publicDelegatedPrefixes. list</code></li>
<li><code>compute. publicDelegatedPrefixes. listEffectiveTags</code></li>
<li><code>compute. publicDelegatedPrefixes. listTagBindings</code></li>
<li><code>compute. publicDelegatedPrefixes. update</code></li>
<li><code>compute. publicDelegatedPrefixes. updatePolicy</code></li>
<li><code>compute. publicDelegatedPrefixes. use</code></li>
<li><code>compute. publicDelegatedPrefixes. withdraw</code></li>
<li><code>compute. recoverableSnapshots. delete</code></li>
<li><code>compute. recoverableSnapshots. get</code></li>
<li><code>compute. recoverableSnapshots. getIamPolicy</code></li>
<li><code>compute. recoverableSnapshots. list</code></li>
<li><code>compute. recoverableSnapshots. recover</code></li>
<li><code>compute. recoverableSnapshots. setIamPolicy</code></li>
<li><code>compute. regionBackendBuckets. create</code></li>
<li><code>compute. regionBackendBuckets. createTagBinding</code></li>
<li><code>compute. regionBackendBuckets. delete</code></li>
<li><code>compute. regionBackendBuckets. deleteTagBinding</code></li>
<li><code>compute. regionBackendBuckets. get</code></li>
<li><code>compute. regionBackendBuckets. getIamPolicy</code></li>
<li><code>compute. regionBackendBuckets. list</code></li>
<li><code>compute. regionBackendBuckets. listEffectiveTags</code></li>
<li><code>compute. regionBackendBuckets. listTagBindings</code></li>
<li><code>compute. regionBackendBuckets. setIamPolicy</code></li>
<li><code>compute. regionBackendBuckets. update</code></li>
<li><code>compute. regionBackendBuckets. use</code></li>
<li><code>compute. regionBackendServices. create</code></li>
<li><code>compute. regionBackendServices. createTagBinding</code></li>
<li><code>compute. regionBackendServices. delete</code></li>
<li><code>compute. regionBackendServices. deleteTagBinding</code></li>
<li><code>compute. regionBackendServices. get</code></li>
<li><code>compute. regionBackendServices. getIamPolicy</code></li>
<li><code>compute. regionBackendServices. list</code></li>
<li><code>compute. regionBackendServices. listEffectiveTags</code></li>
<li><code>compute. regionBackendServices. listTagBindings</code></li>
<li><code>compute. regionBackendServices. setIamPolicy</code></li>
<li><code>compute. regionBackendServices. setSecurityPolicy</code></li>
<li><code>compute. regionBackendServices. update</code></li>
<li><code>compute. regionBackendServices. use</code></li>
<li><code>compute. regionCompositeHealthChecks. create</code></li>
<li><code>compute. regionCompositeHealthChecks. delete</code></li>
<li><code>compute. regionCompositeHealthChecks. get</code></li>
<li><code>compute. regionCompositeHealthChecks. list</code></li>
<li><code>compute. regionCompositeHealthChecks. update</code></li>
<li><code>compute. regionFirewallPolicies. cloneRules</code></li>
<li><code>compute. regionFirewallPolicies. create</code></li>
<li><code>compute. regionFirewallPolicies. createTagBinding</code></li>
<li><code>compute. regionFirewallPolicies. delete</code></li>
<li><code>compute. regionFirewallPolicies. deleteTagBinding</code></li>
<li><code>compute. regionFirewallPolicies. get</code></li>
<li><code>compute. regionFirewallPolicies. getIamPolicy</code></li>
<li><code>compute. regionFirewallPolicies. list</code></li>
<li><code>compute. regionFirewallPolicies. listEffectiveTags</code></li>
<li><code>compute. regionFirewallPolicies. listTagBindings</code></li>
<li><code>compute. regionFirewallPolicies. setIamPolicy</code></li>
<li><code>compute. regionFirewallPolicies. update</code></li>
<li><code>compute. regionFirewallPolicies. use</code></li>
<li><code>compute. regionHealthAggregationPolicies. create</code></li>
<li><code>compute. regionHealthAggregationPolicies. delete</code></li>
<li><code>compute. regionHealthAggregationPolicies. get</code></li>
<li><code>compute. regionHealthAggregationPolicies. list</code></li>
<li><code>compute. regionHealthAggregationPolicies. update</code></li>
<li><code>compute. regionHealthCheckServices. create</code></li>
<li><code>compute. regionHealthCheckServices. delete</code></li>
<li><code>compute. regionHealthCheckServices. get</code></li>
<li><code>compute. regionHealthCheckServices. list</code></li>
<li><code>compute. regionHealthCheckServices. update</code></li>
<li><code>compute. regionHealthCheckServices. use</code></li>
<li><code>compute. regionHealthChecks. create</code></li>
<li><code>compute. regionHealthChecks. createTagBinding</code></li>
<li><code>compute. regionHealthChecks. delete</code></li>
<li><code>compute. regionHealthChecks. deleteTagBinding</code></li>
<li><code>compute.regionHealthChecks.get</code></li>
<li><code>compute. regionHealthChecks. list</code></li>
<li><code>compute. regionHealthChecks. listEffectiveTags</code></li>
<li><code>compute. regionHealthChecks. listTagBindings</code></li>
<li><code>compute. regionHealthChecks. update</code></li>
<li><code>compute.regionHealthChecks.use</code></li>
<li><code>compute. regionHealthChecks. useReadOnly</code></li>
<li><code>compute. regionHealthSources. create</code></li>
<li><code>compute. regionHealthSources. delete</code></li>
<li><code>compute. regionHealthSources. get</code></li>
<li><code>compute. regionHealthSources. list</code></li>
<li><code>compute. regionHealthSources. update</code></li>
<li><code>compute. regionNetworkEndpointGroups. attachNetworkEndpoints</code></li>
<li><code>compute. regionNetworkEndpointGroups. create</code></li>
<li><code>compute. regionNetworkEndpointGroups. createTagBinding</code></li>
<li><code>compute. regionNetworkEndpointGroups. delete</code></li>
<li><code>compute. regionNetworkEndpointGroups. deleteTagBinding</code></li>
<li><code>compute. regionNetworkEndpointGroups. detachNetworkEndpoints</code></li>
<li><code>compute. regionNetworkEndpointGroups. get</code></li>
<li><code>compute. regionNetworkEndpointGroups. list</code></li>
<li><code>compute. regionNetworkEndpointGroups. listEffectiveTags</code></li>
<li><code>compute. regionNetworkEndpointGroups. listTagBindings</code></li>
<li><code>compute. regionNetworkEndpointGroups. use</code></li>
<li><code>compute. regionNetworkPolicies. create</code></li>
<li><code>compute. regionNetworkPolicies. delete</code></li>
<li><code>compute. regionNetworkPolicies. get</code></li>
<li><code>compute. regionNetworkPolicies. list</code></li>
<li><code>compute. regionNetworkPolicies. update</code></li>
<li><code>compute. regionNetworkPolicies. use</code></li>
<li><code>compute. regionNotificationEndpoints. create</code></li>
<li><code>compute. regionNotificationEndpoints. delete</code></li>
<li><code>compute. regionNotificationEndpoints. get</code></li>
<li><code>compute. regionNotificationEndpoints. list</code></li>
<li><code>compute. regionNotificationEndpoints. update</code></li>
<li><code>compute. regionNotificationEndpoints. use</code></li>
<li><code>compute. regionOperations. delete</code></li>
<li><code>compute.regionOperations.get</code></li>
<li><code>compute. regionOperations. getIamPolicy</code></li>
<li><code>compute.regionOperations.list</code></li>
<li><code>compute. regionOperations. setIamPolicy</code></li>
<li><code>compute. regionSecurityPolicies. create</code></li>
<li><code>compute. regionSecurityPolicies. createTagBinding</code></li>
<li><code>compute. regionSecurityPolicies. delete</code></li>
<li><code>compute. regionSecurityPolicies. deleteTagBinding</code></li>
<li><code>compute. regionSecurityPolicies. get</code></li>
<li><code>compute. regionSecurityPolicies. list</code></li>
<li><code>compute. regionSecurityPolicies. listEffectiveTags</code></li>
<li><code>compute. regionSecurityPolicies. listTagBindings</code></li>
<li><code>compute. regionSecurityPolicies. update</code></li>
<li><code>compute. regionSecurityPolicies. use</code></li>
<li><code>compute. regionSslCertificates. create</code></li>
<li><code>compute. regionSslCertificates. createTagBinding</code></li>
<li><code>compute. regionSslCertificates. delete</code></li>
<li><code>compute. regionSslCertificates. deleteTagBinding</code></li>
<li><code>compute. regionSslCertificates. get</code></li>
<li><code>compute. regionSslCertificates. list</code></li>
<li><code>compute. regionSslCertificates. listEffectiveTags</code></li>
<li><code>compute. regionSslCertificates. listTagBindings</code></li>
<li><code>compute. regionSslPolicies. create</code></li>
<li><code>compute. regionSslPolicies. createTagBinding</code></li>
<li><code>compute. regionSslPolicies. delete</code></li>
<li><code>compute. regionSslPolicies. deleteTagBinding</code></li>
<li><code>compute.regionSslPolicies.get</code></li>
<li><code>compute. regionSslPolicies. getIamPolicy</code></li>
<li><code>compute.regionSslPolicies.list</code></li>
<li><code>compute. regionSslPolicies. listAvailableFeatures</code></li>
<li><code>compute. regionSslPolicies. listEffectiveTags</code></li>
<li><code>compute. regionSslPolicies. listTagBindings</code></li>
<li><code>compute. regionSslPolicies. setIamPolicy</code></li>
<li><code>compute. regionSslPolicies. update</code></li>
<li><code>compute.regionSslPolicies.use</code></li>
<li><code>compute. regionTargetHttpProxies. create</code></li>
<li><code>compute. regionTargetHttpProxies. createTagBinding</code></li>
<li><code>compute. regionTargetHttpProxies. delete</code></li>
<li><code>compute. regionTargetHttpProxies. deleteTagBinding</code></li>
<li><code>compute. regionTargetHttpProxies. get</code></li>
<li><code>compute. regionTargetHttpProxies. list</code></li>
<li><code>compute. regionTargetHttpProxies. listEffectiveTags</code></li>
<li><code>compute. regionTargetHttpProxies. listTagBindings</code></li>
<li><code>compute. regionTargetHttpProxies. setUrlMap</code></li>
<li><code>compute. regionTargetHttpProxies. use</code></li>
<li><code>compute. regionTargetHttpsProxies. create</code></li>
<li><code>compute. regionTargetHttpsProxies. createTagBinding</code></li>
<li><code>compute. regionTargetHttpsProxies. delete</code></li>
<li><code>compute. regionTargetHttpsProxies. deleteTagBinding</code></li>
<li><code>compute. regionTargetHttpsProxies. get</code></li>
<li><code>compute. regionTargetHttpsProxies. list</code></li>
<li><code>compute. regionTargetHttpsProxies. listEffectiveTags</code></li>
<li><code>compute. regionTargetHttpsProxies. listTagBindings</code></li>
<li><code>compute. regionTargetHttpsProxies. setSslCertificates</code></li>
<li><code>compute. regionTargetHttpsProxies. setUrlMap</code></li>
<li><code>compute. regionTargetHttpsProxies. update</code></li>
<li><code>compute. regionTargetHttpsProxies. use</code></li>
<li><code>compute. regionTargetTcpProxies. attach</code></li>
<li><code>compute. regionTargetTcpProxies. create</code></li>
<li><code>compute. regionTargetTcpProxies. createTagBinding</code></li>
<li><code>compute. regionTargetTcpProxies. delete</code></li>
<li><code>compute. regionTargetTcpProxies. deleteTagBinding</code></li>
<li><code>compute. regionTargetTcpProxies. get</code></li>
<li><code>compute. regionTargetTcpProxies. list</code></li>
<li><code>compute. regionTargetTcpProxies. listEffectiveTags</code></li>
<li><code>compute. regionTargetTcpProxies. listTagBindings</code></li>
<li><code>compute. regionTargetTcpProxies. use</code></li>
<li><code>compute.regionUrlMaps.create</code></li>
<li><code>compute. regionUrlMaps. createTagBinding</code></li>
<li><code>compute.regionUrlMaps.delete</code></li>
<li><code>compute. regionUrlMaps. deleteTagBinding</code></li>
<li><code>compute.regionUrlMaps.get</code></li>
<li><code>compute. regionUrlMaps. invalidateCache</code></li>
<li><code>compute.regionUrlMaps.list</code></li>
<li><code>compute. regionUrlMaps. listEffectiveTags</code></li>
<li><code>compute. regionUrlMaps. listTagBindings</code></li>
<li><code>compute.regionUrlMaps.update</code></li>
<li><code>compute.regionUrlMaps.use</code></li>
<li><code>compute.regionUrlMaps.validate</code></li>
<li><code>compute.regions.get</code></li>
<li><code>compute.regions.list</code></li>
<li><code>compute.reliabilityRisks.get</code></li>
<li><code>compute.reliabilityRisks.list</code></li>
<li><code>compute.reservationBlocks.get</code></li>
<li><code>compute.reservationBlocks.list</code></li>
<li><code>compute. reservationBlocks. performMaintenance</code></li>
<li><code>compute. reservationConsumedInstances. list</code></li>
<li><code>compute.reservationSlots.get</code></li>
<li><code>compute.reservationSlots.list</code></li>
<li><code>compute. reservationSlots. update</code></li>
<li><code>compute. reservationSubBlocks. get</code></li>
<li><code>compute. reservationSubBlocks. list</code></li>
<li><code>compute. reservationSubBlocks. performMaintenance</code></li>
<li><code>compute. reservationSubBlocks. reportFaulty</code></li>
<li><code>compute.reservations.create</code></li>
<li><code>compute. reservations. createTagBinding</code></li>
<li><code>compute.reservations.delete</code></li>
<li><code>compute. reservations. deleteTagBinding</code></li>
<li><code>compute.reservations.get</code></li>
<li><code>compute.reservations.list</code></li>
<li><code>compute. reservations. listEffectiveTags</code></li>
<li><code>compute. reservations. listTagBindings</code></li>
<li><code>compute. reservations. performMaintenance</code></li>
<li><code>compute.reservations.resize</code></li>
<li><code>compute.reservations.update</code></li>
<li><code>compute. resourcePolicies. create</code></li>
<li><code>compute. resourcePolicies. delete</code></li>
<li><code>compute.resourcePolicies.get</code></li>
<li><code>compute. resourcePolicies. getIamPolicy</code></li>
<li><code>compute.resourcePolicies.list</code></li>
<li><code>compute. resourcePolicies. setIamPolicy</code></li>
<li><code>compute. resourcePolicies. update</code></li>
<li><code>compute.resourcePolicies.use</code></li>
<li><code>compute. resourcePolicies. useReadOnly</code></li>
<li><code>compute.rolloutPlans.create</code></li>
<li><code>compute.rolloutPlans.delete</code></li>
<li><code>compute.rolloutPlans.get</code></li>
<li><code>compute.rolloutPlans.list</code></li>
<li><code>compute.rollouts.cancel</code></li>
<li><code>compute.rollouts.delete</code></li>
<li><code>compute.rollouts.get</code></li>
<li><code>compute.rollouts.list</code></li>
<li><code>compute.routers.create</code></li>
<li><code>compute. routers. createTagBinding</code></li>
<li><code>compute.routers.delete</code></li>
<li><code>compute. routers. deleteRoutePolicy</code></li>
<li><code>compute. routers. deleteTagBinding</code></li>
<li><code>compute.routers.get</code></li>
<li><code>compute.routers.getRoutePolicy</code></li>
<li><code>compute.routers.list</code></li>
<li><code>compute.routers.listBgpRoutes</code></li>
<li><code>compute. routers. listEffectiveTags</code></li>
<li><code>compute. routers. listRoutePolicies</code></li>
<li><code>compute. routers. listTagBindings</code></li>
<li><code>compute.routers.update</code></li>
<li><code>compute. routers. updateRoutePolicy</code></li>
<li><code>compute.routers.use</code></li>
<li><code>compute.routes.create</code></li>
<li><code>compute. routes. createTagBinding</code></li>
<li><code>compute.routes.delete</code></li>
<li><code>compute. routes. deleteTagBinding</code></li>
<li><code>compute.routes.get</code></li>
<li><code>compute.routes.list</code></li>
<li><code>compute. routes. listEffectiveTags</code></li>
<li><code>compute.routes.listTagBindings</code></li>
<li><code>compute. securityPolicies. addAssociation</code></li>
<li><code>compute. securityPolicies. copyRules</code></li>
<li><code>compute. securityPolicies. create</code></li>
<li><code>compute. securityPolicies. createTagBinding</code></li>
<li><code>compute. securityPolicies. delete</code></li>
<li><code>compute. securityPolicies. deleteTagBinding</code></li>
<li><code>compute.securityPolicies.get</code></li>
<li><code>compute.securityPolicies.list</code></li>
<li><code>compute. securityPolicies. listEffectiveTags</code></li>
<li><code>compute. securityPolicies. listTagBindings</code></li>
<li><code>compute.securityPolicies.move</code></li>
<li><code>compute. securityPolicies. removeAssociation</code></li>
<li><code>compute. securityPolicies. setLabels</code></li>
<li><code>compute. securityPolicies. update</code></li>
<li><code>compute.securityPolicies.use</code></li>
<li><code>compute. serviceAttachments. create</code></li>
<li><code>compute. serviceAttachments. createTagBinding</code></li>
<li><code>compute. serviceAttachments. delete</code></li>
<li><code>compute. serviceAttachments. deleteTagBinding</code></li>
<li><code>compute.serviceAttachments.get</code></li>
<li><code>compute. serviceAttachments. getIamPolicy</code></li>
<li><code>compute. serviceAttachments. list</code></li>
<li><code>compute. serviceAttachments. listEffectiveTags</code></li>
<li><code>compute. serviceAttachments. listTagBindings</code></li>
<li><code>compute. serviceAttachments. setIamPolicy</code></li>
<li><code>compute. serviceAttachments. update</code></li>
<li><code>compute.serviceAttachments.use</code></li>
<li><code>compute.snapshotGroups.create</code></li>
<li><code>compute.snapshotGroups.delete</code></li>
<li><code>compute.snapshotGroups.get</code></li>
<li><code>compute. snapshotGroups. getIamPolicy</code></li>
<li><code>compute.snapshotGroups.list</code></li>
<li><code>compute. snapshotGroups. setIamPolicy</code></li>
<li><code>compute. snapshotGroups. useReadOnly</code></li>
<li><code>compute. snapshotRecycleBinPolicy. get</code></li>
<li><code>compute. snapshotRecycleBinPolicy. update</code></li>
<li><code>compute.snapshotSettings.get</code></li>
<li><code>compute. snapshotSettings. update</code></li>
<li><code>compute.snapshots.create</code></li>
<li><code>compute. snapshots. createTagBinding</code></li>
<li><code>compute.snapshots.delete</code></li>
<li><code>compute. snapshots. deleteTagBinding</code></li>
<li><code>compute.snapshots.get</code></li>
<li><code>compute. snapshots. getEffectiveRecycleBinRule</code></li>
<li><code>compute.snapshots.getIamPolicy</code></li>
<li><code>compute.snapshots.list</code></li>
<li><code>compute. snapshots. listEffectiveTags</code></li>
<li><code>compute. snapshots. listTagBindings</code></li>
<li><code>compute.snapshots.setIamPolicy</code></li>
<li><code>compute.snapshots.setLabels</code></li>
<li><code>compute.snapshots.updateKmsKey</code></li>
<li><code>compute.snapshots.useReadOnly</code></li>
<li><code>compute.spotAssistants.get</code></li>
<li><code>compute.sslCertificates.create</code></li>
<li><code>compute. sslCertificates. createTagBinding</code></li>
<li><code>compute.sslCertificates.delete</code></li>
<li><code>compute. sslCertificates. deleteTagBinding</code></li>
<li><code>compute.sslCertificates.get</code></li>
<li><code>compute.sslCertificates.list</code></li>
<li><code>compute. sslCertificates. listEffectiveTags</code></li>
<li><code>compute. sslCertificates. listTagBindings</code></li>
<li><code>compute.sslPolicies.create</code></li>
<li><code>compute. sslPolicies. createTagBinding</code></li>
<li><code>compute.sslPolicies.delete</code></li>
<li><code>compute. sslPolicies. deleteTagBinding</code></li>
<li><code>compute.sslPolicies.get</code></li>
<li><code>compute. sslPolicies. getIamPolicy</code></li>
<li><code>compute.sslPolicies.list</code></li>
<li><code>compute. sslPolicies. listAvailableFeatures</code></li>
<li><code>compute. sslPolicies. listEffectiveTags</code></li>
<li><code>compute. sslPolicies. listTagBindings</code></li>
<li><code>compute. sslPolicies. setIamPolicy</code></li>
<li><code>compute.sslPolicies.update</code></li>
<li><code>compute.sslPolicies.use</code></li>
<li><code>compute.storagePools.create</code></li>
<li><code>compute. storagePools. createTagBinding</code></li>
<li><code>compute.storagePools.delete</code></li>
<li><code>compute. storagePools. deleteTagBinding</code></li>
<li><code>compute.storagePools.get</code></li>
<li><code>compute. storagePools. getIamPolicy</code></li>
<li><code>compute.storagePools.list</code></li>
<li><code>compute. storagePools. listEffectiveTags</code></li>
<li><code>compute. storagePools. listTagBindings</code></li>
<li><code>compute. storagePools. setIamPolicy</code></li>
<li><code>compute.storagePools.update</code></li>
<li><code>compute.storagePools.use</code></li>
<li><code>compute.subnetworks.create</code></li>
<li><code>compute. subnetworks. createTagBinding</code></li>
<li><code>compute.subnetworks.delete</code></li>
<li><code>compute. subnetworks. deleteTagBinding</code></li>
<li><code>compute. subnetworks. expandIpCidrRange</code></li>
<li><code>compute.subnetworks.get</code></li>
<li><code>compute. subnetworks. getIamPolicy</code></li>
<li><code>compute.subnetworks.list</code></li>
<li><code>compute. subnetworks. listEffectiveTags</code></li>
<li><code>compute. subnetworks. listTagBindings</code></li>
<li><code>compute.subnetworks.mirror</code></li>
<li><code>compute. subnetworks. setIamPolicy</code></li>
<li><code>compute. subnetworks. setPrivateIpGoogleAccess</code></li>
<li><code>compute.subnetworks.update</code></li>
<li><code>compute.subnetworks.use</code></li>
<li><code>compute. subnetworks. useExternalIp</code></li>
<li><code>compute. subnetworks. usePeerMigration</code></li>
<li><code>compute. targetGrpcProxies. create</code></li>
<li><code>compute. targetGrpcProxies. createTagBinding</code></li>
<li><code>compute. targetGrpcProxies. delete</code></li>
<li><code>compute. targetGrpcProxies. deleteTagBinding</code></li>
<li><code>compute.targetGrpcProxies.get</code></li>
<li><code>compute.targetGrpcProxies.list</code></li>
<li><code>compute. targetGrpcProxies. listEffectiveTags</code></li>
<li><code>compute. targetGrpcProxies. listTagBindings</code></li>
<li><code>compute. targetGrpcProxies. update</code></li>
<li><code>compute.targetGrpcProxies.use</code></li>
<li><code>compute. targetHttpProxies. create</code></li>
<li><code>compute. targetHttpProxies. createTagBinding</code></li>
<li><code>compute. targetHttpProxies. delete</code></li>
<li><code>compute. targetHttpProxies. deleteTagBinding</code></li>
<li><code>compute.targetHttpProxies.get</code></li>
<li><code>compute.targetHttpProxies.list</code></li>
<li><code>compute. targetHttpProxies. listEffectiveTags</code></li>
<li><code>compute. targetHttpProxies. listTagBindings</code></li>
<li><code>compute. targetHttpProxies. setUrlMap</code></li>
<li><code>compute. targetHttpProxies. update</code></li>
<li><code>compute.targetHttpProxies.use</code></li>
<li><code>compute. targetHttpsProxies. create</code></li>
<li><code>compute. targetHttpsProxies. createTagBinding</code></li>
<li><code>compute. targetHttpsProxies. delete</code></li>
<li><code>compute. targetHttpsProxies. deleteTagBinding</code></li>
<li><code>compute.targetHttpsProxies.get</code></li>
<li><code>compute. targetHttpsProxies. list</code></li>
<li><code>compute. targetHttpsProxies. listEffectiveTags</code></li>
<li><code>compute. targetHttpsProxies. listTagBindings</code></li>
<li><code>compute. targetHttpsProxies. setCertificateMap</code></li>
<li><code>compute. targetHttpsProxies. setQuicOverride</code></li>
<li><code>compute. targetHttpsProxies. setSslCertificates</code></li>
<li><code>compute. targetHttpsProxies. setSslPolicy</code></li>
<li><code>compute. targetHttpsProxies. setUrlMap</code></li>
<li><code>compute. targetHttpsProxies. update</code></li>
<li><code>compute.targetHttpsProxies.use</code></li>
<li><code>compute.targetInstances.create</code></li>
<li><code>compute. targetInstances. createTagBinding</code></li>
<li><code>compute.targetInstances.delete</code></li>
<li><code>compute. targetInstances. deleteTagBinding</code></li>
<li><code>compute.targetInstances.get</code></li>
<li><code>compute.targetInstances.list</code></li>
<li><code>compute. targetInstances. listEffectiveTags</code></li>
<li><code>compute. targetInstances. listTagBindings</code></li>
<li><code>compute. targetInstances. setSecurityPolicy</code></li>
<li><code>compute.targetInstances.use</code></li>
<li><code>compute. targetPools. addHealthCheck</code></li>
<li><code>compute. targetPools. addInstance</code></li>
<li><code>compute.targetPools.create</code></li>
<li><code>compute. targetPools. createTagBinding</code></li>
<li><code>compute.targetPools.delete</code></li>
<li><code>compute. targetPools. deleteTagBinding</code></li>
<li><code>compute.targetPools.get</code></li>
<li><code>compute.targetPools.list</code></li>
<li><code>compute. targetPools. listEffectiveTags</code></li>
<li><code>compute. targetPools. listTagBindings</code></li>
<li><code>compute. targetPools. removeHealthCheck</code></li>
<li><code>compute. targetPools. removeInstance</code></li>
<li><code>compute. targetPools. setSecurityPolicy</code></li>
<li><code>compute.targetPools.update</code></li>
<li><code>compute.targetPools.use</code></li>
<li><code>compute. targetSslProxies. create</code></li>
<li><code>compute. targetSslProxies. createTagBinding</code></li>
<li><code>compute. targetSslProxies. delete</code></li>
<li><code>compute. targetSslProxies. deleteTagBinding</code></li>
<li><code>compute.targetSslProxies.get</code></li>
<li><code>compute.targetSslProxies.list</code></li>
<li><code>compute. targetSslProxies. listEffectiveTags</code></li>
<li><code>compute. targetSslProxies. listTagBindings</code></li>
<li><code>compute. targetSslProxies. setBackendService</code></li>
<li><code>compute. targetSslProxies. setCertificateMap</code></li>
<li><code>compute. targetSslProxies. setProxyHeader</code></li>
<li><code>compute. targetSslProxies. setSslCertificates</code></li>
<li><code>compute. targetSslProxies. setSslPolicy</code></li>
<li><code>compute. targetSslProxies. update</code></li>
<li><code>compute.targetSslProxies.use</code></li>
<li><code>compute. targetTcpProxies. attach</code></li>
<li><code>compute. targetTcpProxies. create</code></li>
<li><code>compute. targetTcpProxies. createTagBinding</code></li>
<li><code>compute. targetTcpProxies. delete</code></li>
<li><code>compute. targetTcpProxies. deleteTagBinding</code></li>
<li><code>compute.targetTcpProxies.get</code></li>
<li><code>compute.targetTcpProxies.list</code></li>
<li><code>compute. targetTcpProxies. listEffectiveTags</code></li>
<li><code>compute. targetTcpProxies. listTagBindings</code></li>
<li><code>compute. targetTcpProxies. update</code></li>
<li><code>compute.targetTcpProxies.use</code></li>
<li><code>compute. targetVpnGateways. create</code></li>
<li><code>compute. targetVpnGateways. createTagBinding</code></li>
<li><code>compute. targetVpnGateways. delete</code></li>
<li><code>compute. targetVpnGateways. deleteTagBinding</code></li>
<li><code>compute.targetVpnGateways.get</code></li>
<li><code>compute.targetVpnGateways.list</code></li>
<li><code>compute. targetVpnGateways. listEffectiveTags</code></li>
<li><code>compute. targetVpnGateways. listTagBindings</code></li>
<li><code>compute. targetVpnGateways. setLabels</code></li>
<li><code>compute.targetVpnGateways.use</code></li>
<li><code>compute.urlMaps.create</code></li>
<li><code>compute. urlMaps. createTagBinding</code></li>
<li><code>compute.urlMaps.delete</code></li>
<li><code>compute. urlMaps. deleteTagBinding</code></li>
<li><code>compute.urlMaps.get</code></li>
<li><code>compute. urlMaps. invalidateCache</code></li>
<li><code>compute.urlMaps.list</code></li>
<li><code>compute. urlMaps. listEffectiveTags</code></li>
<li><code>compute. urlMaps. listTagBindings</code></li>
<li><code>compute.urlMaps.update</code></li>
<li><code>compute.urlMaps.use</code></li>
<li><code>compute.urlMaps.validate</code></li>
<li><code>compute. vmExtensionPolicies. create</code></li>
<li><code>compute. vmExtensionPolicies. delete</code></li>
<li><code>compute. vmExtensionPolicies. get</code></li>
<li><code>compute. vmExtensionPolicies. list</code></li>
<li><code>compute. vmExtensionPolicies. update</code></li>
<li><code>compute.vpnGateways.create</code></li>
<li><code>compute. vpnGateways. createTagBinding</code></li>
<li><code>compute.vpnGateways.delete</code></li>
<li><code>compute. vpnGateways. deleteTagBinding</code></li>
<li><code>compute.vpnGateways.get</code></li>
<li><code>compute.vpnGateways.list</code></li>
<li><code>compute. vpnGateways. listEffectiveTags</code></li>
<li><code>compute. vpnGateways. listTagBindings</code></li>
<li><code>compute.vpnGateways.setLabels</code></li>
<li><code>compute.vpnGateways.use</code></li>
<li><code>compute.vpnTunnels.create</code></li>
<li><code>compute. vpnTunnels. createTagBinding</code></li>
<li><code>compute.vpnTunnels.delete</code></li>
<li><code>compute. vpnTunnels. deleteTagBinding</code></li>
<li><code>compute.vpnTunnels.get</code></li>
<li><code>compute.vpnTunnels.list</code></li>
<li><code>compute. vpnTunnels. listEffectiveTags</code></li>
<li><code>compute. vpnTunnels. listTagBindings</code></li>
<li><code>compute.vpnTunnels.setLabels</code></li>
<li><code>compute.wireGroups.create</code></li>
<li><code>compute.wireGroups.delete</code></li>
<li><code>compute.wireGroups.get</code></li>
<li><code>compute.wireGroups.list</code></li>
<li><code>compute.wireGroups.update</code></li>
<li><code>compute.zoneOperations.delete</code></li>
<li><code>compute.zoneOperations.get</code></li>
<li><code>compute. zoneOperations. getIamPolicy</code></li>
<li><code>compute.zoneOperations.list</code></li>
<li><code>compute. zoneOperations. setIamPolicy</code></li>
<li><code>compute.zones.get</code></li>
<li><code>compute.zones.list</code></li>
</ul>
<p><code>notebooks.*</code></p>
<ul>
<li><code>notebooks.environments.create</code></li>
<li><code>notebooks.environments.delete</code></li>
<li><code>notebooks.environments.get</code></li>
<li><code>notebooks. environments. getIamPolicy</code></li>
<li><code>notebooks.environments.list</code></li>
<li><code>notebooks. environments. setIamPolicy</code></li>
<li><code>notebooks.executions.create</code></li>
<li><code>notebooks.executions.delete</code></li>
<li><code>notebooks.executions.get</code></li>
<li><code>notebooks. executions. getIamPolicy</code></li>
<li><code>notebooks.executions.list</code></li>
<li><code>notebooks. executions. setIamPolicy</code></li>
<li><code>notebooks. instances. checkUpgradability</code></li>
<li><code>notebooks.instances.create</code></li>
<li><code>notebooks. instances. createTagBinding</code></li>
<li><code>notebooks.instances.delete</code></li>
<li><code>notebooks. instances. deleteTagBinding</code></li>
<li><code>notebooks.instances.diagnose</code></li>
<li><code>notebooks.instances.get</code></li>
<li><code>notebooks.instances.getHealth</code></li>
<li><code>notebooks. instances. getIamPolicy</code></li>
<li><code>notebooks.instances.list</code></li>
<li><code>notebooks. instances. listEffectiveTags</code></li>
<li><code>notebooks. instances. listTagBindings</code></li>
<li><code>notebooks.instances.reset</code></li>
<li><code>notebooks. instances. setAccelerator</code></li>
<li><code>notebooks. instances. setIamPolicy</code></li>
<li><code>notebooks.instances.setLabels</code></li>
<li><code>notebooks. instances. setMachineType</code></li>
<li><code>notebooks.instances.start</code></li>
<li><code>notebooks.instances.stop</code></li>
<li><code>notebooks.instances.update</code></li>
<li><code>notebooks. instances. updateConfig</code></li>
<li><code>notebooks. instances. updateShieldInstanceConfig</code></li>
<li><code>notebooks.instances.upgrade</code></li>
<li><code>notebooks.instances.use</code></li>
<li><code>notebooks.locations.get</code></li>
<li><code>notebooks.locations.list</code></li>
<li><code>notebooks.operations.cancel</code></li>
<li><code>notebooks.operations.delete</code></li>
<li><code>notebooks.operations.get</code></li>
<li><code>notebooks.operations.list</code></li>
<li><code>notebooks.runtimes.create</code></li>
<li><code>notebooks.runtimes.delete</code></li>
<li><code>notebooks.runtimes.diagnose</code></li>
<li><code>notebooks.runtimes.get</code></li>
<li><code>notebooks. runtimes. getIamPolicy</code></li>
<li><code>notebooks.runtimes.list</code></li>
<li><code>notebooks.runtimes.reset</code></li>
<li><code>notebooks. runtimes. setIamPolicy</code></li>
<li><code>notebooks.runtimes.start</code></li>
<li><code>notebooks.runtimes.stop</code></li>
<li><code>notebooks.runtimes.switch</code></li>
<li><code>notebooks.runtimes.update</code></li>
<li><code>notebooks.runtimes.upgrade</code></li>
<li><code>notebooks.schedules.create</code></li>
<li><code>notebooks.schedules.delete</code></li>
<li><code>notebooks.schedules.get</code></li>
<li><code>notebooks. schedules. getIamPolicy</code></li>
<li><code>notebooks.schedules.list</code></li>
<li><code>notebooks. schedules. setIamPolicy</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p>
<p><code>serviceusage. consumerpolicy. analyze</code></p>
<p><code>serviceusage. consumerpolicy. get</code></p>
<p><code>serviceusage. effectivepolicy. get</code></p>
<p><code>serviceusage.groups.*</code></p>
<ul>
<li><code>serviceusage.groups.list</code></li>
<li><code>serviceusage. groups. listExpandedMembers</code></li>
<li><code>serviceusage. groups. listMembers</code></li>
</ul>
<p><code>serviceusage.quotas.get</code></p>
<p><code>serviceusage.services.get</code></p>
<p><code>serviceusage.services.list</code></p>
<p><code>serviceusage.values.test</code></p></td>
</tr>
<tr class="odd">
<td>Notebooks Legacy Viewer
<p>( <code>roles/ notebooks.legacyViewer</code> )</p>
<p>Read-only access to Notebooks all resources through compute API.</p></td>
<td><p><code>compute.acceleratorTypes.*</code></p>
<ul>
<li><code>compute.acceleratorTypes.get</code></li>
<li><code>compute.acceleratorTypes.list</code></li>
</ul>
<p><code>compute.addresses.get</code></p>
<p><code>compute.addresses.list</code></p>
<p><code>compute. addresses. listEffectiveTags</code></p>
<p><code>compute. addresses. listTagBindings</code></p>
<p><code>compute.advice.capacity</code></p>
<p><code>compute.advice.capacityHistory</code></p>
<p><code>compute.autoscalers.get</code></p>
<p><code>compute.autoscalers.list</code></p>
<p><code>compute.backendBuckets.get</code></p>
<p><code>compute. backendBuckets. getIamPolicy</code></p>
<p><code>compute.backendBuckets.list</code></p>
<p><code>compute. backendBuckets. listEffectiveTags</code></p>
<p><code>compute. backendBuckets. listTagBindings</code></p>
<p><code>compute.backendServices.get</code></p>
<p><code>compute. backendServices. getIamPolicy</code></p>
<p><code>compute.backendServices.list</code></p>
<p><code>compute. backendServices. listEffectiveTags</code></p>
<p><code>compute. backendServices. listTagBindings</code></p>
<p><code>compute.commitments.get</code></p>
<p><code>compute.commitments.list</code></p>
<p><code>compute. commitments. listEffectiveTags</code></p>
<p><code>compute. commitments. listTagBindings</code></p>
<p><code>compute.crossSiteNetworks.get</code></p>
<p><code>compute.crossSiteNetworks.list</code></p>
<p><code>compute.diskSettings.get</code></p>
<p><code>compute.diskTypes.*</code></p>
<ul>
<li><code>compute.diskTypes.get</code></li>
<li><code>compute.diskTypes.list</code></li>
</ul>
<p><code>compute.disks.get</code></p>
<p><code>compute.disks.getIamPolicy</code></p>
<p><code>compute.disks.list</code></p>
<p><code>compute. disks. listEffectiveTags</code></p>
<p><code>compute.disks.listTagBindings</code></p>
<p><code>compute. externalVpnGateways. get</code></p>
<p><code>compute. externalVpnGateways. list</code></p>
<p><code>compute. externalVpnGateways. listEffectiveTags</code></p>
<p><code>compute. externalVpnGateways. listTagBindings</code></p>
<p><code>compute.firewallPolicies.get</code></p>
<p><code>compute. firewallPolicies. getIamPolicy</code></p>
<p><code>compute.firewallPolicies.list</code></p>
<p><code>compute. firewallPolicies. listEffectiveTags</code></p>
<p><code>compute. firewallPolicies. listTagBindings</code></p>
<p><code>compute.firewalls.get</code></p>
<p><code>compute.firewalls.list</code></p>
<p><code>compute. firewalls. listEffectiveTags</code></p>
<p><code>compute. firewalls. listTagBindings</code></p>
<p><code>compute.forwardingRules.get</code></p>
<p><code>compute.forwardingRules.list</code></p>
<p><code>compute. forwardingRules. listEffectiveTags</code></p>
<p><code>compute. forwardingRules. listTagBindings</code></p>
<p><code>compute.futureReservations.get</code></p>
<p><code>compute. futureReservations. getIamPolicy</code></p>
<p><code>compute. futureReservations. list</code></p>
<p><code>compute. futureReservations. listEffectiveTags</code></p>
<p><code>compute. futureReservations. listTagBindings</code></p>
<p><code>compute.globalAddresses.get</code></p>
<p><code>compute.globalAddresses.list</code></p>
<p><code>compute. globalAddresses. listEffectiveTags</code></p>
<p><code>compute. globalAddresses. listTagBindings</code></p>
<p><code>compute. globalForwardingRules. get</code></p>
<p><code>compute. globalForwardingRules. list</code></p>
<p><code>compute. globalForwardingRules. listEffectiveTags</code></p>
<p><code>compute. globalForwardingRules. listTagBindings</code></p>
<p><code>compute. globalFrontendSettings. get</code></p>
<p><code>compute. globalNetworkEndpointGroups. get</code></p>
<p><code>compute. globalNetworkEndpointGroups. list</code></p>
<p><code>compute. globalNetworkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. globalNetworkEndpointGroups. listTagBindings</code></p>
<p><code>compute.globalOperations.get</code></p>
<p><code>compute. globalOperations. getIamPolicy</code></p>
<p><code>compute.globalOperations.list</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. get</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. list</code></p>
<p><code>compute.healthChecks.get</code></p>
<p><code>compute.healthChecks.list</code></p>
<p><code>compute. healthChecks. listEffectiveTags</code></p>
<p><code>compute. healthChecks. listTagBindings</code></p>
<p><code>compute.hosts.*</code></p>
<ul>
<li><code>compute.hosts.get</code></li>
<li><code>compute.hosts.getVersion</code></li>
<li><code>compute.hosts.list</code></li>
</ul>
<p><code>compute.httpHealthChecks.get</code></p>
<p><code>compute.httpHealthChecks.list</code></p>
<p><code>compute. httpHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpHealthChecks. listTagBindings</code></p>
<p><code>compute.httpsHealthChecks.get</code></p>
<p><code>compute.httpsHealthChecks.list</code></p>
<p><code>compute. httpsHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpsHealthChecks. listTagBindings</code></p>
<p><code>compute.images.get</code></p>
<p><code>compute.images.getFromFamily</code></p>
<p><code>compute.images.getIamPolicy</code></p>
<p><code>compute.images.list</code></p>
<p><code>compute. images. listEffectiveTags</code></p>
<p><code>compute.images.listTagBindings</code></p>
<p><code>compute. instanceGroupManagers. get</code></p>
<p><code>compute. instanceGroupManagers. list</code></p>
<p><code>compute. instanceGroupManagers. listEffectiveTags</code></p>
<p><code>compute. instanceGroupManagers. listTagBindings</code></p>
<p><code>compute.instanceGroups.get</code></p>
<p><code>compute.instanceGroups.list</code></p>
<p><code>compute. instanceGroups. listEffectiveTags</code></p>
<p><code>compute. instanceGroups. listTagBindings</code></p>
<p><code>compute.instanceSettings.get</code></p>
<p><code>compute.instanceTemplates.get</code></p>
<p><code>compute. instanceTemplates. getIamPolicy</code></p>
<p><code>compute.instanceTemplates.list</code></p>
<p><code>compute.instances.get</code></p>
<p><code>compute. instances. getEffectiveFirewalls</code></p>
<p><code>compute. instances. getGuestAttributes</code></p>
<p><code>compute.instances.getIamPolicy</code></p>
<p><code>compute. instances. getScreenshot</code></p>
<p><code>compute. instances. getSerialPortOutput</code></p>
<p><code>compute. instances. getShieldedInstanceIdentity</code></p>
<p><code>compute. instances. getShieldedVmIdentity</code></p>
<p><code>compute. instances. getVmExtensionState</code></p>
<p><code>compute.instances.list</code></p>
<p><code>compute. instances. listEffectiveTags</code></p>
<p><code>compute. instances. listReferrers</code></p>
<p><code>compute. instances. listTagBindings</code></p>
<p><code>compute. instances. listVmExtensionStates</code></p>
<p><code>compute.instances.troubleshoot</code></p>
<p><code>compute. instantSnapshotGroups. get</code></p>
<p><code>compute. instantSnapshotGroups. getIamPolicy</code></p>
<p><code>compute. instantSnapshotGroups. list</code></p>
<p><code>compute.instantSnapshots.get</code></p>
<p><code>compute. instantSnapshots. getIamPolicy</code></p>
<p><code>compute.instantSnapshots.list</code></p>
<p><code>compute. instantSnapshots. listEffectiveTags</code></p>
<p><code>compute. instantSnapshots. listTagBindings</code></p>
<p><code>compute. interconnectAttachmentGroups. get</code></p>
<p><code>compute. interconnectAttachmentGroups. list</code></p>
<p><code>compute. interconnectAttachments. get</code></p>
<p><code>compute. interconnectAttachments. list</code></p>
<p><code>compute. interconnectAttachments. listEffectiveTags</code></p>
<p><code>compute. interconnectAttachments. listTagBindings</code></p>
<p><code>compute.interconnectGroups.get</code></p>
<p><code>compute. interconnectGroups. list</code></p>
<p><code>compute. interconnectLocations.*</code></p>
<ul>
<li><code>compute. interconnectLocations. get</code></li>
<li><code>compute. interconnectLocations. list</code></li>
</ul>
<p><code>compute. interconnectRemoteLocations.*</code></p>
<ul>
<li><code>compute. interconnectRemoteLocations. get</code></li>
<li><code>compute. interconnectRemoteLocations. list</code></li>
</ul>
<p><code>compute.interconnects.get</code></p>
<p><code>compute.interconnects.list</code></p>
<p><code>compute. interconnects. listEffectiveTags</code></p>
<p><code>compute. interconnects. listTagBindings</code></p>
<p><code>compute.licenseCodes.get</code></p>
<p><code>compute. licenseCodes. getIamPolicy</code></p>
<p><code>compute.licenseCodes.list</code></p>
<p><code>compute.licenses.get</code></p>
<p><code>compute.licenses.getIamPolicy</code></p>
<p><code>compute.licenses.list</code></p>
<p><code>compute. licenses. listEffectiveTags</code></p>
<p><code>compute. licenses. listTagBindings</code></p>
<p><code>compute.machineImages.get</code></p>
<p><code>compute. machineImages. getIamPolicy</code></p>
<p><code>compute.machineImages.list</code></p>
<p><code>compute. machineImages. listEffectiveTags</code></p>
<p><code>compute. machineImages. listTagBindings</code></p>
<p><code>compute.machineTypes.*</code></p>
<ul>
<li><code>compute.machineTypes.get</code></li>
<li><code>compute.machineTypes.list</code></li>
</ul>
<p><code>compute.managedRulesets.*</code></p>
<ul>
<li><code>compute.managedRulesets.get</code></li>
<li><code>compute.managedRulesets.list</code></li>
</ul>
<p><code>compute.multiMig.get</code></p>
<p><code>compute.multiMig.list</code></p>
<p><code>compute.multiMigMembers.*</code></p>
<ul>
<li><code>compute.multiMigMembers.get</code></li>
<li><code>compute.multiMigMembers.list</code></li>
</ul>
<p><code>compute.networkAttachments.get</code></p>
<p><code>compute. networkAttachments. getIamPolicy</code></p>
<p><code>compute. networkAttachments. list</code></p>
<p><code>compute. networkAttachments. listEffectiveTags</code></p>
<p><code>compute. networkAttachments. listTagBindings</code></p>
<p><code>compute. networkEdgeSecurityServices. get</code></p>
<p><code>compute. networkEdgeSecurityServices. list</code></p>
<p><code>compute. networkEdgeSecurityServices. listEffectiveTags</code></p>
<p><code>compute. networkEdgeSecurityServices. listTagBindings</code></p>
<p><code>compute. networkEndpointGroups. get</code></p>
<p><code>compute. networkEndpointGroups. list</code></p>
<p><code>compute. networkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. networkEndpointGroups. listTagBindings</code></p>
<p><code>compute.networkProfiles.*</code></p>
<ul>
<li><code>compute.networkProfiles.get</code></li>
<li><code>compute.networkProfiles.list</code></li>
</ul>
<p><code>compute.networks.get</code></p>
<p><code>compute. networks. getEffectiveFirewalls</code></p>
<p><code>compute. networks. getRegionEffectiveFirewalls</code></p>
<p><code>compute.networks.list</code></p>
<p><code>compute. networks. listEffectiveTags</code></p>
<p><code>compute. networks. listPeeringRoutes</code></p>
<p><code>compute. networks. listTagBindings</code></p>
<p><code>compute.nodeGroups.get</code></p>
<p><code>compute. nodeGroups. getIamPolicy</code></p>
<p><code>compute.nodeGroups.list</code></p>
<p><code>compute.nodeTemplates.get</code></p>
<p><code>compute. nodeTemplates. getIamPolicy</code></p>
<p><code>compute.nodeTemplates.list</code></p>
<p><code>compute.nodeTypes.*</code></p>
<ul>
<li><code>compute.nodeTypes.get</code></li>
<li><code>compute.nodeTypes.list</code></li>
</ul>
<p><code>compute.orgRolloutPlans.get</code></p>
<p><code>compute.orgRolloutPlans.list</code></p>
<p><code>compute.orgRollouts.get</code></p>
<p><code>compute.orgRollouts.list</code></p>
<p><code>compute. organizations. listAssociations</code></p>
<p><code>compute.packetMirrorings.get</code></p>
<p><code>compute.packetMirrorings.list</code></p>
<p><code>compute. packetMirrorings. listEffectiveTags</code></p>
<p><code>compute. packetMirrorings. listTagBindings</code></p>
<p><code>compute.previewFeatures.get</code></p>
<p><code>compute.previewFeatures.list</code></p>
<p><code>compute.projects.get</code></p>
<p><code>compute. publicAdvertisedPrefixes. get</code></p>
<p><code>compute. publicAdvertisedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. get</code></p>
<p><code>compute. publicDelegatedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. listEffectiveTags</code></p>
<p><code>compute. publicDelegatedPrefixes. listTagBindings</code></p>
<p><code>compute. recoverableSnapshots. get</code></p>
<p><code>compute. recoverableSnapshots. getIamPolicy</code></p>
<p><code>compute. recoverableSnapshots. list</code></p>
<p><code>compute. regionBackendBuckets. get</code></p>
<p><code>compute. regionBackendBuckets. getIamPolicy</code></p>
<p><code>compute. regionBackendBuckets. list</code></p>
<p><code>compute. regionBackendBuckets. listEffectiveTags</code></p>
<p><code>compute. regionBackendBuckets. listTagBindings</code></p>
<p><code>compute. regionBackendServices. get</code></p>
<p><code>compute. regionBackendServices. getIamPolicy</code></p>
<p><code>compute. regionBackendServices. list</code></p>
<p><code>compute. regionBackendServices. listEffectiveTags</code></p>
<p><code>compute. regionBackendServices. listTagBindings</code></p>
<p><code>compute. regionCompositeHealthChecks. get</code></p>
<p><code>compute. regionCompositeHealthChecks. list</code></p>
<p><code>compute. regionFirewallPolicies. get</code></p>
<p><code>compute. regionFirewallPolicies. getIamPolicy</code></p>
<p><code>compute. regionFirewallPolicies. list</code></p>
<p><code>compute. regionFirewallPolicies. listEffectiveTags</code></p>
<p><code>compute. regionFirewallPolicies. listTagBindings</code></p>
<p><code>compute. regionHealthAggregationPolicies. get</code></p>
<p><code>compute. regionHealthAggregationPolicies. list</code></p>
<p><code>compute. regionHealthCheckServices. get</code></p>
<p><code>compute. regionHealthCheckServices. list</code></p>
<p><code>compute.regionHealthChecks.get</code></p>
<p><code>compute. regionHealthChecks. list</code></p>
<p><code>compute. regionHealthChecks. listEffectiveTags</code></p>
<p><code>compute. regionHealthChecks. listTagBindings</code></p>
<p><code>compute. regionHealthSources. get</code></p>
<p><code>compute. regionHealthSources. list</code></p>
<p><code>compute. regionNetworkEndpointGroups. get</code></p>
<p><code>compute. regionNetworkEndpointGroups. list</code></p>
<p><code>compute. regionNetworkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. regionNetworkEndpointGroups. listTagBindings</code></p>
<p><code>compute. regionNetworkPolicies. get</code></p>
<p><code>compute. regionNetworkPolicies. list</code></p>
<p><code>compute. regionNotificationEndpoints. get</code></p>
<p><code>compute. regionNotificationEndpoints. list</code></p>
<p><code>compute.regionOperations.get</code></p>
<p><code>compute. regionOperations. getIamPolicy</code></p>
<p><code>compute.regionOperations.list</code></p>
<p><code>compute. regionSecurityPolicies. get</code></p>
<p><code>compute. regionSecurityPolicies. list</code></p>
<p><code>compute. regionSecurityPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSecurityPolicies. listTagBindings</code></p>
<p><code>compute. regionSslCertificates. get</code></p>
<p><code>compute. regionSslCertificates. list</code></p>
<p><code>compute. regionSslCertificates. listEffectiveTags</code></p>
<p><code>compute. regionSslCertificates. listTagBindings</code></p>
<p><code>compute.regionSslPolicies.get</code></p>
<p><code>compute. regionSslPolicies. getIamPolicy</code></p>
<p><code>compute.regionSslPolicies.list</code></p>
<p><code>compute. regionSslPolicies. listAvailableFeatures</code></p>
<p><code>compute. regionSslPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSslPolicies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpProxies. get</code></p>
<p><code>compute. regionTargetHttpProxies. list</code></p>
<p><code>compute. regionTargetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpProxies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpsProxies. get</code></p>
<p><code>compute. regionTargetHttpsProxies. list</code></p>
<p><code>compute. regionTargetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpsProxies. listTagBindings</code></p>
<p><code>compute. regionTargetTcpProxies. get</code></p>
<p><code>compute. regionTargetTcpProxies. list</code></p>
<p><code>compute. regionTargetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetTcpProxies. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.get</code></p>
<p><code>compute.regionUrlMaps.list</code></p>
<p><code>compute. regionUrlMaps. listEffectiveTags</code></p>
<p><code>compute. regionUrlMaps. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.validate</code></p>
<p><code>compute.regions.*</code></p>
<ul>
<li><code>compute.regions.get</code></li>
<li><code>compute.regions.list</code></li>
</ul>
<p><code>compute.reliabilityRisks.*</code></p>
<ul>
<li><code>compute.reliabilityRisks.get</code></li>
<li><code>compute.reliabilityRisks.list</code></li>
</ul>
<p><code>compute.reservationBlocks.get</code></p>
<p><code>compute.reservationBlocks.list</code></p>
<p><code>compute. reservationConsumedInstances. list</code></p>
<p><code>compute.reservationSlots.get</code></p>
<p><code>compute.reservationSlots.list</code></p>
<p><code>compute. reservationSubBlocks. get</code></p>
<p><code>compute. reservationSubBlocks. list</code></p>
<p><code>compute.reservations.get</code></p>
<p><code>compute.reservations.list</code></p>
<p><code>compute. reservations. listEffectiveTags</code></p>
<p><code>compute. reservations. listTagBindings</code></p>
<p><code>compute.resourcePolicies.get</code></p>
<p><code>compute. resourcePolicies. getIamPolicy</code></p>
<p><code>compute.resourcePolicies.list</code></p>
<p><code>compute.rolloutPlans.get</code></p>
<p><code>compute.rolloutPlans.list</code></p>
<p><code>compute.rollouts.get</code></p>
<p><code>compute.rollouts.list</code></p>
<p><code>compute.routers.get</code></p>
<p><code>compute.routers.getRoutePolicy</code></p>
<p><code>compute.routers.list</code></p>
<p><code>compute.routers.listBgpRoutes</code></p>
<p><code>compute. routers. listEffectiveTags</code></p>
<p><code>compute. routers. listRoutePolicies</code></p>
<p><code>compute. routers. listTagBindings</code></p>
<p><code>compute.routes.get</code></p>
<p><code>compute.routes.list</code></p>
<p><code>compute. routes. listEffectiveTags</code></p>
<p><code>compute.routes.listTagBindings</code></p>
<p><code>compute.securityPolicies.get</code></p>
<p><code>compute.securityPolicies.list</code></p>
<p><code>compute. securityPolicies. listEffectiveTags</code></p>
<p><code>compute. securityPolicies. listTagBindings</code></p>
<p><code>compute.serviceAttachments.get</code></p>
<p><code>compute. serviceAttachments. getIamPolicy</code></p>
<p><code>compute. serviceAttachments. list</code></p>
<p><code>compute. serviceAttachments. listEffectiveTags</code></p>
<p><code>compute. serviceAttachments. listTagBindings</code></p>
<p><code>compute.snapshotGroups.get</code></p>
<p><code>compute. snapshotGroups. getIamPolicy</code></p>
<p><code>compute.snapshotGroups.list</code></p>
<p><code>compute. snapshotRecycleBinPolicy. get</code></p>
<p><code>compute.snapshotSettings.get</code></p>
<p><code>compute.snapshots.get</code></p>
<p><code>compute. snapshots. getEffectiveRecycleBinRule</code></p>
<p><code>compute.snapshots.getIamPolicy</code></p>
<p><code>compute.snapshots.list</code></p>
<p><code>compute. snapshots. listEffectiveTags</code></p>
<p><code>compute. snapshots. listTagBindings</code></p>
<p><code>compute.spotAssistants.get</code></p>
<p><code>compute.sslCertificates.get</code></p>
<p><code>compute.sslCertificates.list</code></p>
<p><code>compute. sslCertificates. listEffectiveTags</code></p>
<p><code>compute. sslCertificates. listTagBindings</code></p>
<p><code>compute.sslPolicies.get</code></p>
<p><code>compute. sslPolicies. getIamPolicy</code></p>
<p><code>compute.sslPolicies.list</code></p>
<p><code>compute. sslPolicies. listAvailableFeatures</code></p>
<p><code>compute. sslPolicies. listEffectiveTags</code></p>
<p><code>compute. sslPolicies. listTagBindings</code></p>
<p><code>compute.storagePools.get</code></p>
<p><code>compute. storagePools. getIamPolicy</code></p>
<p><code>compute.storagePools.list</code></p>
<p><code>compute. storagePools. listEffectiveTags</code></p>
<p><code>compute. storagePools. listTagBindings</code></p>
<p><code>compute.subnetworks.get</code></p>
<p><code>compute. subnetworks. getIamPolicy</code></p>
<p><code>compute.subnetworks.list</code></p>
<p><code>compute. subnetworks. listEffectiveTags</code></p>
<p><code>compute. subnetworks. listTagBindings</code></p>
<p><code>compute.targetGrpcProxies.get</code></p>
<p><code>compute.targetGrpcProxies.list</code></p>
<p><code>compute. targetGrpcProxies. listEffectiveTags</code></p>
<p><code>compute. targetGrpcProxies. listTagBindings</code></p>
<p><code>compute.targetHttpProxies.get</code></p>
<p><code>compute.targetHttpProxies.list</code></p>
<p><code>compute. targetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpProxies. listTagBindings</code></p>
<p><code>compute.targetHttpsProxies.get</code></p>
<p><code>compute. targetHttpsProxies. list</code></p>
<p><code>compute. targetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpsProxies. listTagBindings</code></p>
<p><code>compute.targetInstances.get</code></p>
<p><code>compute.targetInstances.list</code></p>
<p><code>compute. targetInstances. listEffectiveTags</code></p>
<p><code>compute. targetInstances. listTagBindings</code></p>
<p><code>compute.targetPools.get</code></p>
<p><code>compute.targetPools.list</code></p>
<p><code>compute. targetPools. listEffectiveTags</code></p>
<p><code>compute. targetPools. listTagBindings</code></p>
<p><code>compute.targetSslProxies.get</code></p>
<p><code>compute.targetSslProxies.list</code></p>
<p><code>compute. targetSslProxies. listEffectiveTags</code></p>
<p><code>compute. targetSslProxies. listTagBindings</code></p>
<p><code>compute.targetTcpProxies.get</code></p>
<p><code>compute.targetTcpProxies.list</code></p>
<p><code>compute. targetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. targetTcpProxies. listTagBindings</code></p>
<p><code>compute.targetVpnGateways.get</code></p>
<p><code>compute.targetVpnGateways.list</code></p>
<p><code>compute. targetVpnGateways. listEffectiveTags</code></p>
<p><code>compute. targetVpnGateways. listTagBindings</code></p>
<p><code>compute.urlMaps.get</code></p>
<p><code>compute.urlMaps.list</code></p>
<p><code>compute. urlMaps. listEffectiveTags</code></p>
<p><code>compute. urlMaps. listTagBindings</code></p>
<p><code>compute.urlMaps.validate</code></p>
<p><code>compute. vmExtensionPolicies. get</code></p>
<p><code>compute. vmExtensionPolicies. list</code></p>
<p><code>compute.vpnGateways.get</code></p>
<p><code>compute.vpnGateways.list</code></p>
<p><code>compute. vpnGateways. listEffectiveTags</code></p>
<p><code>compute. vpnGateways. listTagBindings</code></p>
<p><code>compute.vpnTunnels.get</code></p>
<p><code>compute.vpnTunnels.list</code></p>
<p><code>compute. vpnTunnels. listEffectiveTags</code></p>
<p><code>compute. vpnTunnels. listTagBindings</code></p>
<p><code>compute.wireGroups.get</code></p>
<p><code>compute.wireGroups.list</code></p>
<p><code>compute.zoneOperations.get</code></p>
<p><code>compute. zoneOperations. getIamPolicy</code></p>
<p><code>compute.zoneOperations.list</code></p>
<p><code>compute.zones.*</code></p>
<ul>
<li><code>compute.zones.get</code></li>
<li><code>compute.zones.list</code></li>
</ul>
<p><code>notebooks.environments.get</code></p>
<p><code>notebooks. environments. getIamPolicy</code></p>
<p><code>notebooks.environments.list</code></p>
<p><code>notebooks.executions.get</code></p>
<p><code>notebooks. executions. getIamPolicy</code></p>
<p><code>notebooks.executions.list</code></p>
<p><code>notebooks. instances. checkUpgradability</code></p>
<p><code>notebooks.instances.get</code></p>
<p><code>notebooks.instances.getHealth</code></p>
<p><code>notebooks. instances. getIamPolicy</code></p>
<p><code>notebooks.instances.list</code></p>
<p><code>notebooks. instances. listEffectiveTags</code></p>
<p><code>notebooks. instances. listTagBindings</code></p>
<p><code>notebooks.locations.*</code></p>
<ul>
<li><code>notebooks.locations.get</code></li>
<li><code>notebooks.locations.list</code></li>
</ul>
<p><code>notebooks.operations.get</code></p>
<p><code>notebooks.operations.list</code></p>
<p><code>notebooks.runtimes.get</code></p>
<p><code>notebooks. runtimes. getIamPolicy</code></p>
<p><code>notebooks.runtimes.list</code></p>
<p><code>notebooks.schedules.get</code></p>
<p><code>notebooks. schedules. getIamPolicy</code></p>
<p><code>notebooks.schedules.list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p>
<p><code>serviceusage. consumerpolicy. analyze</code></p>
<p><code>serviceusage. consumerpolicy. get</code></p>
<p><code>serviceusage. effectivepolicy. get</code></p>
<p><code>serviceusage.groups.*</code></p>
<ul>
<li><code>serviceusage.groups.list</code></li>
<li><code>serviceusage. groups. listExpandedMembers</code></li>
<li><code>serviceusage. groups. listMembers</code></li>
</ul>
<p><code>serviceusage.quotas.get</code></p>
<p><code>serviceusage.services.get</code></p>
<p><code>serviceusage.services.list</code></p>
<p><code>serviceusage.values.test</code></p></td>
</tr>
<tr class="even">
<td>Notebooks Runner
<p>( <code>roles/ notebooks.runner</code> )</p>
<p>Restricted access for running scheduled Notebooks.</p></td>
<td><p><code>aiplatform. notebookExecutionJobs.*</code></p>
<ul>
<li><code>aiplatform. notebookExecutionJobs. create</code></li>
<li><code>aiplatform. notebookExecutionJobs. delete</code></li>
<li><code>aiplatform. notebookExecutionJobs. get</code></li>
<li><code>aiplatform. notebookExecutionJobs. list</code></li>
</ul>
<p><code>aiplatform.operations.list</code></p>
<p><code>aiplatform.pipelineJobs.create</code></p>
<p><code>aiplatform.schedules.*</code></p>
<ul>
<li><code>aiplatform.schedules.create</code></li>
<li><code>aiplatform.schedules.delete</code></li>
<li><code>aiplatform.schedules.get</code></li>
<li><code>aiplatform.schedules.list</code></li>
<li><code>aiplatform.schedules.update</code></li>
</ul>
<p><code>compute.acceleratorTypes.*</code></p>
<ul>
<li><code>compute.acceleratorTypes.get</code></li>
<li><code>compute.acceleratorTypes.list</code></li>
</ul>
<p><code>compute.addresses.get</code></p>
<p><code>compute.addresses.list</code></p>
<p><code>compute. addresses. listEffectiveTags</code></p>
<p><code>compute. addresses. listTagBindings</code></p>
<p><code>compute.advice.capacity</code></p>
<p><code>compute.advice.capacityHistory</code></p>
<p><code>compute.autoscalers.get</code></p>
<p><code>compute.autoscalers.list</code></p>
<p><code>compute.backendBuckets.get</code></p>
<p><code>compute. backendBuckets. getIamPolicy</code></p>
<p><code>compute.backendBuckets.list</code></p>
<p><code>compute. backendBuckets. listEffectiveTags</code></p>
<p><code>compute. backendBuckets. listTagBindings</code></p>
<p><code>compute.backendServices.get</code></p>
<p><code>compute. backendServices. getIamPolicy</code></p>
<p><code>compute.backendServices.list</code></p>
<p><code>compute. backendServices. listEffectiveTags</code></p>
<p><code>compute. backendServices. listTagBindings</code></p>
<p><code>compute.commitments.get</code></p>
<p><code>compute.commitments.list</code></p>
<p><code>compute. commitments. listEffectiveTags</code></p>
<p><code>compute. commitments. listTagBindings</code></p>
<p><code>compute.crossSiteNetworks.get</code></p>
<p><code>compute.crossSiteNetworks.list</code></p>
<p><code>compute.diskSettings.get</code></p>
<p><code>compute.diskTypes.*</code></p>
<ul>
<li><code>compute.diskTypes.get</code></li>
<li><code>compute.diskTypes.list</code></li>
</ul>
<p><code>compute.disks.get</code></p>
<p><code>compute.disks.getIamPolicy</code></p>
<p><code>compute.disks.list</code></p>
<p><code>compute. disks. listEffectiveTags</code></p>
<p><code>compute.disks.listTagBindings</code></p>
<p><code>compute. externalVpnGateways. get</code></p>
<p><code>compute. externalVpnGateways. list</code></p>
<p><code>compute. externalVpnGateways. listEffectiveTags</code></p>
<p><code>compute. externalVpnGateways. listTagBindings</code></p>
<p><code>compute.firewallPolicies.get</code></p>
<p><code>compute. firewallPolicies. getIamPolicy</code></p>
<p><code>compute.firewallPolicies.list</code></p>
<p><code>compute. firewallPolicies. listEffectiveTags</code></p>
<p><code>compute. firewallPolicies. listTagBindings</code></p>
<p><code>compute.firewalls.get</code></p>
<p><code>compute.firewalls.list</code></p>
<p><code>compute. firewalls. listEffectiveTags</code></p>
<p><code>compute. firewalls. listTagBindings</code></p>
<p><code>compute.forwardingRules.get</code></p>
<p><code>compute.forwardingRules.list</code></p>
<p><code>compute. forwardingRules. listEffectiveTags</code></p>
<p><code>compute. forwardingRules. listTagBindings</code></p>
<p><code>compute.futureReservations.get</code></p>
<p><code>compute. futureReservations. getIamPolicy</code></p>
<p><code>compute. futureReservations. list</code></p>
<p><code>compute. futureReservations. listEffectiveTags</code></p>
<p><code>compute. futureReservations. listTagBindings</code></p>
<p><code>compute.globalAddresses.get</code></p>
<p><code>compute.globalAddresses.list</code></p>
<p><code>compute. globalAddresses. listEffectiveTags</code></p>
<p><code>compute. globalAddresses. listTagBindings</code></p>
<p><code>compute. globalForwardingRules. get</code></p>
<p><code>compute. globalForwardingRules. list</code></p>
<p><code>compute. globalForwardingRules. listEffectiveTags</code></p>
<p><code>compute. globalForwardingRules. listTagBindings</code></p>
<p><code>compute. globalFrontendSettings. get</code></p>
<p><code>compute. globalNetworkEndpointGroups. get</code></p>
<p><code>compute. globalNetworkEndpointGroups. list</code></p>
<p><code>compute. globalNetworkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. globalNetworkEndpointGroups. listTagBindings</code></p>
<p><code>compute.globalOperations.get</code></p>
<p><code>compute. globalOperations. getIamPolicy</code></p>
<p><code>compute.globalOperations.list</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. get</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. list</code></p>
<p><code>compute.healthChecks.get</code></p>
<p><code>compute.healthChecks.list</code></p>
<p><code>compute. healthChecks. listEffectiveTags</code></p>
<p><code>compute. healthChecks. listTagBindings</code></p>
<p><code>compute.hosts.*</code></p>
<ul>
<li><code>compute.hosts.get</code></li>
<li><code>compute.hosts.getVersion</code></li>
<li><code>compute.hosts.list</code></li>
</ul>
<p><code>compute.httpHealthChecks.get</code></p>
<p><code>compute.httpHealthChecks.list</code></p>
<p><code>compute. httpHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpHealthChecks. listTagBindings</code></p>
<p><code>compute.httpsHealthChecks.get</code></p>
<p><code>compute.httpsHealthChecks.list</code></p>
<p><code>compute. httpsHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpsHealthChecks. listTagBindings</code></p>
<p><code>compute.images.get</code></p>
<p><code>compute.images.getFromFamily</code></p>
<p><code>compute.images.getIamPolicy</code></p>
<p><code>compute.images.list</code></p>
<p><code>compute. images. listEffectiveTags</code></p>
<p><code>compute.images.listTagBindings</code></p>
<p><code>compute. instanceGroupManagers. get</code></p>
<p><code>compute. instanceGroupManagers. list</code></p>
<p><code>compute. instanceGroupManagers. listEffectiveTags</code></p>
<p><code>compute. instanceGroupManagers. listTagBindings</code></p>
<p><code>compute.instanceGroups.get</code></p>
<p><code>compute.instanceGroups.list</code></p>
<p><code>compute. instanceGroups. listEffectiveTags</code></p>
<p><code>compute. instanceGroups. listTagBindings</code></p>
<p><code>compute.instanceSettings.get</code></p>
<p><code>compute.instanceTemplates.get</code></p>
<p><code>compute. instanceTemplates. getIamPolicy</code></p>
<p><code>compute.instanceTemplates.list</code></p>
<p><code>compute.instances.get</code></p>
<p><code>compute. instances. getEffectiveFirewalls</code></p>
<p><code>compute. instances. getGuestAttributes</code></p>
<p><code>compute.instances.getIamPolicy</code></p>
<p><code>compute. instances. getScreenshot</code></p>
<p><code>compute. instances. getSerialPortOutput</code></p>
<p><code>compute. instances. getShieldedInstanceIdentity</code></p>
<p><code>compute. instances. getShieldedVmIdentity</code></p>
<p><code>compute. instances. getVmExtensionState</code></p>
<p><code>compute.instances.list</code></p>
<p><code>compute. instances. listEffectiveTags</code></p>
<p><code>compute. instances. listReferrers</code></p>
<p><code>compute. instances. listTagBindings</code></p>
<p><code>compute. instances. listVmExtensionStates</code></p>
<p><code>compute.instances.troubleshoot</code></p>
<p><code>compute. instantSnapshotGroups. get</code></p>
<p><code>compute. instantSnapshotGroups. getIamPolicy</code></p>
<p><code>compute. instantSnapshotGroups. list</code></p>
<p><code>compute.instantSnapshots.get</code></p>
<p><code>compute. instantSnapshots. getIamPolicy</code></p>
<p><code>compute.instantSnapshots.list</code></p>
<p><code>compute. instantSnapshots. listEffectiveTags</code></p>
<p><code>compute. instantSnapshots. listTagBindings</code></p>
<p><code>compute. interconnectAttachmentGroups. get</code></p>
<p><code>compute. interconnectAttachmentGroups. list</code></p>
<p><code>compute. interconnectAttachments. get</code></p>
<p><code>compute. interconnectAttachments. list</code></p>
<p><code>compute. interconnectAttachments. listEffectiveTags</code></p>
<p><code>compute. interconnectAttachments. listTagBindings</code></p>
<p><code>compute.interconnectGroups.get</code></p>
<p><code>compute. interconnectGroups. list</code></p>
<p><code>compute. interconnectLocations.*</code></p>
<ul>
<li><code>compute. interconnectLocations. get</code></li>
<li><code>compute. interconnectLocations. list</code></li>
</ul>
<p><code>compute. interconnectRemoteLocations.*</code></p>
<ul>
<li><code>compute. interconnectRemoteLocations. get</code></li>
<li><code>compute. interconnectRemoteLocations. list</code></li>
</ul>
<p><code>compute.interconnects.get</code></p>
<p><code>compute.interconnects.list</code></p>
<p><code>compute. interconnects. listEffectiveTags</code></p>
<p><code>compute. interconnects. listTagBindings</code></p>
<p><code>compute.licenseCodes.get</code></p>
<p><code>compute. licenseCodes. getIamPolicy</code></p>
<p><code>compute.licenseCodes.list</code></p>
<p><code>compute.licenses.get</code></p>
<p><code>compute.licenses.getIamPolicy</code></p>
<p><code>compute.licenses.list</code></p>
<p><code>compute. licenses. listEffectiveTags</code></p>
<p><code>compute. licenses. listTagBindings</code></p>
<p><code>compute.machineImages.get</code></p>
<p><code>compute. machineImages. getIamPolicy</code></p>
<p><code>compute.machineImages.list</code></p>
<p><code>compute. machineImages. listEffectiveTags</code></p>
<p><code>compute. machineImages. listTagBindings</code></p>
<p><code>compute.machineTypes.*</code></p>
<ul>
<li><code>compute.machineTypes.get</code></li>
<li><code>compute.machineTypes.list</code></li>
</ul>
<p><code>compute.managedRulesets.*</code></p>
<ul>
<li><code>compute.managedRulesets.get</code></li>
<li><code>compute.managedRulesets.list</code></li>
</ul>
<p><code>compute.multiMig.get</code></p>
<p><code>compute.multiMig.list</code></p>
<p><code>compute.multiMigMembers.*</code></p>
<ul>
<li><code>compute.multiMigMembers.get</code></li>
<li><code>compute.multiMigMembers.list</code></li>
</ul>
<p><code>compute.networkAttachments.get</code></p>
<p><code>compute. networkAttachments. getIamPolicy</code></p>
<p><code>compute. networkAttachments. list</code></p>
<p><code>compute. networkAttachments. listEffectiveTags</code></p>
<p><code>compute. networkAttachments. listTagBindings</code></p>
<p><code>compute. networkEdgeSecurityServices. get</code></p>
<p><code>compute. networkEdgeSecurityServices. list</code></p>
<p><code>compute. networkEdgeSecurityServices. listEffectiveTags</code></p>
<p><code>compute. networkEdgeSecurityServices. listTagBindings</code></p>
<p><code>compute. networkEndpointGroups. get</code></p>
<p><code>compute. networkEndpointGroups. list</code></p>
<p><code>compute. networkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. networkEndpointGroups. listTagBindings</code></p>
<p><code>compute.networkProfiles.*</code></p>
<ul>
<li><code>compute.networkProfiles.get</code></li>
<li><code>compute.networkProfiles.list</code></li>
</ul>
<p><code>compute.networks.get</code></p>
<p><code>compute. networks. getEffectiveFirewalls</code></p>
<p><code>compute. networks. getRegionEffectiveFirewalls</code></p>
<p><code>compute.networks.list</code></p>
<p><code>compute. networks. listEffectiveTags</code></p>
<p><code>compute. networks. listPeeringRoutes</code></p>
<p><code>compute. networks. listTagBindings</code></p>
<p><code>compute.nodeGroups.get</code></p>
<p><code>compute. nodeGroups. getIamPolicy</code></p>
<p><code>compute.nodeGroups.list</code></p>
<p><code>compute.nodeTemplates.get</code></p>
<p><code>compute. nodeTemplates. getIamPolicy</code></p>
<p><code>compute.nodeTemplates.list</code></p>
<p><code>compute.nodeTypes.*</code></p>
<ul>
<li><code>compute.nodeTypes.get</code></li>
<li><code>compute.nodeTypes.list</code></li>
</ul>
<p><code>compute.orgRolloutPlans.get</code></p>
<p><code>compute.orgRolloutPlans.list</code></p>
<p><code>compute.orgRollouts.get</code></p>
<p><code>compute.orgRollouts.list</code></p>
<p><code>compute. organizations. listAssociations</code></p>
<p><code>compute.packetMirrorings.get</code></p>
<p><code>compute.packetMirrorings.list</code></p>
<p><code>compute. packetMirrorings. listEffectiveTags</code></p>
<p><code>compute. packetMirrorings. listTagBindings</code></p>
<p><code>compute.previewFeatures.get</code></p>
<p><code>compute.previewFeatures.list</code></p>
<p><code>compute.projects.get</code></p>
<p><code>compute. publicAdvertisedPrefixes. get</code></p>
<p><code>compute. publicAdvertisedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. get</code></p>
<p><code>compute. publicDelegatedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. listEffectiveTags</code></p>
<p><code>compute. publicDelegatedPrefixes. listTagBindings</code></p>
<p><code>compute. recoverableSnapshots. get</code></p>
<p><code>compute. recoverableSnapshots. getIamPolicy</code></p>
<p><code>compute. recoverableSnapshots. list</code></p>
<p><code>compute. regionBackendBuckets. get</code></p>
<p><code>compute. regionBackendBuckets. getIamPolicy</code></p>
<p><code>compute. regionBackendBuckets. list</code></p>
<p><code>compute. regionBackendBuckets. listEffectiveTags</code></p>
<p><code>compute. regionBackendBuckets. listTagBindings</code></p>
<p><code>compute. regionBackendServices. get</code></p>
<p><code>compute. regionBackendServices. getIamPolicy</code></p>
<p><code>compute. regionBackendServices. list</code></p>
<p><code>compute. regionBackendServices. listEffectiveTags</code></p>
<p><code>compute. regionBackendServices. listTagBindings</code></p>
<p><code>compute. regionCompositeHealthChecks. get</code></p>
<p><code>compute. regionCompositeHealthChecks. list</code></p>
<p><code>compute. regionFirewallPolicies. get</code></p>
<p><code>compute. regionFirewallPolicies. getIamPolicy</code></p>
<p><code>compute. regionFirewallPolicies. list</code></p>
<p><code>compute. regionFirewallPolicies. listEffectiveTags</code></p>
<p><code>compute. regionFirewallPolicies. listTagBindings</code></p>
<p><code>compute. regionHealthAggregationPolicies. get</code></p>
<p><code>compute. regionHealthAggregationPolicies. list</code></p>
<p><code>compute. regionHealthCheckServices. get</code></p>
<p><code>compute. regionHealthCheckServices. list</code></p>
<p><code>compute.regionHealthChecks.get</code></p>
<p><code>compute. regionHealthChecks. list</code></p>
<p><code>compute. regionHealthChecks. listEffectiveTags</code></p>
<p><code>compute. regionHealthChecks. listTagBindings</code></p>
<p><code>compute. regionHealthSources. get</code></p>
<p><code>compute. regionHealthSources. list</code></p>
<p><code>compute. regionNetworkEndpointGroups. get</code></p>
<p><code>compute. regionNetworkEndpointGroups. list</code></p>
<p><code>compute. regionNetworkEndpointGroups. listEffectiveTags</code></p>
<p><code>compute. regionNetworkEndpointGroups. listTagBindings</code></p>
<p><code>compute. regionNetworkPolicies. get</code></p>
<p><code>compute. regionNetworkPolicies. list</code></p>
<p><code>compute. regionNotificationEndpoints. get</code></p>
<p><code>compute. regionNotificationEndpoints. list</code></p>
<p><code>compute.regionOperations.get</code></p>
<p><code>compute. regionOperations. getIamPolicy</code></p>
<p><code>compute.regionOperations.list</code></p>
<p><code>compute. regionSecurityPolicies. get</code></p>
<p><code>compute. regionSecurityPolicies. list</code></p>
<p><code>compute. regionSecurityPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSecurityPolicies. listTagBindings</code></p>
<p><code>compute. regionSslCertificates. get</code></p>
<p><code>compute. regionSslCertificates. list</code></p>
<p><code>compute. regionSslCertificates. listEffectiveTags</code></p>
<p><code>compute. regionSslCertificates. listTagBindings</code></p>
<p><code>compute.regionSslPolicies.get</code></p>
<p><code>compute. regionSslPolicies. getIamPolicy</code></p>
<p><code>compute.regionSslPolicies.list</code></p>
<p><code>compute. regionSslPolicies. listAvailableFeatures</code></p>
<p><code>compute. regionSslPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSslPolicies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpProxies. get</code></p>
<p><code>compute. regionTargetHttpProxies. list</code></p>
<p><code>compute. regionTargetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpProxies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpsProxies. get</code></p>
<p><code>compute. regionTargetHttpsProxies. list</code></p>
<p><code>compute. regionTargetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpsProxies. listTagBindings</code></p>
<p><code>compute. regionTargetTcpProxies. get</code></p>
<p><code>compute. regionTargetTcpProxies. list</code></p>
<p><code>compute. regionTargetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetTcpProxies. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.get</code></p>
<p><code>compute.regionUrlMaps.list</code></p>
<p><code>compute. regionUrlMaps. listEffectiveTags</code></p>
<p><code>compute. regionUrlMaps. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.validate</code></p>
<p><code>compute.regions.*</code></p>
<ul>
<li><code>compute.regions.get</code></li>
<li><code>compute.regions.list</code></li>
</ul>
<p><code>compute.reliabilityRisks.*</code></p>
<ul>
<li><code>compute.reliabilityRisks.get</code></li>
<li><code>compute.reliabilityRisks.list</code></li>
</ul>
<p><code>compute.reservationBlocks.get</code></p>
<p><code>compute.reservationBlocks.list</code></p>
<p><code>compute. reservationConsumedInstances. list</code></p>
<p><code>compute.reservationSlots.get</code></p>
<p><code>compute.reservationSlots.list</code></p>
<p><code>compute. reservationSubBlocks. get</code></p>
<p><code>compute. reservationSubBlocks. list</code></p>
<p><code>compute.reservations.get</code></p>
<p><code>compute.reservations.list</code></p>
<p><code>compute. reservations. listEffectiveTags</code></p>
<p><code>compute. reservations. listTagBindings</code></p>
<p><code>compute.resourcePolicies.get</code></p>
<p><code>compute. resourcePolicies. getIamPolicy</code></p>
<p><code>compute.resourcePolicies.list</code></p>
<p><code>compute.rolloutPlans.get</code></p>
<p><code>compute.rolloutPlans.list</code></p>
<p><code>compute.rollouts.get</code></p>
<p><code>compute.rollouts.list</code></p>
<p><code>compute.routers.get</code></p>
<p><code>compute.routers.getRoutePolicy</code></p>
<p><code>compute.routers.list</code></p>
<p><code>compute.routers.listBgpRoutes</code></p>
<p><code>compute. routers. listEffectiveTags</code></p>
<p><code>compute. routers. listRoutePolicies</code></p>
<p><code>compute. routers. listTagBindings</code></p>
<p><code>compute.routes.get</code></p>
<p><code>compute.routes.list</code></p>
<p><code>compute. routes. listEffectiveTags</code></p>
<p><code>compute.routes.listTagBindings</code></p>
<p><code>compute.securityPolicies.get</code></p>
<p><code>compute.securityPolicies.list</code></p>
<p><code>compute. securityPolicies. listEffectiveTags</code></p>
<p><code>compute. securityPolicies. listTagBindings</code></p>
<p><code>compute.serviceAttachments.get</code></p>
<p><code>compute. serviceAttachments. getIamPolicy</code></p>
<p><code>compute. serviceAttachments. list</code></p>
<p><code>compute. serviceAttachments. listEffectiveTags</code></p>
<p><code>compute. serviceAttachments. listTagBindings</code></p>
<p><code>compute.snapshotGroups.get</code></p>
<p><code>compute. snapshotGroups. getIamPolicy</code></p>
<p><code>compute.snapshotGroups.list</code></p>
<p><code>compute. snapshotRecycleBinPolicy. get</code></p>
<p><code>compute.snapshotSettings.get</code></p>
<p><code>compute.snapshots.get</code></p>
<p><code>compute. snapshots. getEffectiveRecycleBinRule</code></p>
<p><code>compute.snapshots.getIamPolicy</code></p>
<p><code>compute.snapshots.list</code></p>
<p><code>compute. snapshots. listEffectiveTags</code></p>
<p><code>compute. snapshots. listTagBindings</code></p>
<p><code>compute.spotAssistants.get</code></p>
<p><code>compute.sslCertificates.get</code></p>
<p><code>compute.sslCertificates.list</code></p>
<p><code>compute. sslCertificates. listEffectiveTags</code></p>
<p><code>compute. sslCertificates. listTagBindings</code></p>
<p><code>compute.sslPolicies.get</code></p>
<p><code>compute. sslPolicies. getIamPolicy</code></p>
<p><code>compute.sslPolicies.list</code></p>
<p><code>compute. sslPolicies. listAvailableFeatures</code></p>
<p><code>compute. sslPolicies. listEffectiveTags</code></p>
<p><code>compute. sslPolicies. listTagBindings</code></p>
<p><code>compute.storagePools.get</code></p>
<p><code>compute. storagePools. getIamPolicy</code></p>
<p><code>compute.storagePools.list</code></p>
<p><code>compute. storagePools. listEffectiveTags</code></p>
<p><code>compute. storagePools. listTagBindings</code></p>
<p><code>compute.subnetworks.get</code></p>
<p><code>compute. subnetworks. getIamPolicy</code></p>
<p><code>compute.subnetworks.list</code></p>
<p><code>compute. subnetworks. listEffectiveTags</code></p>
<p><code>compute. subnetworks. listTagBindings</code></p>
<p><code>compute.targetGrpcProxies.get</code></p>
<p><code>compute.targetGrpcProxies.list</code></p>
<p><code>compute. targetGrpcProxies. listEffectiveTags</code></p>
<p><code>compute. targetGrpcProxies. listTagBindings</code></p>
<p><code>compute.targetHttpProxies.get</code></p>
<p><code>compute.targetHttpProxies.list</code></p>
<p><code>compute. targetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpProxies. listTagBindings</code></p>
<p><code>compute.targetHttpsProxies.get</code></p>
<p><code>compute. targetHttpsProxies. list</code></p>
<p><code>compute. targetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpsProxies. listTagBindings</code></p>
<p><code>compute.targetInstances.get</code></p>
<p><code>compute.targetInstances.list</code></p>
<p><code>compute. targetInstances. listEffectiveTags</code></p>
<p><code>compute. targetInstances. listTagBindings</code></p>
<p><code>compute.targetPools.get</code></p>
<p><code>compute.targetPools.list</code></p>
<p><code>compute. targetPools. listEffectiveTags</code></p>
<p><code>compute. targetPools. listTagBindings</code></p>
<p><code>compute.targetSslProxies.get</code></p>
<p><code>compute.targetSslProxies.list</code></p>
<p><code>compute. targetSslProxies. listEffectiveTags</code></p>
<p><code>compute. targetSslProxies. listTagBindings</code></p>
<p><code>compute.targetTcpProxies.get</code></p>
<p><code>compute.targetTcpProxies.list</code></p>
<p><code>compute. targetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. targetTcpProxies. listTagBindings</code></p>
<p><code>compute.targetVpnGateways.get</code></p>
<p><code>compute.targetVpnGateways.list</code></p>
<p><code>compute. targetVpnGateways. listEffectiveTags</code></p>
<p><code>compute. targetVpnGateways. listTagBindings</code></p>
<p><code>compute.urlMaps.get</code></p>
<p><code>compute.urlMaps.list</code></p>
<p><code>compute. urlMaps. listEffectiveTags</code></p>
<p><code>compute. urlMaps. listTagBindings</code></p>
<p><code>compute.urlMaps.validate</code></p>
<p><code>compute. vmExtensionPolicies. get</code></p>
<p><code>compute. vmExtensionPolicies. list</code></p>
<p><code>compute.vpnGateways.get</code></p>
<p><code>compute.vpnGateways.list</code></p>
<p><code>compute. vpnGateways. listEffectiveTags</code></p>
<p><code>compute. vpnGateways. listTagBindings</code></p>
<p><code>compute.vpnTunnels.get</code></p>
<p><code>compute.vpnTunnels.list</code></p>
<p><code>compute. vpnTunnels. listEffectiveTags</code></p>
<p><code>compute. vpnTunnels. listTagBindings</code></p>
<p><code>compute.wireGroups.get</code></p>
<p><code>compute.wireGroups.list</code></p>
<p><code>compute.zoneOperations.get</code></p>
<p><code>compute. zoneOperations. getIamPolicy</code></p>
<p><code>compute.zoneOperations.list</code></p>
<p><code>compute.zones.*</code></p>
<ul>
<li><code>compute.zones.get</code></li>
<li><code>compute.zones.list</code></li>
</ul>
<p><code>notebooks.environments.get</code></p>
<p><code>notebooks. environments. getIamPolicy</code></p>
<p><code>notebooks.environments.list</code></p>
<p><code>notebooks.executions.create</code></p>
<p><code>notebooks.executions.get</code></p>
<p><code>notebooks. executions. getIamPolicy</code></p>
<p><code>notebooks.executions.list</code></p>
<p><code>notebooks. instances. checkUpgradability</code></p>
<p><code>notebooks.instances.create</code></p>
<p><code>notebooks.instances.get</code></p>
<p><code>notebooks.instances.getHealth</code></p>
<p><code>notebooks. instances. getIamPolicy</code></p>
<p><code>notebooks.instances.list</code></p>
<p><code>notebooks. instances. listEffectiveTags</code></p>
<p><code>notebooks. instances. listTagBindings</code></p>
<p><code>notebooks.locations.*</code></p>
<ul>
<li><code>notebooks.locations.get</code></li>
<li><code>notebooks.locations.list</code></li>
</ul>
<p><code>notebooks.operations.get</code></p>
<p><code>notebooks.operations.list</code></p>
<p><code>notebooks.runtimes.create</code></p>
<p><code>notebooks.runtimes.get</code></p>
<p><code>notebooks. runtimes. getIamPolicy</code></p>
<p><code>notebooks.runtimes.list</code></p>
<p><code>notebooks.schedules.create</code></p>
<p><code>notebooks.schedules.get</code></p>
<p><code>notebooks. schedules. getIamPolicy</code></p>
<p><code>notebooks.schedules.list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p>
<p><code>serviceusage. consumerpolicy. analyze</code></p>
<p><code>serviceusage. consumerpolicy. get</code></p>
<p><code>serviceusage. effectivepolicy. get</code></p>
<p><code>serviceusage.groups.*</code></p>
<ul>
<li><code>serviceusage.groups.list</code></li>
<li><code>serviceusage. groups. listExpandedMembers</code></li>
<li><code>serviceusage. groups. listMembers</code></li>
</ul>
<p><code>serviceusage.quotas.get</code></p>
<p><code>serviceusage.services.get</code></p>
<p><code>serviceusage.services.list</code></p>
<p><code>serviceusage.values.test</code></p></td>
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
<td>AI Platform Notebooks Service Agent
<p>( <code>roles/ notebooks.serviceAgent</code> )</p>
<p>Provide access for notebooks service agent to manage notebook instances in user projects</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code>aiplatform.customJobs.cancel</code></p>
<p><code>aiplatform.customJobs.create</code></p>
<p><code>aiplatform.customJobs.get</code></p>
<p><code>aiplatform.customJobs.list</code></p>
<p><code>aiplatform. notebookExecutionJobs.*</code></p>
<ul>
<li><code>aiplatform. notebookExecutionJobs. create</code></li>
<li><code>aiplatform. notebookExecutionJobs. delete</code></li>
<li><code>aiplatform. notebookExecutionJobs. get</code></li>
<li><code>aiplatform. notebookExecutionJobs. list</code></li>
</ul>
<p><code>aiplatform. notebookRuntimes. get</code></p>
<p><code>aiplatform.operations.list</code></p>
<p><code>aiplatform.pipelineJobs.create</code></p>
<p><code>aiplatform.schedules.*</code></p>
<ul>
<li><code>aiplatform.schedules.create</code></li>
<li><code>aiplatform.schedules.delete</code></li>
<li><code>aiplatform.schedules.get</code></li>
<li><code>aiplatform.schedules.list</code></li>
<li><code>aiplatform.schedules.update</code></li>
</ul>
<p><code>backupdr. backupPlanAssociations. createForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. createForComputeInstance</code></p>
<p><code>backupdr. backupPlanAssociations. deleteForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. deleteForComputeInstance</code></p>
<p><code>backupdr. backupPlanAssociations. fetchForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. getForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. list</code></p>
<p><code>backupdr. backupPlanAssociations. triggerBackupForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. triggerBackupForComputeInstance</code></p>
<p><code>backupdr. backupPlanAssociations. updateForComputeDisk</code></p>
<p><code>backupdr. backupPlanAssociations. updateForComputeInstance</code></p>
<p><code>backupdr.backupPlans.get</code></p>
<p><code>backupdr.backupPlans.list</code></p>
<p><code>backupdr. backupPlans. useForComputeDisk</code></p>
<p><code>backupdr. backupPlans. useForComputeInstance</code></p>
<p><code>backupdr.backupVaults.get</code></p>
<p><code>backupdr.backupVaults.list</code></p>
<p><code>backupdr.locations.list</code></p>
<p><code>backupdr.operations.get</code></p>
<p><code>backupdr.operations.list</code></p>
<p><code>backupdr. serviceConfig. initialize</code></p>
<p><code>compute.acceleratorTypes.*</code></p>
<ul>
<li><code>compute.acceleratorTypes.get</code></li>
<li><code>compute.acceleratorTypes.list</code></li>
</ul>
<p><code>compute. addresses. createInternal</code></p>
<p><code>compute. addresses. deleteInternal</code></p>
<p><code>compute.addresses.get</code></p>
<p><code>compute.addresses.list</code></p>
<p><code>compute. addresses. listEffectiveTags</code></p>
<p><code>compute. addresses. listTagBindings</code></p>
<p><code>compute.addresses.use</code></p>
<p><code>compute.addresses.useInternal</code></p>
<p><code>compute.advice.capacity</code></p>
<p><code>compute.advice.capacityHistory</code></p>
<p><code>compute.autoscalers.*</code></p>
<ul>
<li><code>compute.autoscalers.create</code></li>
<li><code>compute.autoscalers.delete</code></li>
<li><code>compute.autoscalers.get</code></li>
<li><code>compute.autoscalers.list</code></li>
<li><code>compute.autoscalers.update</code></li>
</ul>
<p><code>compute.backendBuckets.get</code></p>
<p><code>compute. backendBuckets. getIamPolicy</code></p>
<p><code>compute.backendBuckets.list</code></p>
<p><code>compute. backendBuckets. listEffectiveTags</code></p>
<p><code>compute. backendBuckets. listTagBindings</code></p>
<p><code>compute.backendServices.get</code></p>
<p><code>compute. backendServices. getIamPolicy</code></p>
<p><code>compute.backendServices.list</code></p>
<p><code>compute. backendServices. listEffectiveTags</code></p>
<p><code>compute. backendServices. listTagBindings</code></p>
<p><code>compute.commitments.get</code></p>
<p><code>compute.commitments.list</code></p>
<p><code>compute. commitments. listEffectiveTags</code></p>
<p><code>compute. commitments. listTagBindings</code></p>
<p><code>compute.crossSiteNetworks.get</code></p>
<p><code>compute.crossSiteNetworks.list</code></p>
<p><code>compute.diskSettings.get</code></p>
<p><code>compute.diskTypes.*</code></p>
<ul>
<li><code>compute.diskTypes.get</code></li>
<li><code>compute.diskTypes.list</code></li>
</ul>
<p><code>compute.disks.*</code></p>
<ul>
<li><code>compute. disks. addResourcePolicies</code></li>
<li><code>compute.disks.create</code></li>
<li><code>compute.disks.createSnapshot</code></li>
<li><code>compute.disks.createTagBinding</code></li>
<li><code>compute.disks.delete</code></li>
<li><code>compute.disks.deleteTagBinding</code></li>
<li><code>compute.disks.get</code></li>
<li><code>compute.disks.getIamPolicy</code></li>
<li><code>compute.disks.list</code></li>
<li><code>compute. disks. listEffectiveTags</code></li>
<li><code>compute.disks.listTagBindings</code></li>
<li><code>compute. disks. removeResourcePolicies</code></li>
<li><code>compute.disks.resize</code></li>
<li><code>compute.disks.setIamPolicy</code></li>
<li><code>compute.disks.setLabels</code></li>
<li><code>compute. disks. startAsyncReplication</code></li>
<li><code>compute. disks. stopAsyncReplication</code></li>
<li><code>compute. disks. stopGroupAsyncReplication</code></li>
<li><code>compute.disks.update</code></li>
<li><code>compute.disks.updateKmsKey</code></li>
<li><code>compute.disks.use</code></li>
<li><code>compute.disks.useReadOnly</code></li>
</ul>
<p><code>compute. externalVpnGateways. get</code></p>
<p><code>compute. externalVpnGateways. list</code></p>
<p><code>compute. externalVpnGateways. listEffectiveTags</code></p>
<p><code>compute. externalVpnGateways. listTagBindings</code></p>
<p><code>compute.firewallPolicies.get</code></p>
<p><code>compute. firewallPolicies. getIamPolicy</code></p>
<p><code>compute.firewallPolicies.list</code></p>
<p><code>compute. firewallPolicies. listEffectiveTags</code></p>
<p><code>compute. firewallPolicies. listTagBindings</code></p>
<p><code>compute.firewalls.get</code></p>
<p><code>compute.firewalls.list</code></p>
<p><code>compute. firewalls. listEffectiveTags</code></p>
<p><code>compute. firewalls. listTagBindings</code></p>
<p><code>compute.forwardingRules.get</code></p>
<p><code>compute.forwardingRules.list</code></p>
<p><code>compute. forwardingRules. listEffectiveTags</code></p>
<p><code>compute. forwardingRules. listTagBindings</code></p>
<p><code>compute.futureReservations.get</code></p>
<p><code>compute. futureReservations. getIamPolicy</code></p>
<p><code>compute. futureReservations. list</code></p>
<p><code>compute. futureReservations. listEffectiveTags</code></p>
<p><code>compute. futureReservations. listTagBindings</code></p>
<p><code>compute.globalAddresses.get</code></p>
<p><code>compute.globalAddresses.list</code></p>
<p><code>compute. globalAddresses. listEffectiveTags</code></p>
<p><code>compute. globalAddresses. listTagBindings</code></p>
<p><code>compute.globalAddresses.use</code></p>
<p><code>compute. globalForwardingRules. get</code></p>
<p><code>compute. globalForwardingRules. list</code></p>
<p><code>compute. globalForwardingRules. listEffectiveTags</code></p>
<p><code>compute. globalForwardingRules. listTagBindings</code></p>
<p><code>compute. globalFrontendSettings. get</code></p>
<p><code>compute. globalNetworkEndpointGroups.*</code></p>
<ul>
<li><code>compute. globalNetworkEndpointGroups. attachNetworkEndpoints</code></li>
<li><code>compute. globalNetworkEndpointGroups. create</code></li>
<li><code>compute. globalNetworkEndpointGroups. createTagBinding</code></li>
<li><code>compute. globalNetworkEndpointGroups. delete</code></li>
<li><code>compute. globalNetworkEndpointGroups. deleteTagBinding</code></li>
<li><code>compute. globalNetworkEndpointGroups. detachNetworkEndpoints</code></li>
<li><code>compute. globalNetworkEndpointGroups. get</code></li>
<li><code>compute. globalNetworkEndpointGroups. list</code></li>
<li><code>compute. globalNetworkEndpointGroups. listEffectiveTags</code></li>
<li><code>compute. globalNetworkEndpointGroups. listTagBindings</code></li>
<li><code>compute. globalNetworkEndpointGroups. use</code></li>
</ul>
<p><code>compute.globalOperations.get</code></p>
<p><code>compute. globalOperations. getIamPolicy</code></p>
<p><code>compute.globalOperations.list</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. get</code></p>
<p><code>compute. globalPublicDelegatedPrefixes. list</code></p>
<p><code>compute.healthChecks.get</code></p>
<p><code>compute.healthChecks.list</code></p>
<p><code>compute. healthChecks. listEffectiveTags</code></p>
<p><code>compute. healthChecks. listTagBindings</code></p>
<p><code>compute.hosts.*</code></p>
<ul>
<li><code>compute.hosts.get</code></li>
<li><code>compute.hosts.getVersion</code></li>
<li><code>compute.hosts.list</code></li>
</ul>
<p><code>compute.httpHealthChecks.get</code></p>
<p><code>compute.httpHealthChecks.list</code></p>
<p><code>compute. httpHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpHealthChecks. listTagBindings</code></p>
<p><code>compute.httpsHealthChecks.get</code></p>
<p><code>compute.httpsHealthChecks.list</code></p>
<p><code>compute. httpsHealthChecks. listEffectiveTags</code></p>
<p><code>compute. httpsHealthChecks. listTagBindings</code></p>
<p><code>compute.images.*</code></p>
<ul>
<li><code>compute.images.create</code></li>
<li><code>compute. images. createTagBinding</code></li>
<li><code>compute.images.delete</code></li>
<li><code>compute. images. deleteTagBinding</code></li>
<li><code>compute.images.deprecate</code></li>
<li><code>compute.images.get</code></li>
<li><code>compute.images.getFromFamily</code></li>
<li><code>compute.images.getIamPolicy</code></li>
<li><code>compute.images.list</code></li>
<li><code>compute. images. listEffectiveTags</code></li>
<li><code>compute.images.listTagBindings</code></li>
<li><code>compute.images.setIamPolicy</code></li>
<li><code>compute.images.setLabels</code></li>
<li><code>compute.images.update</code></li>
<li><code>compute.images.useReadOnly</code></li>
</ul>
<p><code>compute. instanceGroupManagers.*</code></p>
<ul>
<li><code>compute. instanceGroupManagers. create</code></li>
<li><code>compute. instanceGroupManagers. createTagBinding</code></li>
<li><code>compute. instanceGroupManagers. delete</code></li>
<li><code>compute. instanceGroupManagers. deleteTagBinding</code></li>
<li><code>compute. instanceGroupManagers. get</code></li>
<li><code>compute. instanceGroupManagers. list</code></li>
<li><code>compute. instanceGroupManagers. listEffectiveTags</code></li>
<li><code>compute. instanceGroupManagers. listTagBindings</code></li>
<li><code>compute. instanceGroupManagers. update</code></li>
<li><code>compute. instanceGroupManagers. use</code></li>
</ul>
<p><code>compute.instanceGroups.*</code></p>
<ul>
<li><code>compute.instanceGroups.create</code></li>
<li><code>compute. instanceGroups. createTagBinding</code></li>
<li><code>compute.instanceGroups.delete</code></li>
<li><code>compute. instanceGroups. deleteTagBinding</code></li>
<li><code>compute.instanceGroups.get</code></li>
<li><code>compute.instanceGroups.list</code></li>
<li><code>compute. instanceGroups. listEffectiveTags</code></li>
<li><code>compute. instanceGroups. listTagBindings</code></li>
<li><code>compute.instanceGroups.update</code></li>
<li><code>compute.instanceGroups.use</code></li>
</ul>
<p><code>compute.instanceSettings.*</code></p>
<ul>
<li><code>compute.instanceSettings.get</code></li>
<li><code>compute. instanceSettings. update</code></li>
</ul>
<p><code>compute.instanceTemplates.*</code></p>
<ul>
<li><code>compute. instanceTemplates. create</code></li>
<li><code>compute. instanceTemplates. delete</code></li>
<li><code>compute.instanceTemplates.get</code></li>
<li><code>compute. instanceTemplates. getIamPolicy</code></li>
<li><code>compute.instanceTemplates.list</code></li>
<li><code>compute. instanceTemplates. setIamPolicy</code></li>
<li><code>compute. instanceTemplates. useReadOnly</code></li>
</ul>
<p><code>compute.instances.*</code></p>
<ul>
<li><code>compute. instances. addAccessConfig</code></li>
<li><code>compute. instances. addNetworkInterface</code></li>
<li><code>compute. instances. addResourcePolicies</code></li>
<li><code>compute.instances.attachDisk</code></li>
<li><code>compute.instances.create</code></li>
<li><code>compute. instances. createTagBinding</code></li>
<li><code>compute.instances.delete</code></li>
<li><code>compute. instances. deleteAccessConfig</code></li>
<li><code>compute. instances. deleteNetworkInterface</code></li>
<li><code>compute. instances. deleteTagBinding</code></li>
<li><code>compute.instances.detachDisk</code></li>
<li><code>compute.instances.get</code></li>
<li><code>compute. instances. getEffectiveFirewalls</code></li>
<li><code>compute. instances. getGuestAttributes</code></li>
<li><code>compute.instances.getIamPolicy</code></li>
<li><code>compute. instances. getScreenshot</code></li>
<li><code>compute. instances. getSerialPortOutput</code></li>
<li><code>compute. instances. getShieldedInstanceIdentity</code></li>
<li><code>compute. instances. getShieldedVmIdentity</code></li>
<li><code>compute. instances. getVmExtensionState</code></li>
<li><code>compute.instances.list</code></li>
<li><code>compute. instances. listEffectiveTags</code></li>
<li><code>compute. instances. listReferrers</code></li>
<li><code>compute. instances. listTagBindings</code></li>
<li><code>compute. instances. listVmExtensionStates</code></li>
<li><code>compute.instances.osAdminLogin</code></li>
<li><code>compute.instances.osLogin</code></li>
<li><code>compute. instances. pscInterfaceCreate</code></li>
<li><code>compute. instances. removeResourcePolicies</code></li>
<li><code>compute.instances.reset</code></li>
<li><code>compute.instances.resume</code></li>
<li><code>compute. instances. sendDiagnosticInterrupt</code></li>
<li><code>compute. instances. setDeletionProtection</code></li>
<li><code>compute. instances. setDiskAutoDelete</code></li>
<li><code>compute.instances.setIamPolicy</code></li>
<li><code>compute.instances.setLabels</code></li>
<li><code>compute. instances. setMachineResources</code></li>
<li><code>compute. instances. setMachineType</code></li>
<li><code>compute.instances.setMetadata</code></li>
<li><code>compute. instances. setMinCpuPlatform</code></li>
<li><code>compute.instances.setName</code></li>
<li><code>compute. instances. setScheduling</code></li>
<li><code>compute. instances. setSecurityPolicy</code></li>
<li><code>compute. instances. setServiceAccount</code></li>
<li><code>compute. instances. setShieldedInstanceIntegrityPolicy</code></li>
<li><code>compute. instances. setShieldedVmIntegrityPolicy</code></li>
<li><code>compute.instances.setTags</code></li>
<li><code>compute. instances. simulateMaintenanceEvent</code></li>
<li><code>compute.instances.start</code></li>
<li><code>compute. instances. startWithEncryptionKey</code></li>
<li><code>compute.instances.stop</code></li>
<li><code>compute.instances.suspend</code></li>
<li><code>compute.instances.troubleshoot</code></li>
<li><code>compute.instances.update</code></li>
<li><code>compute. instances. updateAccessConfig</code></li>
<li><code>compute. instances. updateDisplayDevice</code></li>
<li><code>compute. instances. updateNetworkInterface</code></li>
<li><code>compute. instances. updateSecurity</code></li>
<li><code>compute. instances. updateShieldedInstanceConfig</code></li>
<li><code>compute. instances. updateShieldedVmConfig</code></li>
<li><code>compute.instances.use</code></li>
<li><code>compute.instances.useReadOnly</code></li>
</ul>
<p><code>compute. instantSnapshotGroups.*</code></p>
<ul>
<li><code>compute. instantSnapshotGroups. create</code></li>
<li><code>compute. instantSnapshotGroups. delete</code></li>
<li><code>compute. instantSnapshotGroups. get</code></li>
<li><code>compute. instantSnapshotGroups. getIamPolicy</code></li>
<li><code>compute. instantSnapshotGroups. list</code></li>
<li><code>compute. instantSnapshotGroups. setIamPolicy</code></li>
<li><code>compute. instantSnapshotGroups. useReadOnly</code></li>
</ul>
<p><code>compute. instantSnapshots. create</code></p>
<p><code>compute. instantSnapshots. delete</code></p>
<p><code>compute. instantSnapshots. export</code></p>
<p><code>compute.instantSnapshots.get</code></p>
<p><code>compute. instantSnapshots. getIamPolicy</code></p>
<p><code>compute.instantSnapshots.list</code></p>
<p><code>compute. instantSnapshots. listEffectiveTags</code></p>
<p><code>compute. instantSnapshots. listTagBindings</code></p>
<p><code>compute. instantSnapshots. setIamPolicy</code></p>
<p><code>compute. instantSnapshots. setLabels</code></p>
<p><code>compute. instantSnapshots. useReadOnly</code></p>
<p><code>compute. interconnectAttachmentGroups. get</code></p>
<p><code>compute. interconnectAttachmentGroups. list</code></p>
<p><code>compute. interconnectAttachments. get</code></p>
<p><code>compute. interconnectAttachments. list</code></p>
<p><code>compute. interconnectAttachments. listEffectiveTags</code></p>
<p><code>compute. interconnectAttachments. listTagBindings</code></p>
<p><code>compute.interconnectGroups.get</code></p>
<p><code>compute. interconnectGroups. list</code></p>
<p><code>compute. interconnectLocations.*</code></p>
<ul>
<li><code>compute. interconnectLocations. get</code></li>
<li><code>compute. interconnectLocations. list</code></li>
</ul>
<p><code>compute. interconnectRemoteLocations.*</code></p>
<ul>
<li><code>compute. interconnectRemoteLocations. get</code></li>
<li><code>compute. interconnectRemoteLocations. list</code></li>
</ul>
<p><code>compute.interconnects.get</code></p>
<p><code>compute.interconnects.list</code></p>
<p><code>compute. interconnects. listEffectiveTags</code></p>
<p><code>compute. interconnects. listTagBindings</code></p>
<p><code>compute.licenseCodes.*</code></p>
<ul>
<li><code>compute.licenseCodes.get</code></li>
<li><code>compute. licenseCodes. getIamPolicy</code></li>
<li><code>compute.licenseCodes.list</code></li>
<li><code>compute. licenseCodes. setIamPolicy</code></li>
</ul>
<p><code>compute.licenses.create</code></p>
<p><code>compute.licenses.delete</code></p>
<p><code>compute.licenses.get</code></p>
<p><code>compute.licenses.getIamPolicy</code></p>
<p><code>compute.licenses.list</code></p>
<p><code>compute. licenses. listEffectiveTags</code></p>
<p><code>compute. licenses. listTagBindings</code></p>
<p><code>compute.licenses.setIamPolicy</code></p>
<p><code>compute.licenses.update</code></p>
<p><code>compute.machineImages.create</code></p>
<p><code>compute.machineImages.delete</code></p>
<p><code>compute.machineImages.get</code></p>
<p><code>compute. machineImages. getIamPolicy</code></p>
<p><code>compute.machineImages.list</code></p>
<p><code>compute. machineImages. listEffectiveTags</code></p>
<p><code>compute. machineImages. listTagBindings</code></p>
<p><code>compute. machineImages. setIamPolicy</code></p>
<p><code>compute. machineImages. setLabels</code></p>
<p><code>compute. machineImages. useReadOnly</code></p>
<p><code>compute.machineTypes.*</code></p>
<ul>
<li><code>compute.machineTypes.get</code></li>
<li><code>compute.machineTypes.list</code></li>
</ul>
<p><code>compute.managedRulesets.*</code></p>
<ul>
<li><code>compute.managedRulesets.get</code></li>
<li><code>compute.managedRulesets.list</code></li>
</ul>
<p><code>compute.multiMig.*</code></p>
<ul>
<li><code>compute.multiMig.create</code></li>
<li><code>compute.multiMig.delete</code></li>
<li><code>compute.multiMig.get</code></li>
<li><code>compute.multiMig.list</code></li>
</ul>
<p><code>compute.multiMigMembers.*</code></p>
<ul>
<li><code>compute.multiMigMembers.get</code></li>
<li><code>compute.multiMigMembers.list</code></li>
</ul>
<p><code>compute.networkAttachments.get</code></p>
<p><code>compute. networkAttachments. getIamPolicy</code></p>
<p><code>compute. networkAttachments. list</code></p>
<p><code>compute. networkAttachments. listEffectiveTags</code></p>
<p><code>compute. networkAttachments. listTagBindings</code></p>
<p><code>compute. networkEdgeSecurityServices. get</code></p>
<p><code>compute. networkEdgeSecurityServices. list</code></p>
<p><code>compute. networkEdgeSecurityServices. listEffectiveTags</code></p>
<p><code>compute. networkEdgeSecurityServices. listTagBindings</code></p>
<p><code>compute. networkEndpointGroups.*</code></p>
<ul>
<li><code>compute. networkEndpointGroups. attachNetworkEndpoints</code></li>
<li><code>compute. networkEndpointGroups. create</code></li>
<li><code>compute. networkEndpointGroups. createTagBinding</code></li>
<li><code>compute. networkEndpointGroups. delete</code></li>
<li><code>compute. networkEndpointGroups. deleteTagBinding</code></li>
<li><code>compute. networkEndpointGroups. detachNetworkEndpoints</code></li>
<li><code>compute. networkEndpointGroups. get</code></li>
<li><code>compute. networkEndpointGroups. list</code></li>
<li><code>compute. networkEndpointGroups. listEffectiveTags</code></li>
<li><code>compute. networkEndpointGroups. listTagBindings</code></li>
<li><code>compute. networkEndpointGroups. use</code></li>
</ul>
<p><code>compute.networkProfiles.*</code></p>
<ul>
<li><code>compute.networkProfiles.get</code></li>
<li><code>compute.networkProfiles.list</code></li>
</ul>
<p><code>compute.networks.get</code></p>
<p><code>compute. networks. getEffectiveFirewalls</code></p>
<p><code>compute. networks. getRegionEffectiveFirewalls</code></p>
<p><code>compute.networks.list</code></p>
<p><code>compute. networks. listEffectiveTags</code></p>
<p><code>compute. networks. listPeeringRoutes</code></p>
<p><code>compute. networks. listTagBindings</code></p>
<p><code>compute.networks.use</code></p>
<p><code>compute.networks.useExternalIp</code></p>
<p><code>compute.nodeGroups.get</code></p>
<p><code>compute. nodeGroups. getIamPolicy</code></p>
<p><code>compute.nodeGroups.list</code></p>
<p><code>compute.nodeTemplates.get</code></p>
<p><code>compute. nodeTemplates. getIamPolicy</code></p>
<p><code>compute.nodeTemplates.list</code></p>
<p><code>compute.nodeTypes.*</code></p>
<ul>
<li><code>compute.nodeTypes.get</code></li>
<li><code>compute.nodeTypes.list</code></li>
</ul>
<p><code>compute.orgRolloutPlans.get</code></p>
<p><code>compute.orgRolloutPlans.list</code></p>
<p><code>compute.orgRollouts.get</code></p>
<p><code>compute.orgRollouts.list</code></p>
<p><code>compute. organizations. listAssociations</code></p>
<p><code>compute.packetMirrorings.get</code></p>
<p><code>compute.packetMirrorings.list</code></p>
<p><code>compute. packetMirrorings. listEffectiveTags</code></p>
<p><code>compute. packetMirrorings. listTagBindings</code></p>
<p><code>compute.previewFeatures.get</code></p>
<p><code>compute.previewFeatures.list</code></p>
<p><code>compute.projects.get</code></p>
<p><code>compute. projects. setCommonInstanceMetadata</code></p>
<p><code>compute. publicAdvertisedPrefixes. get</code></p>
<p><code>compute. publicAdvertisedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. get</code></p>
<p><code>compute. publicDelegatedPrefixes. list</code></p>
<p><code>compute. publicDelegatedPrefixes. listEffectiveTags</code></p>
<p><code>compute. publicDelegatedPrefixes. listTagBindings</code></p>
<p><code>compute.recoverableSnapshots.*</code></p>
<ul>
<li><code>compute. recoverableSnapshots. delete</code></li>
<li><code>compute. recoverableSnapshots. get</code></li>
<li><code>compute. recoverableSnapshots. getIamPolicy</code></li>
<li><code>compute. recoverableSnapshots. list</code></li>
<li><code>compute. recoverableSnapshots. recover</code></li>
<li><code>compute. recoverableSnapshots. setIamPolicy</code></li>
</ul>
<p><code>compute. regionBackendBuckets. get</code></p>
<p><code>compute. regionBackendBuckets. getIamPolicy</code></p>
<p><code>compute. regionBackendBuckets. list</code></p>
<p><code>compute. regionBackendBuckets. listEffectiveTags</code></p>
<p><code>compute. regionBackendBuckets. listTagBindings</code></p>
<p><code>compute. regionBackendServices. get</code></p>
<p><code>compute. regionBackendServices. getIamPolicy</code></p>
<p><code>compute. regionBackendServices. list</code></p>
<p><code>compute. regionBackendServices. listEffectiveTags</code></p>
<p><code>compute. regionBackendServices. listTagBindings</code></p>
<p><code>compute. regionCompositeHealthChecks. get</code></p>
<p><code>compute. regionCompositeHealthChecks. list</code></p>
<p><code>compute. regionFirewallPolicies. get</code></p>
<p><code>compute. regionFirewallPolicies. getIamPolicy</code></p>
<p><code>compute. regionFirewallPolicies. list</code></p>
<p><code>compute. regionFirewallPolicies. listEffectiveTags</code></p>
<p><code>compute. regionFirewallPolicies. listTagBindings</code></p>
<p><code>compute. regionHealthAggregationPolicies. get</code></p>
<p><code>compute. regionHealthAggregationPolicies. list</code></p>
<p><code>compute. regionHealthCheckServices. get</code></p>
<p><code>compute. regionHealthCheckServices. list</code></p>
<p><code>compute.regionHealthChecks.get</code></p>
<p><code>compute. regionHealthChecks. list</code></p>
<p><code>compute. regionHealthChecks. listEffectiveTags</code></p>
<p><code>compute. regionHealthChecks. listTagBindings</code></p>
<p><code>compute. regionHealthSources. get</code></p>
<p><code>compute. regionHealthSources. list</code></p>
<p><code>compute. regionNetworkEndpointGroups.*</code></p>
<ul>
<li><code>compute. regionNetworkEndpointGroups. attachNetworkEndpoints</code></li>
<li><code>compute. regionNetworkEndpointGroups. create</code></li>
<li><code>compute. regionNetworkEndpointGroups. createTagBinding</code></li>
<li><code>compute. regionNetworkEndpointGroups. delete</code></li>
<li><code>compute. regionNetworkEndpointGroups. deleteTagBinding</code></li>
<li><code>compute. regionNetworkEndpointGroups. detachNetworkEndpoints</code></li>
<li><code>compute. regionNetworkEndpointGroups. get</code></li>
<li><code>compute. regionNetworkEndpointGroups. list</code></li>
<li><code>compute. regionNetworkEndpointGroups. listEffectiveTags</code></li>
<li><code>compute. regionNetworkEndpointGroups. listTagBindings</code></li>
<li><code>compute. regionNetworkEndpointGroups. use</code></li>
</ul>
<p><code>compute. regionNetworkPolicies. get</code></p>
<p><code>compute. regionNetworkPolicies. list</code></p>
<p><code>compute. regionNotificationEndpoints. get</code></p>
<p><code>compute. regionNotificationEndpoints. list</code></p>
<p><code>compute.regionOperations.get</code></p>
<p><code>compute. regionOperations. getIamPolicy</code></p>
<p><code>compute.regionOperations.list</code></p>
<p><code>compute. regionSecurityPolicies. get</code></p>
<p><code>compute. regionSecurityPolicies. list</code></p>
<p><code>compute. regionSecurityPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSecurityPolicies. listTagBindings</code></p>
<p><code>compute. regionSslCertificates. get</code></p>
<p><code>compute. regionSslCertificates. list</code></p>
<p><code>compute. regionSslCertificates. listEffectiveTags</code></p>
<p><code>compute. regionSslCertificates. listTagBindings</code></p>
<p><code>compute.regionSslPolicies.get</code></p>
<p><code>compute. regionSslPolicies. getIamPolicy</code></p>
<p><code>compute.regionSslPolicies.list</code></p>
<p><code>compute. regionSslPolicies. listAvailableFeatures</code></p>
<p><code>compute. regionSslPolicies. listEffectiveTags</code></p>
<p><code>compute. regionSslPolicies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpProxies. get</code></p>
<p><code>compute. regionTargetHttpProxies. list</code></p>
<p><code>compute. regionTargetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpProxies. listTagBindings</code></p>
<p><code>compute. regionTargetHttpsProxies. get</code></p>
<p><code>compute. regionTargetHttpsProxies. list</code></p>
<p><code>compute. regionTargetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetHttpsProxies. listTagBindings</code></p>
<p><code>compute. regionTargetTcpProxies. get</code></p>
<p><code>compute. regionTargetTcpProxies. list</code></p>
<p><code>compute. regionTargetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. regionTargetTcpProxies. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.get</code></p>
<p><code>compute.regionUrlMaps.list</code></p>
<p><code>compute. regionUrlMaps. listEffectiveTags</code></p>
<p><code>compute. regionUrlMaps. listTagBindings</code></p>
<p><code>compute.regionUrlMaps.validate</code></p>
<p><code>compute.regions.*</code></p>
<ul>
<li><code>compute.regions.get</code></li>
<li><code>compute.regions.list</code></li>
</ul>
<p><code>compute.reliabilityRisks.*</code></p>
<ul>
<li><code>compute.reliabilityRisks.get</code></li>
<li><code>compute.reliabilityRisks.list</code></li>
</ul>
<p><code>compute.reservationBlocks.get</code></p>
<p><code>compute.reservationBlocks.list</code></p>
<p><code>compute. reservationConsumedInstances. list</code></p>
<p><code>compute.reservationSlots.*</code></p>
<ul>
<li><code>compute.reservationSlots.get</code></li>
<li><code>compute.reservationSlots.list</code></li>
<li><code>compute. reservationSlots. update</code></li>
</ul>
<p><code>compute. reservationSubBlocks. get</code></p>
<p><code>compute. reservationSubBlocks. list</code></p>
<p><code>compute.reservations.get</code></p>
<p><code>compute.reservations.list</code></p>
<p><code>compute. reservations. listEffectiveTags</code></p>
<p><code>compute. reservations. listTagBindings</code></p>
<p><code>compute.resourcePolicies.*</code></p>
<ul>
<li><code>compute. resourcePolicies. create</code></li>
<li><code>compute. resourcePolicies. delete</code></li>
<li><code>compute.resourcePolicies.get</code></li>
<li><code>compute. resourcePolicies. getIamPolicy</code></li>
<li><code>compute.resourcePolicies.list</code></li>
<li><code>compute. resourcePolicies. setIamPolicy</code></li>
<li><code>compute. resourcePolicies. update</code></li>
<li><code>compute.resourcePolicies.use</code></li>
<li><code>compute. resourcePolicies. useReadOnly</code></li>
</ul>
<p><code>compute.rolloutPlans.get</code></p>
<p><code>compute.rolloutPlans.list</code></p>
<p><code>compute.rollouts.get</code></p>
<p><code>compute.rollouts.list</code></p>
<p><code>compute.routers.get</code></p>
<p><code>compute.routers.getRoutePolicy</code></p>
<p><code>compute.routers.list</code></p>
<p><code>compute.routers.listBgpRoutes</code></p>
<p><code>compute. routers. listEffectiveTags</code></p>
<p><code>compute. routers. listRoutePolicies</code></p>
<p><code>compute. routers. listTagBindings</code></p>
<p><code>compute.routes.get</code></p>
<p><code>compute.routes.list</code></p>
<p><code>compute. routes. listEffectiveTags</code></p>
<p><code>compute.routes.listTagBindings</code></p>
<p><code>compute.securityPolicies.get</code></p>
<p><code>compute.securityPolicies.list</code></p>
<p><code>compute. securityPolicies. listEffectiveTags</code></p>
<p><code>compute. securityPolicies. listTagBindings</code></p>
<p><code>compute.serviceAttachments.get</code></p>
<p><code>compute. serviceAttachments. getIamPolicy</code></p>
<p><code>compute. serviceAttachments. list</code></p>
<p><code>compute. serviceAttachments. listEffectiveTags</code></p>
<p><code>compute. serviceAttachments. listTagBindings</code></p>
<p><code>compute.snapshotGroups.*</code></p>
<ul>
<li><code>compute.snapshotGroups.create</code></li>
<li><code>compute.snapshotGroups.delete</code></li>
<li><code>compute.snapshotGroups.get</code></li>
<li><code>compute. snapshotGroups. getIamPolicy</code></li>
<li><code>compute.snapshotGroups.list</code></li>
<li><code>compute. snapshotGroups. setIamPolicy</code></li>
<li><code>compute. snapshotGroups. useReadOnly</code></li>
</ul>
<p><code>compute. snapshotRecycleBinPolicy. get</code></p>
<p><code>compute.snapshotSettings.get</code></p>
<p><code>compute.snapshots.*</code></p>
<ul>
<li><code>compute.snapshots.create</code></li>
<li><code>compute. snapshots. createTagBinding</code></li>
<li><code>compute.snapshots.delete</code></li>
<li><code>compute. snapshots. deleteTagBinding</code></li>
<li><code>compute.snapshots.get</code></li>
<li><code>compute. snapshots. getEffectiveRecycleBinRule</code></li>
<li><code>compute.snapshots.getIamPolicy</code></li>
<li><code>compute.snapshots.list</code></li>
<li><code>compute. snapshots. listEffectiveTags</code></li>
<li><code>compute. snapshots. listTagBindings</code></li>
<li><code>compute.snapshots.setIamPolicy</code></li>
<li><code>compute.snapshots.setLabels</code></li>
<li><code>compute.snapshots.updateKmsKey</code></li>
<li><code>compute.snapshots.useReadOnly</code></li>
</ul>
<p><code>compute.spotAssistants.get</code></p>
<p><code>compute.sslCertificates.get</code></p>
<p><code>compute.sslCertificates.list</code></p>
<p><code>compute. sslCertificates. listEffectiveTags</code></p>
<p><code>compute. sslCertificates. listTagBindings</code></p>
<p><code>compute.sslPolicies.get</code></p>
<p><code>compute. sslPolicies. getIamPolicy</code></p>
<p><code>compute.sslPolicies.list</code></p>
<p><code>compute. sslPolicies. listAvailableFeatures</code></p>
<p><code>compute. sslPolicies. listEffectiveTags</code></p>
<p><code>compute. sslPolicies. listTagBindings</code></p>
<p><code>compute.storagePools.get</code></p>
<p><code>compute. storagePools. getIamPolicy</code></p>
<p><code>compute.storagePools.list</code></p>
<p><code>compute. storagePools. listEffectiveTags</code></p>
<p><code>compute. storagePools. listTagBindings</code></p>
<p><code>compute.storagePools.use</code></p>
<p><code>compute.subnetworks.get</code></p>
<p><code>compute. subnetworks. getIamPolicy</code></p>
<p><code>compute.subnetworks.list</code></p>
<p><code>compute. subnetworks. listEffectiveTags</code></p>
<p><code>compute. subnetworks. listTagBindings</code></p>
<p><code>compute.subnetworks.use</code></p>
<p><code>compute. subnetworks. useExternalIp</code></p>
<p><code>compute.targetGrpcProxies.get</code></p>
<p><code>compute.targetGrpcProxies.list</code></p>
<p><code>compute. targetGrpcProxies. listEffectiveTags</code></p>
<p><code>compute. targetGrpcProxies. listTagBindings</code></p>
<p><code>compute.targetHttpProxies.get</code></p>
<p><code>compute.targetHttpProxies.list</code></p>
<p><code>compute. targetHttpProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpProxies. listTagBindings</code></p>
<p><code>compute.targetHttpsProxies.get</code></p>
<p><code>compute. targetHttpsProxies. list</code></p>
<p><code>compute. targetHttpsProxies. listEffectiveTags</code></p>
<p><code>compute. targetHttpsProxies. listTagBindings</code></p>
<p><code>compute.targetInstances.get</code></p>
<p><code>compute.targetInstances.list</code></p>
<p><code>compute. targetInstances. listEffectiveTags</code></p>
<p><code>compute. targetInstances. listTagBindings</code></p>
<p><code>compute.targetPools.get</code></p>
<p><code>compute.targetPools.list</code></p>
<p><code>compute. targetPools. listEffectiveTags</code></p>
<p><code>compute. targetPools. listTagBindings</code></p>
<p><code>compute.targetSslProxies.get</code></p>
<p><code>compute.targetSslProxies.list</code></p>
<p><code>compute. targetSslProxies. listEffectiveTags</code></p>
<p><code>compute. targetSslProxies. listTagBindings</code></p>
<p><code>compute.targetTcpProxies.get</code></p>
<p><code>compute.targetTcpProxies.list</code></p>
<p><code>compute. targetTcpProxies. listEffectiveTags</code></p>
<p><code>compute. targetTcpProxies. listTagBindings</code></p>
<p><code>compute.targetVpnGateways.get</code></p>
<p><code>compute.targetVpnGateways.list</code></p>
<p><code>compute. targetVpnGateways. listEffectiveTags</code></p>
<p><code>compute. targetVpnGateways. listTagBindings</code></p>
<p><code>compute.urlMaps.get</code></p>
<p><code>compute.urlMaps.list</code></p>
<p><code>compute. urlMaps. listEffectiveTags</code></p>
<p><code>compute. urlMaps. listTagBindings</code></p>
<p><code>compute.urlMaps.validate</code></p>
<p><code>compute. vmExtensionPolicies. get</code></p>
<p><code>compute. vmExtensionPolicies. list</code></p>
<p><code>compute.vpnGateways.get</code></p>
<p><code>compute.vpnGateways.list</code></p>
<p><code>compute. vpnGateways. listEffectiveTags</code></p>
<p><code>compute. vpnGateways. listTagBindings</code></p>
<p><code>compute.vpnTunnels.get</code></p>
<p><code>compute.vpnTunnels.list</code></p>
<p><code>compute. vpnTunnels. listEffectiveTags</code></p>
<p><code>compute. vpnTunnels. listTagBindings</code></p>
<p><code>compute.wireGroups.get</code></p>
<p><code>compute.wireGroups.list</code></p>
<p><code>compute.zoneOperations.get</code></p>
<p><code>compute. zoneOperations. getIamPolicy</code></p>
<p><code>compute.zoneOperations.list</code></p>
<p><code>compute.zones.*</code></p>
<ul>
<li><code>compute.zones.get</code></li>
<li><code>compute.zones.list</code></li>
</ul>
<p><code>dataproc.clusters.get</code></p>
<p><code>dataproc.clusters.use</code></p>
<p><code>dataproc.jobs.cancel</code></p>
<p><code>dataproc.jobs.create</code></p>
<p><code>dataproc.jobs.delete</code></p>
<p><code>dataproc.jobs.get</code></p>
<p><code>dataproc.jobs.list</code></p>
<p><code>dataproc.jobs.update</code></p>
<p><code>iam.serviceAccounts.actAs</code></p>
<p><code>iam.serviceAccounts.get</code></p>
<p><code>iam. serviceAccounts. getAccessToken</code></p>
<p><code>iam.serviceAccounts.list</code></p>
<p><code>ml.jobs.create</code></p>
<p><code>ml.jobs.get</code></p>
<p><code>ml.jobs.list</code></p>
<p><code>notebooks.environments.*</code></p>
<ul>
<li><code>notebooks.environments.create</code></li>
<li><code>notebooks.environments.delete</code></li>
<li><code>notebooks.environments.get</code></li>
<li><code>notebooks. environments. getIamPolicy</code></li>
<li><code>notebooks.environments.list</code></li>
<li><code>notebooks. environments. setIamPolicy</code></li>
</ul>
<p><code>notebooks.executions.*</code></p>
<ul>
<li><code>notebooks.executions.create</code></li>
<li><code>notebooks.executions.delete</code></li>
<li><code>notebooks.executions.get</code></li>
<li><code>notebooks. executions. getIamPolicy</code></li>
<li><code>notebooks.executions.list</code></li>
<li><code>notebooks. executions. setIamPolicy</code></li>
</ul>
<p><code>notebooks. instances. checkUpgradability</code></p>
<p><code>notebooks.instances.create</code></p>
<p><code>notebooks.instances.delete</code></p>
<p><code>notebooks.instances.diagnose</code></p>
<p><code>notebooks.instances.get</code></p>
<p><code>notebooks.instances.getHealth</code></p>
<p><code>notebooks. instances. getIamPolicy</code></p>
<p><code>notebooks.instances.list</code></p>
<p><code>notebooks. instances. listEffectiveTags</code></p>
<p><code>notebooks. instances. listTagBindings</code></p>
<p><code>notebooks.instances.reset</code></p>
<p><code>notebooks. instances. setAccelerator</code></p>
<p><code>notebooks. instances. setIamPolicy</code></p>
<p><code>notebooks.instances.setLabels</code></p>
<p><code>notebooks. instances. setMachineType</code></p>
<p><code>notebooks.instances.start</code></p>
<p><code>notebooks.instances.stop</code></p>
<p><code>notebooks.instances.update</code></p>
<p><code>notebooks. instances. updateConfig</code></p>
<p><code>notebooks. instances. updateShieldInstanceConfig</code></p>
<p><code>notebooks.instances.upgrade</code></p>
<p><code>notebooks.instances.use</code></p>
<p><code>notebooks.locations.*</code></p>
<ul>
<li><code>notebooks.locations.get</code></li>
<li><code>notebooks.locations.list</code></li>
</ul>
<p><code>notebooks.operations.*</code></p>
<ul>
<li><code>notebooks.operations.cancel</code></li>
<li><code>notebooks.operations.delete</code></li>
<li><code>notebooks.operations.get</code></li>
<li><code>notebooks.operations.list</code></li>
</ul>
<p><code>notebooks.runtimes.*</code></p>
<ul>
<li><code>notebooks.runtimes.create</code></li>
<li><code>notebooks.runtimes.delete</code></li>
<li><code>notebooks.runtimes.diagnose</code></li>
<li><code>notebooks.runtimes.get</code></li>
<li><code>notebooks. runtimes. getIamPolicy</code></li>
<li><code>notebooks.runtimes.list</code></li>
<li><code>notebooks.runtimes.reset</code></li>
<li><code>notebooks. runtimes. setIamPolicy</code></li>
<li><code>notebooks.runtimes.start</code></li>
<li><code>notebooks.runtimes.stop</code></li>
<li><code>notebooks.runtimes.switch</code></li>
<li><code>notebooks.runtimes.update</code></li>
<li><code>notebooks.runtimes.upgrade</code></li>
</ul>
<p><code>notebooks.schedules.*</code></p>
<ul>
<li><code>notebooks.schedules.create</code></li>
<li><code>notebooks.schedules.delete</code></li>
<li><code>notebooks.schedules.get</code></li>
<li><code>notebooks. schedules. getIamPolicy</code></li>
<li><code>notebooks.schedules.list</code></li>
<li><code>notebooks. schedules. setIamPolicy</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p>
<p><code>serviceusage. consumerpolicy. analyze</code></p>
<p><code>serviceusage. consumerpolicy. get</code></p>
<p><code>serviceusage. effectivepolicy. get</code></p>
<p><code>serviceusage.groups.*</code></p>
<ul>
<li><code>serviceusage.groups.list</code></li>
<li><code>serviceusage. groups. listExpandedMembers</code></li>
<li><code>serviceusage. groups. listMembers</code></li>
</ul>
<p><code>serviceusage.quotas.get</code></p>
<p><code>serviceusage.services.get</code></p>
<p><code>serviceusage.services.list</code></p>
<p><code>serviceusage.values.test</code></p></td>
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
