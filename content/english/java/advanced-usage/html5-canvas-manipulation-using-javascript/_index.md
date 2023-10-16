---
title: HTML5 Canvas Manipulation Using JavaScript
linktitle: HTML5 Canvas Manipulation Using JavaScript
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/advanced-usage/html5-canvas-manipulation-using-javascript/
---

## Complete Source Code
```java
        //@START
        // Prepare a document with HTML5 Canvas inside and save it to the file 'document.html'
        String code = "< canvas id = myCanvas width = '200' height = '100' style = 'border:1px solid #d3d3d3;' ></canvas >\n" +
                      "<script >\n" +
                      "    var c = document.getElementById('myCanvas');\n" +
                      "    var context = c.getContext('2d');\n" +
                      "    context.font = '20px Arial';\n" +
                      "    context.fillStyle = 'red';\n" +
                      "    context.fillText('Hello World', 40, 50);\n" +
                      "</script >\n";
        try (java.io.FileWriter fileWriter = new java.io.FileWriter(Resources.output("document.html"))) {
            fileWriter.write(code);
        }
        // Initialize an HTML document from the html file
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(Resources.output("document.html"));
        try {
            // Convert HTML to PDF
            com.aspose.html.converters.Converter.convertHTML(
                    document,
                    new com.aspose.html.saving.PdfSaveOptions(),
                    Resources.output("output.pdf")
            );
        } finally {
            if (document != null) {
                document.dispose();
            }
        }
        //@END
```
