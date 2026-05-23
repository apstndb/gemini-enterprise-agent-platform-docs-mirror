---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/FunctionDeclaration
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/FunctionDeclaration
title: FunctionDeclaration
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Structured representation of a function declaration as defined by the [OpenAPI 3.0 specification](https://spec.openapis.org/oas/v3.0.3) . Included in this declaration are the function name, description, parameters and response type. This FunctionDeclaration is a representation of a block of code that can be used as a `Tool` by the model and executed by the client.

Fields

`name` `string`

Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots, colons and dashes, with a maximum length of 128.

`description` `string`

Optional. description and purpose of the function. Model uses it to decide how and whether to call the function.

`parameters` ` object ( Schema  ` )

Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1

`parametersJsonSchema` ` value ( Value  ` format)

Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example:

    {
      "type": "object",
      "properties": {
        "name": { "type": "string" },
        "age": { "type": "integer" }
      },
      "additionalProperties": false,
      "required": ["name", "age"],
      "propertyOrdering": ["name", "age"]
    }

This field is mutually exclusive with `parameters` .

`response` ` object ( Schema  ` )

Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function.

`responseJsonSchema` ` value ( Value  ` format)

Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function.

This field is mutually exclusive with `response` .

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;description&quot;: string,&quot;parameters&quot;: {object (Schema)},&quot;parametersJsonSchema&quot;: value,&quot;response&quot;: {object (Schema)},&quot;responseJsonSchema&quot;: value}</code></pre></td>
</tr>
</tbody>
</table>
