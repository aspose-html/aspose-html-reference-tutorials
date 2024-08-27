---
title: Log Request Duration in Aspose.HTML for Java
linktitle: Log Request Duration in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/logging-timeout-management/log-request-duration/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import com.aspose.html.Url;
import com.aspose.html.net.MessageHandler;
import com.aspose.html.utils.TimeSpan;

import java.util.HashMap;
import java.util.Map;

// START_SNIPPET MessageHandlers_RequestDurationLoggingMessageHandler
public abstract class RequestDurationLoggingMessageHandler extends MessageHandler {

    private static Map<Url, Long> requests = new HashMap<>();

    protected void startTimer(Url url)
    {
        requests.put(url, System.currentTimeMillis());
    }

    protected TimeSpan stopTimer(Url url)
    {
        long end = System.currentTimeMillis();
        long start = requests.get(url);
        return new TimeSpan(end - start);
    }
}
// END_SNIPPET

```
