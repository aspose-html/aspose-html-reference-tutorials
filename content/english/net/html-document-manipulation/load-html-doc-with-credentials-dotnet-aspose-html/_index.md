---
title: Load HTML Documents with Credentials in .NET with Aspose.HTML
linktitle: Load HTML Documents with Credentials in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 11
url: /net/html-document-manipulation/load-html-doc-with-credentials-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            string requestUri = "https://httpbin.org/basic-auth/user/passwd";
            HTMLDocument document = new HTMLDocument();
            try
            {
                var response = document.Context.Network.Send(new RequestMessage(requestUri)
                {
                    Method = HttpMethod.Get,
                    Credentials = new NetworkCredential("user", "passwd"),
                    PreAuthenticate = true
                });
                using (StringReader sr = new StringReader(response.Content.ReadAsString()))
                {
                    System.Console.WriteLine(document.ContentType);
                    System.Console.WriteLine(sr.ReadToEnd());
                }
            }
            catch (System.Exception ex)
            {
                System.Console.WriteLine(ex.Message);
            }
        }
```
