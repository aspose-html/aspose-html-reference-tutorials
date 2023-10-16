---
title: Convert HTML to Markdown Using Git Syntax
linktitle: Convert HTML to Markdown Using Git Syntax
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/converting-between-formats-html-to-markdown/convert-html-to-markdown-using-git-syntax/
---

## Complete Source Code
```java
        // Prepare an HTML code and save it to the file.
        String code = "<h1>Header 1</h1>\n" +
                      "<h2>Header 2</h2>\n" +
                      "<p>Hello World!!</p>\n";
        try (java.io.FileWriter fileWriter = new java.io.FileWriter(Resources.output("document.html"))) {
            fileWriter.write(code);
        }
        // Call ConvertHTML method to convert HTML to Markdown.
        com.aspose.html.converters.Converter.convertHTML(
                Resources.output("document.html"),
                com.aspose.html.saving.MarkdownSaveOptions.getGit(),
                Resources.output("output.md")
        );
```
