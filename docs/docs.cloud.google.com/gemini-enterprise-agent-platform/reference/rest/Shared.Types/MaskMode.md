---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MaskMode
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MaskMode
title: MaskMode
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The mode for generating a mask for the product image if `  ProductImage.mask_image  ` is not provided. A mask is an image that specifies the region of the garment to be worn.

Enums

`MASK_MODE_DEFAULT`

If unspecified, the service uses a default mode for mask generation.

`MASK_MODE_USER_PROVIDED`

Use the mask provided in `  ProductImage.mask_image  ` . No mask generation is performed.

`MASK_MODE_DETECTION_BOX`

Generate a mask from detected bounding boxes in `  ProductImage.image  ` .

`MASK_MODE_CLOTHING_AREA`

Generate a mask by segmenting the clothing area in `  ProductImage.image  ` .

`MASK_MODE_PARSED_PERSON`

Generate a mask by segmenting the person and clothing in `  ProductImage.image  ` .
