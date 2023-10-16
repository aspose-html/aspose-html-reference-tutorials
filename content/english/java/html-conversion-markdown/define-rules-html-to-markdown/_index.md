---
title: Define Rules for HTML to Markdown Conversion
linktitle: Define Rules for HTML to Markdown Conversion
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/html-conversion-markdown/define-rules-html-to-markdown/
---

## Complete Source Code
```java
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("<p>my first paragraph</p>", Resources.outputDirectory());
        try {
            // Create MarkdownSaveOptions object
            com.aspose.html.saving.MarkdownSaveOptions options = new com.aspose.html.saving.MarkdownSaveOptions();
            // Set the rules: only <a>, <img> and <p> elements will be converted to markdown.
            options.setFeatures(com.aspose.html.saving.MarkdownFeatures.Link | com.aspose.html.saving.MarkdownFeatures.Image | com.aspose.html.saving.MarkdownFeatures.AutomaticParagraph);
            document.save(Resources.output("output.rules.html.to.md"), options);
        } finally {
            if (document != null) {
                document.dispose();
            }
        }
```
