---
title: Load HTML Documents Asynchronously in .NET with Aspose.HTML
linktitle: Load HTML Documents Asynchronously in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 10
url: /net/html-document-manipulation/load-html-doc-asynchronously-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:LoadHTMLdocAsyn
            // The path to the documents directory.
            string dataDir = "Your Data Directory";
            var document = new HTMLDocument();
            // subscribe to the event 'OnReadyStateChange' that will be fired once document is completely loaded
            document.OnReadyStateChange += (sender, @event) =>
            {
                if (document.ReadyState == "complete")
                {
                    // manipulate with document here
                }
            };
            document.Navigate(dataDir + "input.html");
            // ExEnd:LoadHTMLdocAsyn           
        }
        public static void EventNavigate()
        {
            // ExStart:EventNavigate
            // The path to the documents directory.
            string dataDir = "Your Data Directory";
            var document = new HTMLDocument();
            // you can subscribe to the event 'OnLoad'
            document.OnLoad += (sender, @event) =>
            {
                // manipulate with document here
            };
            document.Navigate(dataDir + "input.html");
            // ExEnd:EventNavigate
        }
```
