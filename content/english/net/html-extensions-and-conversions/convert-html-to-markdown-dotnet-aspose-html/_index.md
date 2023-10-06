---
title: Convert HTML to Markdown in .NET with Aspose.HTML
linktitle: Convert HTML to Markdown in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 18
url: /net/html-extensions-and-conversions/convert-html-to-markdown-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:HTMLtoMarkdown
            // The path to the documents directory.
            string dataDir = RunExamples.GetDataDir_Data();
            using (var document = new Aspose.Html.HTMLDocument("<p>my first paragraph</p>" +
                                                   "<p>my second paragraph</p>", dataDir))
            {
                document.Save(dataDir + "Markdown.md", Saving.HTMLSaveFormat.Markdown);
            }
            // ExEnd:HTMLtoMarkdown          
        }
        public static void MarkdownOptions()
        {
            // The path to the documents directory.
            string dataDir = RunExamples.GetDataDir_Data();
            // ExStart:MarkdownOptions
            using (var document = new Aspose.Html.HTMLDocument("<p>my first paragraph</p>", dataDir))
            {
                // Save to markdown by using default for the GIT formatting model
                document.Save(dataDir + "Markdown.md", Saving.MarkdownSaveOptions.Git);
            }
            // ExEnd:MarkdownOptions          
        }
        public static void DefineMarkdownRules()
        {
            // The path to the documents directory.
            string dataDir = RunExamples.GetDataDir_Data();
            // ExStart:DefineRules
            using (var document = new Aspose.Html.HTMLDocument("<p>my first paragraph</p>", dataDir))
            {
                // Create MarkdownSaveOptions object
                var options = new Aspose.Html.Saving.MarkdownSaveOptions();
                // Set the rules: only <a>, <img> and <p> elements will be converted to markdown.
                options.Features = MarkdownFeatures.Link | MarkdownFeatures.Image | MarkdownFeatures.AutomaticParagraph;
                document.Save(dataDir + "Markdown.md", options);
                // ExEnd:DefineRules
            }
        }
```
