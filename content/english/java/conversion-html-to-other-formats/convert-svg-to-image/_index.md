---
title: Converting SVG to Image
linktitle: Converting SVG to Image
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 14
url: /java/conversion-html-to-other-formats/convert-svg-to-image/
---

## Complete Source Code
```java
        // Source SVG document
        com.aspose.html.dom.svg.SVGDocument svgDocument = new com.aspose.html.dom.svg.SVGDocument(Resources.input("input.svg"));
        // Initialize ImageSaveOptions
        com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg);
        // Output file path
        String outputFile = Resources.output("SVGtoImage_Output.jpeg");
        // Convert SVG to Image
        com.aspose.html.converters.Converter.convertSVG(svgDocument, options, outputFile);
```
