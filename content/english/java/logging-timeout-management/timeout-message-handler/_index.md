---
title: Implement Timeout Message Handler in Aspose.HTML for Java
linktitle: Implement Timeout Message Handler in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 14
url: /java/logging-timeout-management/timeout-message-handler/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import com.aspose.html.net.INetworkOperationContext;
import com.aspose.html.net.MessageHandler;
import com.aspose.html.utils.TimeSpan;

// START_SNIPPET MessageHandlers_TimeoutMessageHandler
public class TimeoutMessageHandler extends MessageHandler {
    @Override
    public void invoke(INetworkOperationContext context) {
        context.getRequest().setTimeout(TimeSpan.fromSeconds(1));
        invoke(context);
    }
}
// END_SNIPPET

```
