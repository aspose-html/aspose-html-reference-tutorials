---
title: Configure Runtime Service in Aspose.HTML for Java
linktitle: Configure Runtime Service in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 14
url: /java/configuring-environment/configure-runtime-service/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import java.io.IOException;

public class WorkingWithHTMLDocuments_EnvironmentConfiguration_RuntimeService {
    public static void main(String [] args) throws IOException {
        // START_SNIPPET WorkingWithHTMLDocuments_EnvironmentConfiguration_RuntimeService
        // Prepare an HTML code and save it to the file.
        String code = "<h1>Runtime Service</h1>\r\n" +
                "<script> while(true) {} </script>\r\n" +
                "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";

        try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
            fileWriter.write(code);
        }

        // Create an instance of Configuration
        com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
        try {
            // Limit JS execution time to 5 seconds
            com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
            runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));


            // Initialize an HTML document with specified configuration
            com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
            try {
                // Convert HTML to PNG
                com.aspose.html.converters.Converter.convertHTML(
                        document,
                        new com.aspose.html.saving.ImageSaveOptions(),
                        "runtime-service_out.png"
                );
            } finally {
                if (document != null) {
                    document.dispose();
                }
            }
        } finally {
            if (configuration != null) {
                configuration.dispose();
            }
        }
        // END_SNIPPET
    }
}

```
