---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/audit-logging
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/audit-logging
title: Agent Retrieval audit logging
description: Review the audit logs available for Agent Retrieval.
data_source: docs.cloud.google.com
---

This document lists the audited methods for Vertex Vector Search. Google Cloud services generate audit logs that record administrative and access activities within your Google Cloud resources. For more information about Cloud Audit Logs, see the following:

  - [Types of audit logs](https://docs.cloud.google.com/logging/docs/audit#types)
  - [Audit log entry structure](https://docs.cloud.google.com/logging/docs/audit#audit_log_entry_structure)
  - [Storing and routing audit logs](https://docs.cloud.google.com/logging/docs/audit#storing_and_routing_audit_logs)
  - [Cloud Logging pricing summary](https://docs.cloud.google.com/stackdriver/pricing#logs-pricing-summary)
  - [Enable Data Access audit logs](https://docs.cloud.google.com/logging/docs/audit/configure-data-access)

## Service name

To view the Vertex Vector Search audit logs, do the following:

1.  In the Google Cloud console, go to the Logs Explorer page:

2.  Copy and paste the following query into the **Query** field of the Logs Explorer, and then click **Run query** .
    
    ``` 
        protoPayload.serviceName="vectorsearch.googleapis.com"
      
    ```

## Methods by permission type

Each IAM permission has a `type` property, whose value is an enum that can be one of four values: `ADMIN_READ` , `ADMIN_WRITE` , `DATA_READ` , or `DATA_WRITE` . When you call a method, Vertex Vector Search generates an audit log whose category is dependent on the `type` property of the permission required to perform the method. Methods that require an IAM permission with the `type` property value of `DATA_READ` , `DATA_WRITE` , or `ADMIN_READ` generate [Data Access](https://docs.cloud.google.com/logging/docs/audit#data-access) audit logs. Methods that require an IAM permission with the `type` property value of `ADMIN_WRITE` generate [Admin Activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity) audit logs.

API methods in the following list that are marked with (LRO) are long-running operations (LROs). These methods usually generate two audit log entries: one when the operation starts and another when it ends. For more information see [Audit logs for long-running operations](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Permission type</th>
<th>Methods</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">ADMIN_READ</code></td>
<td><code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.GetCollection</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.GetIndex</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.ListCollections</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.ListIndexes</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.GetCollection</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.GetIndex</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.ListCollections</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.ListIndexes</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.GetCollection</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.GetIndex</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.ListCollections</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.ListIndexes</code><br />
<code dir="ltr" translate="no">google.longrunning.Operations.GetOperation</code><br />
<code dir="ltr" translate="no">google.longrunning.Operations.ListOperations</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ADMIN_WRITE</code></td>
<td><code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.CreateCollection</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.CreateIndex</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.DeleteCollection</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.DeleteIndex</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.UpdateCollection</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.UpdateIndex</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.CreateCollection</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.CreateIndex</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.DeleteCollection</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.DeleteIndex</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.UpdateCollection</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.UpdateIndex</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.CreateCollection</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.CreateIndex</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.DeleteCollection</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.DeleteIndex</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.UpdateCollection</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.UpdateIndex</code> (LRO)<br />
<code dir="ltr" translate="no">google.longrunning.Operations.CancelOperation</code><br />
<code dir="ltr" translate="no">google.longrunning.Operations.DeleteOperation</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">DATA_READ</code></td>
<td><code dir="ltr" translate="no">google.cloud.vectorsearch.v1.DataObjectSearchService.QueryDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.DataObjectSearchService.SearchDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.DataObjectService.GetDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.ExportDataObjects</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.DataObjectService.GetDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.ExportDataObjects</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.DataObjectSearchService.SearchDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.DataObjectService.GetDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.ExportDataObjects</code> (LRO)</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">DATA_WRITE</code></td>
<td><code dir="ltr" translate="no">google.cloud.vectorsearch.v1.DataObjectService.BatchCreateDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.DataObjectService.BatchDeleteDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.DataObjectService.BatchUpdateDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.DataObjectService.CreateDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.DataObjectService.DeleteDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.DataObjectService.UpdateDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1.VectorSearchService.ImportDataObjects</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.DataObjectService.BatchCreateDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.DataObjectService.BatchDeleteDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.DataObjectService.BatchUpdateDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.DataObjectService.CreateDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.DataObjectService.DeleteDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.DataObjectService.UpdateDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1alpha.VectorSearchService.ImportDataObjects</code> (LRO)<br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.DataObjectService.BatchCreateDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.DataObjectService.BatchDeleteDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.DataObjectService.BatchUpdateDataObjects</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.DataObjectService.CreateDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.DataObjectService.DeleteDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.DataObjectService.UpdateDataObject</code><br />
<code dir="ltr" translate="no">google.cloud.vectorsearch.v1beta.VectorSearchService.ImportDataObjects</code> (LRO)</td>
</tr>
</tbody>
</table>

## API interface audit logs

For information about how and which permissions are evaluated for each method, see the Identity and Access Management documentation for Vertex Vector Search.

### `google.cloud.vectorsearch.v1.DataObjectSearchService`

The following audit logs are associated with methods belonging to `google.cloud.vectorsearch.v1.DataObjectSearchService` .

#### `QueryDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1.DataObjectSearchService.QueryDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.query - DATA_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.DataObjectSearchService.QueryDataObjects"`  

#### `SearchDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1.DataObjectSearchService.SearchDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.search - DATA_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.DataObjectSearchService.SearchDataObjects"`  

### `google.cloud.vectorsearch.v1.DataObjectService`

The following audit logs are associated with methods belonging to `google.cloud.vectorsearch.v1.DataObjectService` .

#### `BatchCreateDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1.DataObjectService.BatchCreateDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.create - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.DataObjectService.BatchCreateDataObjects"`  

#### `BatchDeleteDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1.DataObjectService.BatchDeleteDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.delete - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.DataObjectService.BatchDeleteDataObjects"`  

#### `BatchUpdateDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1.DataObjectService.BatchUpdateDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.update - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.DataObjectService.BatchUpdateDataObjects"`  

#### `CreateDataObject`

  - **Method** : `google.cloud.vectorsearch.v1.DataObjectService.CreateDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.create - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.DataObjectService.CreateDataObject"`  

#### `DeleteDataObject`

  - **Method** : `google.cloud.vectorsearch.v1.DataObjectService.DeleteDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.delete - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.DataObjectService.DeleteDataObject"`  

#### `GetDataObject`

  - **Method** : `google.cloud.vectorsearch.v1.DataObjectService.GetDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.get - DATA_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.DataObjectService.GetDataObject"`  

#### `UpdateDataObject`

  - **Method** : `google.cloud.vectorsearch.v1.DataObjectService.UpdateDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.update - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.DataObjectService.UpdateDataObject"`  

### `google.cloud.vectorsearch.v1.VectorSearchService`

The following audit logs are associated with methods belonging to `google.cloud.vectorsearch.v1.VectorSearchService` .

#### `CreateCollection`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.CreateCollection`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.collections.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.CreateCollection"`  

#### `CreateIndex`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.CreateIndex`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.CreateIndex"`  

#### `DeleteCollection`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.DeleteCollection`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.DeleteCollection"`  

#### `DeleteIndex`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.DeleteIndex`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.DeleteIndex"`  

#### `ExportDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.ExportDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.export - DATA_READ`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.ExportDataObjects"`  

#### `GetCollection`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.GetCollection`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.collections.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.GetCollection"`  

#### `GetIndex`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.GetIndex`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.indexes.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.GetIndex"`  

#### `ImportDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.ImportDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.import - DATA_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.ImportDataObjects"`  

#### `ListCollections`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.ListCollections`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.collections.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.ListCollections"`  

#### `ListIndexes`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.ListIndexes`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.indexes.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.ListIndexes"`  

#### `UpdateCollection`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.UpdateCollection`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.collections.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.UpdateCollection"`  

#### `UpdateIndex`

  - **Method** : `google.cloud.vectorsearch.v1.VectorSearchService.UpdateIndex`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1.VectorSearchService.UpdateIndex"`  

### `google.cloud.vectorsearch.v1alpha.DataObjectService`

The following audit logs are associated with methods belonging to `google.cloud.vectorsearch.v1alpha.DataObjectService` .

#### `BatchCreateDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1alpha.DataObjectService.BatchCreateDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.create - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.DataObjectService.BatchCreateDataObjects"`  

#### `BatchDeleteDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1alpha.DataObjectService.BatchDeleteDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.delete - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.DataObjectService.BatchDeleteDataObjects"`  

#### `BatchUpdateDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1alpha.DataObjectService.BatchUpdateDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.update - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.DataObjectService.BatchUpdateDataObjects"`  

#### `CreateDataObject`

  - **Method** : `google.cloud.vectorsearch.v1alpha.DataObjectService.CreateDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.create - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.DataObjectService.CreateDataObject"`  

#### `DeleteDataObject`

  - **Method** : `google.cloud.vectorsearch.v1alpha.DataObjectService.DeleteDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.delete - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.DataObjectService.DeleteDataObject"`  

#### `GetDataObject`

  - **Method** : `google.cloud.vectorsearch.v1alpha.DataObjectService.GetDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.get - DATA_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.DataObjectService.GetDataObject"`  

#### `UpdateDataObject`

  - **Method** : `google.cloud.vectorsearch.v1alpha.DataObjectService.UpdateDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.update - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.DataObjectService.UpdateDataObject"`  

### `google.cloud.vectorsearch.v1alpha.VectorSearchService`

The following audit logs are associated with methods belonging to `google.cloud.vectorsearch.v1alpha.VectorSearchService` .

#### `CreateCollection`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.CreateCollection`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.collections.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.CreateCollection"`  

#### `CreateIndex`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.CreateIndex`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.CreateIndex"`  

#### `DeleteCollection`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.DeleteCollection`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.DeleteCollection"`  

#### `DeleteIndex`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.DeleteIndex`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.DeleteIndex"`  

#### `ExportDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.ExportDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.export - DATA_READ`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.ExportDataObjects"`  

#### `GetCollection`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.GetCollection`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.collections.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.GetCollection"`  

#### `GetIndex`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.GetIndex`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.indexes.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.GetIndex"`  

#### `ImportDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.ImportDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.import - DATA_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.ImportDataObjects"`  

#### `ListCollections`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.ListCollections`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.collections.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.ListCollections"`  

#### `ListIndexes`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.ListIndexes`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.indexes.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.ListIndexes"`  

#### `UpdateCollection`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.UpdateCollection`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.collections.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.UpdateCollection"`  

#### `UpdateIndex`

  - **Method** : `google.cloud.vectorsearch.v1alpha.VectorSearchService.UpdateIndex`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1alpha.VectorSearchService.UpdateIndex"`  

### `google.cloud.vectorsearch.v1beta.DataObjectSearchService`

The following audit logs are associated with methods belonging to `google.cloud.vectorsearch.v1beta.DataObjectSearchService` .

#### `SearchDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1beta.DataObjectSearchService.SearchDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.search - DATA_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.DataObjectSearchService.SearchDataObjects"`  

### `google.cloud.vectorsearch.v1beta.DataObjectService`

The following audit logs are associated with methods belonging to `google.cloud.vectorsearch.v1beta.DataObjectService` .

#### `BatchCreateDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1beta.DataObjectService.BatchCreateDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.create - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.DataObjectService.BatchCreateDataObjects"`  

#### `BatchDeleteDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1beta.DataObjectService.BatchDeleteDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.delete - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.DataObjectService.BatchDeleteDataObjects"`  

#### `BatchUpdateDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1beta.DataObjectService.BatchUpdateDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.update - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.DataObjectService.BatchUpdateDataObjects"`  

#### `CreateDataObject`

  - **Method** : `google.cloud.vectorsearch.v1beta.DataObjectService.CreateDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.create - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.DataObjectService.CreateDataObject"`  

#### `DeleteDataObject`

  - **Method** : `google.cloud.vectorsearch.v1beta.DataObjectService.DeleteDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.delete - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.DataObjectService.DeleteDataObject"`  

#### `GetDataObject`

  - **Method** : `google.cloud.vectorsearch.v1beta.DataObjectService.GetDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.get - DATA_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.DataObjectService.GetDataObject"`  

#### `UpdateDataObject`

  - **Method** : `google.cloud.vectorsearch.v1beta.DataObjectService.UpdateDataObject`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.update - DATA_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.DataObjectService.UpdateDataObject"`  

### `google.cloud.vectorsearch.v1beta.VectorSearchService`

The following audit logs are associated with methods belonging to `google.cloud.vectorsearch.v1beta.VectorSearchService` .

#### `CreateCollection`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.CreateCollection`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.collections.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.CreateCollection"`  

#### `CreateIndex`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.CreateIndex`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.CreateIndex"`  

#### `DeleteCollection`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.DeleteCollection`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.dataObjects.delete - DATA_WRITE`
      - `vectorsearch.indexes.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.DeleteCollection"`  

#### `DeleteIndex`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.DeleteIndex`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.DeleteIndex"`  

#### `ExportDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.ExportDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.export - DATA_READ`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.ExportDataObjects"`  

#### `GetCollection`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.GetCollection`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.collections.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.GetCollection"`  

#### `GetIndex`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.GetIndex`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.indexes.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.GetIndex"`  

#### `ImportDataObjects`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.ImportDataObjects`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.dataObjects.import - DATA_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.ImportDataObjects"`  

#### `ListCollections`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.ListCollections`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.collections.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.ListCollections"`  

#### `ListIndexes`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.ListIndexes`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.indexes.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.ListIndexes"`  

#### `UpdateCollection`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.UpdateCollection`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.collections.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.UpdateCollection"`  

#### `UpdateIndex`

  - **Method** : `google.cloud.vectorsearch.v1beta.VectorSearchService.UpdateIndex`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.indexes.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Long-running operation**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.vectorsearch.v1beta.VectorSearchService.UpdateIndex"`  

### `google.longrunning.Operations`

The following audit logs are associated with methods belonging to `google.longrunning.Operations` .

#### `CancelOperation`

  - **Method** : `google.longrunning.Operations.CancelOperation`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.operations.cancel - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.CancelOperation"`  

#### `DeleteOperation`

  - **Method** : `google.longrunning.Operations.DeleteOperation`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `vectorsearch.operations.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.DeleteOperation"`  

#### `GetOperation`

  - **Method** : `google.longrunning.Operations.GetOperation`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.operations.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.GetOperation"`  

#### `ListOperations`

  - **Method** : `google.longrunning.Operations.ListOperations`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `vectorsearch.operations.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.longrunning.Operations.ListOperations"`  

## Methods that don't produce audit logs

A method might not produce audit logs for one or more of the following reasons:

  - It is a high volume method involving significant log generation and storage costs.
  - It has low auditing value.
  - Another audit or platform log already provides method coverage.

The following methods don't produce audit logs:

  - `google.cloud.location.Locations.GetLocation`
  - `google.cloud.location.Locations.ListLocations`
  - `google.longrunning.Operations.WaitOperation`
