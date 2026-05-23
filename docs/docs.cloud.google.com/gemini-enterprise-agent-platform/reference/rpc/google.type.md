---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.type
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.type
title: Package google.type
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  Color  ` (message)
  - `  Date  ` (message)
  - `  Expr  ` (message)
  - `  Interval  ` (message)
  - `  LatLng  ` (message)

## Color

Represents a color in the RGBA color space. This representation is designed for simplicity of conversion to and from color representations in various languages over compactness. For example, the fields of this representation can be trivially provided to the constructor of `java.awt.Color` in Java; it can also be trivially provided to UIColor's `+colorWithRed:green:blue:alpha` method in iOS; and, with just a little work, it can be easily formatted into a CSS `rgba()` string in JavaScript.

This reference page doesn't have information about the absolute color space that should be used to interpret the RGB value—for example, sRGB, Adobe RGB, DCI-P3, and BT.2020. By default, applications should assume the sRGB color space.

When color equality needs to be decided, implementations, unless documented otherwise, treat two colors as equal if all their red, green, blue, and alpha values each differ by at most `1e-5` .

Example (Java):

``` 
 import com.google.type.Color;

 // ...
 public static java.awt.Color fromProto(Color protocolor) {
   float alpha = protocolor.hasAlpha()
       ? protocolor.getAlpha().getValue()
       : 1.0;

   return new java.awt.Color(
       protocolor.getRed(),
       protocolor.getGreen(),
       protocolor.getBlue(),
       alpha);
 }

 public static Color toProto(java.awt.Color color) {
   float red = (float) color.getRed();
   float green = (float) color.getGreen();
   float blue = (float) color.getBlue();
   float denominator = 255.0;
   Color.Builder resultBuilder =
       Color
           .newBuilder()
           .setRed(red / denominator)
           .setGreen(green / denominator)
           .setBlue(blue / denominator);
   int alpha = color.getAlpha();
   if (alpha != 255) {
     result.setAlpha(
         FloatValue
             .newBuilder()
             .setValue(((float) alpha) / denominator)
             .build());
   }
   return resultBuilder.build();
 }
 // ...
