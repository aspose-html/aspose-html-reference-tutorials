---
title: HTML to Markdown Conversion
linktitle: HTML to Markdown Conversion
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 11
url: /java/html-conversion-markdown/html-to-markdown/
---

## Complete Source Code
```java
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(
                "<p>my first paragraph</p>" +
                "<p>my second paragraph</p>",
                Resources.outputDirectory()
        );
        try {
            document.save(Resources.output("Markdown-to-html.out.md"), com.aspose.html.saving.HTMLSaveFormat.Markdown);
        } finally {
            if (document != null) {
                document.dispose();
            }
        }
```
