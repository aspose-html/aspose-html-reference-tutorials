---
title: Custom Schema Message Handler with Aspose.HTML for Java
linktitle: Custom Schema Message Handler with Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 11
url: /java/custom-schema-message-handling/custom-schema-message-handler/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import com.aspose.html.net.MessageHandler;

// START_SNIPPET MessageHandlers_CustomeShemaMessageHandler
public abstract class CustomSchemaMessageHandler extends MessageHandler {

    protected CustomSchemaMessageHandler(String schema) {
        getFilters().addItem(new CustomSchemaMessageFilter(schema));
    }
}
// END_SNIPPET

```