```

Example (iOS / Obj-C):

``` 
 // ...
 static UIColor* fromProto(Color* protocolor) {
    float red = [protocolor red];
    float green = [protocolor green];
    float blue = [protocolor blue];
    FloatValue* alpha_wrapper = [protocolor alpha];
    float alpha = 1.0;
    if (alpha_wrapper != nil) {
      alpha = [alpha_wrapper value];
    }
    return [UIColor colorWithRed:red green:green blue:blue alpha:alpha];
 }

 static Color* toProto(UIColor* color) {
     CGFloat red, green, blue, alpha;
     if (![color getRed:&red green:&green blue:&blue alpha:&alpha]) {
       return nil;
     }
     Color* result = [[Color alloc] init];
     [result setRed:red];
     [result setGreen:green];
     [result setBlue:blue];
     if (alpha <= 0.9999) {
       [result setAlpha:floatWrapperWithValue(alpha)];
     }
     [result autorelease];
     return result;
}
// ...
```

Example (JavaScript):

    // ...
    
    var protoToCssColor = function(rgb_color) {
       var redFrac = rgb_color.red || 0.0;
       var greenFrac = rgb_color.green || 0.0;
       var blueFrac = rgb_color.blue || 0.0;
       var red = Math.floor(redFrac * 255);
       var green = Math.floor(greenFrac * 255);
       var blue = Math.floor(blueFrac * 255);
    
       if (!('alpha' in rgb_color)) {
          return rgbToCssColor(red, green, blue);
       }
    
       var alphaFrac = rgb_color.alpha.value || 0.0;
       var rgbParams = [red, green, blue].join(',');
       return ['rgba(', rgbParams, ',', alphaFrac, ')'].join('');
    };
    
    var rgbToCssColor = function(red, green, blue) {
      var rgbNumber = new Number((red << 16) | (green << 8) | blue);
      var hexString = rgbNumber.toString(16);
      var missingZeros = 6 - hexString.length;
      var resultBuilder = ['#'];
      for (var i = 0; i < missingZeros; i++) {
         resultBuilder.push('0');
      }
      resultBuilder.push(hexString);
      return resultBuilder.join('');
    };
    
    // ...

Fields

`red`

`float`

The amount of red in the color as a value in the interval \[0, 1\].

`green`

`float`

The amount of green in the color as a value in the interval \[0, 1\].

`blue`

`float`

The amount of blue in the color as a value in the interval \[0, 1\].

`alpha`

`  FloatValue  `

The fraction of this color that should be applied to the pixel. That is, the final pixel color is defined by the equation:

`pixel color = alpha * (this color) + (1.0 - alpha) * (background color)`

This means that a value of 1.0 corresponds to a solid color, whereas a value of 0.0 corresponds to a completely transparent color. This uses a wrapper message rather than a simple float scalar so that it is possible to distinguish between a default value and the value being unset. If omitted, this color object is rendered as a solid color (as if the alpha value had been explicitly given a value of 1.0).

## Date

Represents a whole or partial calendar date, such as a birthday. The time of day and time zone are either specified elsewhere or are insignificant. The date is relative to the Gregorian Calendar. This can represent one of the following:

  - A full date, with non-zero year, month, and day values.
  - A month and day, with a zero year (for example, an anniversary).
  - A year on its own, with a zero month and a zero day.
  - A year and month, with a zero day (for example, a credit card expiration date).

Related types:

  - `google.type.TimeOfDay`
  - `google.type.DateTime`
  - `  google.protobuf.Timestamp  `

Fields

`year`

`int32`

Year of the date. Must be from 1 to 9999, or 0 to specify a date without a year.

`month`

`int32`

Month of a year. Must be from 1 to 12, or 0 to specify a year without a month and day.

`day`

`int32`

Day of a month. Must be from 1 to 31 and valid for the year and month, or 0 to specify a year by itself or a year and month where the day isn't significant.

## Expr

Represents a textual expression in the Common Expression Language (CEL) syntax. CEL is a C-like expression language. The syntax and semantics of CEL are documented at <https://github.com/google/cel-spec> .

Example (Comparison):

    title: "Summary size limit"
    description: "Determines if a summary is less than 100 chars"
    expression: "document.summary.size() < 100"

Example (Equality):

    title: "Requestor is owner"
    description: "Determines if requestor is the document owner"
    expression: "document.owner == request.auth.claims.email"

Example (Logic):

    title: "Public documents"
    description: "Determine whether the document should be publicly visible"
    expression: "document.type != 'private' && document.type != 'internal'"

Example (Data Manipulation):

    title: "Notification string"
    description: "Create a notification string with a timestamp."
    expression: "'New message received at ' + string(document.create_time)"

The exact variables and functions that may be referenced within an expression are determined by the service that evaluates it. See the service documentation for additional information.

Fields

`expression`

`string`

Textual representation of an expression in Common Expression Language syntax.

`title`

`string`

Optional. Title for the expression, i.e. a short string describing its purpose. This can be used e.g. in UIs which allow to enter the expression.

`description`

`string`

Optional. Description of the expression. This is a longer text which describes the expression, e.g. when hovered over it in a UI.

`location`

`string`

Optional. String indicating the location of the expression for error reporting, e.g. a file name and a position in the file.

## Interval

Represents a time interval, encoded as a Timestamp start (inclusive) and a Timestamp end (exclusive).

The start must be less than or equal to the end. When the start equals the end, the interval is empty (matches no time). When both start and end are unspecified, the interval matches any time.

Fields

`start_time`

`  Timestamp  `

Required. Inclusive start of the interval.

If specified, a Timestamp matching this interval will have to be the same or after the start.

`end_time`

`  Timestamp  `

Optional. Exclusive end of the interval.

If specified, a Timestamp matching this interval will have to be before the end.

## LatLng

An object that represents a latitude/longitude pair. This is expressed as a pair of doubles to represent degrees latitude and degrees longitude. Unless specified otherwise, this object must conform to the [WGS84 standard](https://en.wikipedia.org/wiki/World_Geodetic_System#1984_version) . Values must be within normalized ranges.

Fields

`latitude`

`double`

The latitude in degrees. It must be in the range \[-90.0, +90.0\].

`longitude`

`double`

The longitude in degrees. It must be in the range \[-180.0, +180.0\].
