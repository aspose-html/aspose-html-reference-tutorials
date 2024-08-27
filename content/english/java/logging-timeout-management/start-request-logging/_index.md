---
title: Start Request Duration Logging in Aspose.HTML for Java
linktitle: Start Request Duration Logging in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 11
url: /java/logging-timeout-management/start-request-logging/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import com.aspose.html.net.INetworkOperationContext;

// START_SNIPPET MessageHandlers_StartRequestDurationLoggingMessageHandler
public class StartRequestDurationLoggingMessageHandler extends RequestDurationLoggingMessageHandler {

    @Override
    public void invoke(INetworkOperationContext context) {
        // Start the stopwatch
        startTimer(context.getRequest().getRequestUri());

        // Invoke the next message handler in the chain
        invoke(context);
    }
}
// END_SNIPPET

```
