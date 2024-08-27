---
title: Stop Request Duration Logging with Aspose.HTML for Java
linktitle: Stop Request Duration Logging with Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/logging-timeout-management/stop-request-logging/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import com.aspose.html.net.INetworkOperationContext;

// START_SNIPPET MessageHandlers_StopRequestDurationLoggingMessageHandler
public class StopRequestDurationLoggingMessageHandler extends RequestDurationLoggingMessageHandler {

    @Override
    public void invoke(INetworkOperationContext context) {
        // Start the stopwatch
        stopTimer(context.getRequest().getRequestUri());

        // Invoke the next message handler in the chain
        invoke(context);
    }
}
// END_SNIPPET

```
