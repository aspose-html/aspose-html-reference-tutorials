---
title: Converting SVG to XPS
linktitle: Converting SVG to XPS
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 16
url: /java/conversion-html-to-other-formats//conversion/convert-svg-to-xps/
---

## Complete Source Code
```java
        // Source SVG document
        com.aspose.html.dom.svg.SVGDocument svgDocument = new com.aspose.html.dom.svg.SVGDocument(Resources.input("input.svg"));
        // Initialize XpsSaveOptions
        com.aspose.html.saving.XpsSaveOptions options = new com.aspose.html.saving.XpsSaveOptions();
        options.setBackgroundColor(com.aspose.html.drawing.Color.getCyan());
        // Output file path
        String outputFile = Resources.output("SVGtoXPS_Output.xps");
        // Convert SVG to XPS
        com.aspose.html.converters.Converter.convertSVG(svgDocument, options, outputFile);
```
