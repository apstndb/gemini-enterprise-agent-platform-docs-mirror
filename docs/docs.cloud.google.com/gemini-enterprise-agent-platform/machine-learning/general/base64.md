---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/base64
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/base64
title: Encode image data using Base64
description: Provide image data for prediction to the Agent Platform API by sending the image data as Base64-encoded text.
data_source: docs.cloud.google.com
---

You can provide image data for prediction to the Agent Platform API by sending the image data as Base64-encoded text.

## Using the command line

Within a gRPC request, you can simply write binary data out directly; however, JSON is used when making a REST request. JSON is a text format that does not directly support binary data, so you will need to convert such binary data into text using [Base64](https://en.wikipedia.org/wiki/Base64) encoding.

Most development environments contain a native `base64` utility to encode a binary into ASCII text data. To encode a file:

### Linux

Encode the file using the `base64` command line tool, making sure to prevent line-wrapping by using the `-w 0` flag:

    base64 INPUT_FILE -w 0 > OUTPUT_FILE

### macOS

Encode the file using the `base64` command line tool:

    base64 -i INPUT_FILE -o OUTPUT_FILE

### Windows

Encode the file using the `Base64.exe` tool:

    Base64.exe -e INPUT_FILE > OUTPUT_FILE

### PowerShell

Encode the file using the `Convert.ToBase64String` method:

    [Convert]::ToBase64String([IO.File]::ReadAllBytes("./INPUT_FILE")) > OUTPUT_FILE

Create a JSON request file, inlining the base64-encoded data:

### JSON

    {
      "instances": [
        {
          "content": "BASE64_ENCODED_DATA"
        }
      ],
      "parameters": {
        "confidenceThreshold": DECIMAL,
        "maxPredictions": INTEGER
      }
    }

## Using client libraries

Embedding binary data into requests through text editors is neither desirable or practical. In practice, you will be embedding base64 encoded files within client code. All supported programming languages have built-in mechanisms for base64 encoding content.

### Python

    # Import the base64 encoding library.
    import base64
    
    # Pass the image data to an encoding function.
    def encode_image(image):
        with open(image, "rb") as image_file:
            encoded_string = base64.b64encode(image_file.read())
        return encoded_string

### Node.js

    // Read the file into memory.
    var fs = require('fs');
    var imageFile = fs.readFileSync('/path/to/file');
    
    // Convert the image data to a Buffer and base64 encode it.
    var encoded = Buffer.from(imageFile).toString('base64');

### Java

    // Import the Base64 encoding library.
    import org.apache.commons.codec.binary.Base64;
    
    // Encode the image.
    String encodedString = Base64.getEncoder().encodeToString(imageFile.getBytes());

### Go

    import (
        "bufio"
        "encoding/base64"
        "io"
        "os"
    )
    
    // Open image file.
    f, _ := os.Open("image.jpg")
    
    // Read entire image into byte slice.
    reader := bufio.NewReader(f)
    content, _ := io.ReadAll(reader)
    
    // Encode image as base64.
    base64.StdEncoding.EncodeToString(content)
