---
title: Advanced Mutation Observer with Aspose.HTML for Java
linktitle: Advanced Mutation Observer with Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/mutation-observers-handlers/mutation-observer/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

public class Advanced_MutationObserver {
    public static void main(String [] args) throws java.io.IOException {
        // START_SNIPPET Advanced_MutationObserver
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument();

        com.aspose.html.dom.mutations.MutationObserver observer = new com.aspose.html.dom.mutations.MutationObserver(new com.aspose.html.dom.mutations.MutationCallback() {
            @Override
            public void invoke(com.aspose.html.utils.collections.generic.IGenericList<com.aspose.html.dom.mutations.MutationRecord> mutations, com.aspose.html.dom.mutations.MutationObserver mutationObserver) {
                for (int i = 0 ; i < mutations.size(); i++) {
                    com.aspose.html.dom.mutations.MutationRecord record = mutations.get_Item(i);
                    for (com.aspose.html.dom.Node node : record.getAddedNodes().toArray()) {
                        System.out.println("The '" + node + "' node was added to the document.");
                    }
                }
            }
        });

        // configuration of the observer
        com.aspose.html.dom.mutations.MutationObserverInit config = new com.aspose.html.dom.mutations.MutationObserverInit();
        config.setChildList(true);
        config.setSubtree(true);
        config.setCharacterData(true);

        // pass in the target node to observe with the specified configuration
        observer.observe(document.getBody(), config);

        // Now, we are going to modify DOM tree to check
        // Create an paragraph element and append it to the document body
        com.aspose.html.dom.Element p = document.createElement("p");
        document.getBody().appendChild(p);
        // Create a text and append it to the paragraph
        com.aspose.html.dom.Text text = document.createTextNode("Hello World");
        p.appendChild(text);

        System.out.println("Waiting for mutation. Press any key to continue...");
        System.in.read();
        // END_SNIPPET
    }
}

```
