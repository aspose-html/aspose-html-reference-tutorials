---
title: Custom Schema Message Filtering in Aspose.HTML for Java
linktitle: Custom Schema Message Filtering in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/custom-schema-message-handling/custom-schema-message-filter/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import com.aspose.html.net.INetworkOperationContext;
import com.aspose.html.net.MessageFilter;

// START_SNIPPET MessageHandlers_CustomeShemaMessageFilter
public class CustomSchemaMessageFilter extends MessageFilter {

    private final String schema;

    CustomSchemaMessageFilter(String schema) {
        this.schema = schema;
    }

    @Override
    public boolean match(INetworkOperationContext context) {
        String protocol = context.getRequest().getRequestUri().getProtocol();
        return (schema+":").equals(protocol);
    }
}
// END_SNIPPET

```
