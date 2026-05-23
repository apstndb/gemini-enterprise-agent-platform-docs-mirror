---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RecordErrorType
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RecordErrorType
title: RecordErrorType
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Enums

`ERROR_TYPE_UNSPECIFIED`

Default, shall not be used.

`EMPTY_LINE`

The record is empty.

`INVALID_JSON_SYNTAX`

Invalid json format.

`INVALID_CSV_SYNTAX`

Invalid csv format.

`INVALID_AVRO_SYNTAX`

Invalid avro format.

`INVALID_EMBEDDING_ID`

The embedding id is not valid.

`EMBEDDING_SIZE_MISMATCH`

The size of the dense embedding vectors does not match with the specified dimension.

`NAMESPACE_MISSING`

The `namespace` field is missing.

`PARSING_ERROR`

Generic catch-all error. Only used for validation failure where the root cause cannot be easily retrieved programmatically.

`DUPLICATE_NAMESPACE`

There are multiple restricts with the same `namespace` value.

`OP_IN_DATAPOINT`

Numeric restrict has operator specified in datapoint.

`MULTIPLE_VALUES`

Numeric restrict has multiple values specified.

`INVALID_NUMERIC_VALUE`

Numeric restrict has invalid numeric value specified.

`INVALID_ENCODING`

File is not in UTF\_8 format.

`INVALID_SPARSE_DIMENSIONS`

Error parsing sparse dimensions field.

`INVALID_TOKEN_VALUE`

token restrict value is invalid.

`INVALID_SPARSE_EMBEDDING`

Invalid sparse embedding.

`INVALID_EMBEDDING`

Invalid dense embedding.

`INVALID_EMBEDDING_METADATA`

Invalid embedding metadata.

`EMBEDDING_METADATA_EXCEEDS_SIZE_LIMIT`

Embedding metadata exceeds size limit.
