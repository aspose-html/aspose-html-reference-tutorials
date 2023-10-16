---
title: Markdown Options for HTML to Markdown Conversion
linktitle: Markdown Options for HTML to Markdown Conversion
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/html-conversion-markdown/markdown-options-html-to-markdown/
---

## Complete Source Code
```java
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("<p>my first paragraph</p>", Resources.outputDirectory());
        try {
            // Save to markdown by using default for the GIT formatting model
            document.save(Resources.output("Markdown-with-options.out.md"), com.aspose.html.saving.MarkdownSaveOptions.getGit());
        } finally {
            if (document != null) {
                document.dispose();
            }
        }
```
