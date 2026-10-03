---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationAnnotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationAnnotation
title: ImageSegmentationAnnotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Annotation details specific to image segmentation.

Fields

`annotation` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`maskAnnotation` `object ( `[`MaskAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationAnnotation#MaskAnnotation)` )`

Mask based segmentation annotation. Only one mask annotation can exist for one image.

`polygonAnnotation` `object ( `[`PolygonAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationAnnotation#PolygonAnnotation)` )`

Polygon annotation.

`polylineAnnotation` `object ( `[`PolylineAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationAnnotation#PolylineAnnotation)` )`

Polyline annotation.

End of mutually exclusive fields.

**JSON representation**

```
{

  // annotation
  "maskAnnotation": {
    object (MaskAnnotation)
  },
  "polygonAnnotation": {
    object (PolygonAnnotation)
  },
  "polylineAnnotation": {
    object (PolylineAnnotation)
  }
  // Union type
}
```

## MaskAnnotation

The mask based segmentation annotation.

Fields

`maskGcsUri` `string`

Google Cloud Storage URI that points to the mask image. The image must be in PNG format. It must have the same size as the DataItem's image. Each pixel in the image mask represents the AnnotationSpec which the pixel in the image DataItem belong to. Each color is mapped to one AnnotationSpec based on annotationSpecColors.

`annotationSpecColors[]` `object ( `[`AnnotationSpecColor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AnnotationSpecColor)` )`

The mapping between color and AnnotationSpec for this Annotation.

**JSON representation**

```
{
  "maskGcsUri": string,
  "annotationSpecColors": [
    {
      object (AnnotationSpecColor)
    }
  ]
}
```

## PolygonAnnotation

Represents a polygon in image.

Fields

`vertexes[]` `object ( `[`Vertex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationAnnotation#Vertex)` )`

The vertexes are connected one by one and the last vertex is connected to the first one to represent a polygon.

`annotationSpecId` `string`

The resource id of the AnnotationSpec that this Annotation pertains to.

`displayName` `string`

The display name of the AnnotationSpec that this Annotation pertains to.

**JSON representation**

```
{
  "vertexes": [
    {
      object (Vertex)
    }
  ],
  "annotationSpecId": string,
  "displayName": string
}
```

## Vertex

Represents a 2D point in the image. Vertex coordinates are normalized to be relative to the original image dimensions and range from 0 to 1. The origin of the coordinate system (0,0) is the top-left corner of the image. x increases to the right, and y increases to the bottom.

Fields

`x` `number`

X coordinate of the vertex, normalized to \[0.0, 1.0\].

`y` `number`

Y coordinate of the vertex, normalized to \[0.0, 1.0\].

**JSON representation**

```
{
  "x": number,
  "y": number
}
```

## PolylineAnnotation

Represents a polyline in image.

Fields

`vertexes[]` `object ( `[`Vertex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationAnnotation#Vertex)` )`

The vertexes are connected one by one and the last vertex in not connected to the first one.

`annotationSpecId` `string`

The resource id of the AnnotationSpec that this Annotation pertains to.

`displayName` `string`

The display name of the AnnotationSpec that this Annotation pertains to.

**JSON representation**

```
{
  "vertexes": [
    {
      object (Vertex)
    }
  ],
  "annotationSpecId": string,
  "displayName": string
}
```
