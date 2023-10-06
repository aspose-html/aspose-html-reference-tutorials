---
title: Web Scraping in .NET with Aspose.HTML
linktitle: Web Scraping in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 13
url: /net/advanced-features/web-scraping-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void NavigateThroughHTML()
        {
            // Prepare an HTML code
            var html_code = "<span>Hello</span> <span>World!</span>";
            // Initialize a document from the prepared code
            using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
            {
                // Get the reference to the first child (first SPAN) of the BODY
                var element = document.Body.FirstChild;
                Console.WriteLine(element.TextContent); // output: Hello
                // Get the reference to the whitespace between html elements
                element = element.NextSibling;
                Console.WriteLine(element.TextContent); // output: ' '
                // Get the reference to the second SPAN element
                element = element.NextSibling;
                Console.WriteLine(element.TextContent); // output: World!
            }
        }
        public static void NodeFilterUsageExample()
        {
            // Prepare an HTML code
            var code = @"
                <p>Hello</p>
                <img src='image1.png'>
                <img src='image2.png'>
                <p>World!</p>";
            // Initialize a document based on the prepared code
            using (var document = new Aspose.Html.HTMLDocument(code, "."))
            {
                // To start HTML navigation we need to create an instance of TreeWalker.
                // The specified parameters mean that it starts walking from the root of the document, iterating all nodes and use our custom implementation of the filter
                using (var iterator = document.CreateTreeWalker(document, Aspose.Html.Dom.Traversal.Filters.NodeFilter.SHOW_ALL, new OnlyImageFilter()))
                {
                    // Use 
                    while (iterator.NextNode() != null)
                    {
                        // Since we are using our own filter, the current node will always be an instance of the HTMLImageElement.
                        // So, we don't need the additional validations here.
                        var image = (Aspose.Html.HTMLImageElement)iterator.CurrentNode;
                        System.Console.WriteLine(image.Src);
                        // output: image1.png
                        // output: image2.png
                    }
                }
            }
        }
        public static void XPathQueryUsageExample()
        {
            // Prepare an HTML code
            var code = @"
                <div class='happy'>
                    <div>
                        <span>Hello!</span>
                    </div>
                </div>
                <p class='happy'>
                    <span>World</span>
                </p>
            ";
            // Initialize a document based on the prepared code
            using (var document = new Aspose.Html.HTMLDocument(code, "."))
            {
                // Here we evaluate the XPath expression where we select all child SPAN elements from elements whose 'class' attribute equals to 'happy':
                var result = document.Evaluate("//*[@class='happy']//span",
                    document,
                    null,
                    Aspose.Html.Dom.XPath.XPathResultType.Any,
                    null);
                // Iterate over the resulted nodes
                for (Aspose.Html.Dom.Node node; (node = result.IterateNext()) != null;)
                {
                    System.Console.WriteLine(node.TextContent);
                    // output: Hello
                    // output: World!
                }
            }
        }
        public static void CSSSelectorUsageExample()
        {
            // Prepare an HTML code
            var code = @"
                <div class='happy'>
                    <div>
                        <span>Hello</span>
                    </div>
                </div>
                <p class='happy'>
                    <span>World!</span>
                </p>
            ";
            // Initialize a document based on the prepared code
            using (var document = new Aspose.Html.HTMLDocument(code, "."))
            {
                // Here we create a CSS Selector that extract all elements whose 'class' attribute equals to 'happy' and their child SPAN elements
                var elements = document.QuerySelectorAll(".happy span");
                // Iterate over the resulted list of elements
                foreach (Aspose.Html.HTMLElement element in elements)
                {
                    System.Console.WriteLine(element.InnerHTML);
                    // output: Hello
                    // output: World!
                }
            }
        }
        class OnlyImageFilter : Aspose.Html.Dom.Traversal.Filters.NodeFilter
        {
            public override short AcceptNode(Aspose.Html.Dom.Node n)
            {
                // The current filter skips all elements, except IMG elements.
                return string.Equals("img", n.LocalName)
                    ? FILTER_ACCEPT
                    : FILTER_SKIP;
            }
        }
```
