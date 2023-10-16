---
title: Specify Markdown Save Options
linktitle: Specify Markdown Save Options
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/converting-between-formats-html-to-markdown/specify-markdown-save-options/
---

## Complete Source Code
```java
        // Prepare an HTML code and save it to the file.
        String code = "<h1>Header 1</h1>\n" +
                      "<h2>Header 2</h2>\n" +
                      "<p>Hello World!!</p>\n" +
                      "<a href='aspose.com'>aspose</a>\n";
        try (java.io.FileWriter fileWriter = new java.io.FileWriter(Resources.output("document.html"))) {
            fileWriter.write(code);
        }
        // Create an instance of SaveOptions and set up the rule:
        // - only <a> and <p> elements will be converted to markdown.
        com.aspose.html.saving.MarkdownSaveOptions options = new com.aspose.html.saving.MarkdownSaveOptions();
        options.setFeatures(
                com.aspose.html.saving.MarkdownFeatures.Link
                |
                com.aspose.html.saving.MarkdownFeatures.AutomaticParagraph
        );
        // Call the ConvertHTML method to convert the HTML to Markdown.
        com.aspose.html.converters.Converter.convertHTML(
                Resources.output("document.html"),
                options,
                Resources.output("output.md")
        );
```
