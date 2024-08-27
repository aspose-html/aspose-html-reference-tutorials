---
title: Using Credential Handler in Aspose.HTML for Java
linktitle: Using Credential Handler in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 11
url: /java/mutation-observers-handlers/credential-handler/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import com.aspose.html.net.INetworkOperationContext;
import com.aspose.html.net.MessageHandler;

// START_SNIPPET MessageHandlers_CredentialHandler

public class CredentialHandler extends MessageHandler {
    @Override
    public void invoke(INetworkOperationContext context) {
        // TODO: NetworkCredential is hidden class
//        context.getRequest().setCredentials(new com.aspose.ms.System.Net.NetworkCredential("username", "securelystoredpassword");
        context.getRequest().setPreAuthenticate(true);

        invoke(context);
    }
}

// END_SNIPPET

```
