---
title: Inline HTML in Markdown
linktitle: Inline HTML in Markdown
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 11
url: /java/converting-between-formats-html-to-markdown/inline-html-in-markdown/
---

## Complete Source Code
```java
        // Prepare an HTML code and save it to the file.
        String code = "text<div markdown='inline'><code>text</code></div>";
        try (java.io.FileWriter fileWriter = new java.io.FileWriter(Resources.output("document.html"))) {
            fileWriter.write(code);
        }
        // Call ConvertHTML method to convert HTML to Markdown.
        com.aspose.html.converters.Converter.convertHTML(
                Resources.output("document.html"),
                new com.aspose.html.saving.MarkdownSaveOptions(),
                Resources.output("output.md")
        );
        // Output file will contain: text\r\n<div markdown="inline"><code>text</code></div>
```
