---
title: Time Logger Message Handler in Aspose.HTML for Java
linktitle: Time Logger Message Handler in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/logging-timeout-management/time-logger-message-handler/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import com.aspose.html.net.INetworkOperationContext;
import com.aspose.html.net.MessageHandler;

// START_SNIPPET MessageHandlers_TimeLoggerMessageHandler

public class TimeLoggerMessageHandler extends MessageHandler {
    @Override
    public void invoke(INetworkOperationContext context) {
        // Start the stopwatch
        long start = System.currentTimeMillis();

        // Invoke the next message handler in the chain
        invoke(context);

        // Stop the stopwatch
        long end = System.currentTimeMillis();

        // Print the result
        System.out.println("Request: " + context.getRequest().getRequestUri());
        System.out.println("Time: " + (end - start) + "ms");
    }
}
// END_SNIPPET
```
