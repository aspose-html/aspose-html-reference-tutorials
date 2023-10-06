---
title: Using HTML Templates in .NET with Aspose.HTML
linktitle: Using HTML Templates in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 17
url: /net/advanced-features/using-html-templates-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void CreateHTMLFromTemplate()
        {
            // Prepare a JSON data-source and save it to the file.
            var data = @"{
                'FirstName': 'John',
                'LastName': 'Smith',
                'Address': {
                    'City': 'Dallas',
                    'Street': 'Austin rd.',
                    'Number': '200'
                    }
                }";
            System.IO.File.WriteAllText("data-source.json", data);
            // Prepare an HTML Template and save it to the file.
            var template = @"
                <table border=1>
                    <tr>
                        <th>Person</th>
                        <th>Address</th>
                    </tr>
                    <tr>
                        <td>{{FirstName}} {{LastName}}</td>
                        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
                    </tr>
                </table>
                ";
            System.IO.File.WriteAllText("template.html", template);
            // Invoke Converter.ConvertTemplate in order to populate 'template.html' with the data-source from 'data-source.json' file
            Aspose.Html.Converters.Converter.ConvertTemplate("template.html", new Aspose.Html.Converters.TemplateData("data-source.json"), new Aspose.Html.Loading.TemplateLoadOptions(), "document.html");
        }
```
