---
title: 使用 Aspose.HTML 在 .NET 中進行網頁抓取
linktitle: .NET 中的網頁抓取
second_title: Aspose.HTML .NET HTML 操作 API
description: 學習使用 Aspose.HTML 操作 .NET 中的 HTML 文件。有效地導航、過濾、查詢和選擇元素以增強 Web 開發。
type: docs
weight: 13
url: /zh-hant/net/advanced-features/web-scraping/
---

在當今的數位時代，從 HTML 文件中操作和提取資訊是開發人員的常見任務。 Aspose.HTML for .NET 是一個功能強大的工具，可以簡化 .NET 應用程式中的 HTML 處理和操作。在本教程中，我們將探討 Aspose.HTML for .NET 的各個方面，包括先決條件、命名空間和逐步範例，以幫助您充分利用其潛力。

## 先決條件

在深入了解 Aspose.HTML for .NET 的世界之前，您需要滿足一些先決條件：

1. 開發環境：確保您擁有使用 Visual Studio 或任何其他用於 .NET 開發的相容 IDE 設定的工作開發環境。

2.  Aspose.HTML for .NET：從下列位置下載並安裝 Aspose.HTML for .NET 函式庫：[下載連結](https://releases.aspose.com/html/net/)。您可以根據需要選擇免費試用版或授權版。

3. HTML 基礎：熟悉 HTML 結構和元素對於有效使用 Aspose.HTML for .NET 至關重要。

## 導入命名空間

首先，您需要在 C# 專案中匯入必要的命名空間。這些命名空間提供對 Aspose.HTML for .NET 類別和功能的存取：

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

滿足先決條件並匯入命名空間後，我們將逐步分解一些關鍵範例，以說明如何有效地使用 Aspose.HTML for .NET。

## 透過 HTML 導航

在此範例中，我們將瀏覽 HTML 文件並逐步存取其元素。

```csharp
public static void NavigateThroughHTML()
{
    //準備 HTML 程式碼
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    //從準備好的程式碼初始化文檔
    using (var document = new HTMLDocument(html_code, "."))
    {
        //取得 BODY 的第一個子級（第一個 SPAN）的引用
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); //輸出：你好

        //取得 HTML 元素之間的空白的引用
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); //輸出： ' '

        //取得對第二個 SPAN 元素的引用
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); //輸出：世界！
    }
}
```

在此範例中，我們建立一個 HTML 文檔，存取其第一個子文檔（a`SPAN`元素）、元素之間的空白、第二個`SPAN`元素，示範基本導航。

## 使用節點過濾器

節點過濾器可讓您選擇性地處理 HTML 文件中的特定元素。

```csharp
public static void NodeFilterUsageExample()
{
    //準備 HTML 程式碼
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    //根據準備好的程式碼初始化一個文檔
    using (var document = new HTMLDocument(code, "."))
    {
        //使用影像元素的自訂濾鏡建立 TreeWalker
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                //輸出：image1.png
                //輸出：image2.png
            }
        }
    }
}
```

此範例示範如何使用自訂節點過濾器來提取特定元素（在本例中，`IMG`元素）來自 HTML 文件。

## XPath 查詢

XPath 查詢可讓您根據特定條件搜尋 HTML 文件中的元素。

```csharp
public static void XPathQueryUsageExample()
{
    //準備 HTML 程式碼
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
    
    //根據準備好的程式碼初始化一個文檔
    using (var document = new HTMLDocument(code, "."))
    {
        //評估 XPath 表達式以選擇特定元素
        var result = document.Evaluate("//*[@class='happy']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        //迭代結果節點
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            //輸出：你好
            //輸出：世界！
        }
    }
}
```

此範例展示如何使用 XPath 查詢根據元素的屬性和結構來定位 HTML 文件中的元素。

## CSS 選擇器

CSS 選擇器提供了另一種選擇 HTML 文件中的元素的方法，類似於 CSS 樣式表定位元素的方式。

```csharp
public static void CSSSelectorUsageExample()
{
    //準備 HTML 程式碼
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
    
    //根據準備好的程式碼初始化一個文檔
    using (var document = new HTMLDocument(code, "."))
    {
        //使用 CSS 選擇器根據類別和層次結構提取元素
        var elements = document.QuerySelectorAll(".happy span");
        
        //迭代結果元素列表
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            //輸出：你好
            //輸出：世界！
        }
    }
}
```

在這裡，我們示範如何使用 CSS 選擇器來定位 HTML 文件中的特定元素。

透過這些範例，您對如何使用 Aspose.HTML for .NET 在 HTML 文件中導覽、篩選、查詢和選擇元素有了基本的了解。

## 結論

 Aspose.HTML for .NET 是一個多功能函式庫，使 .NET 開發人員能夠有效率地處理 HTML 文件。憑藉其強大的導航、過濾、查詢和選擇元素功能，您可以無縫處理各種 HTML 處理任務。透過遵循本教程並瀏覽以下位置的文檔[Aspose.HTML for .NET 文檔](https://reference.aspose.com/html/net/)，您可以為您的 .NET 應用程式釋放此工具的全部潛力。

## 常見問題解答

### Q1. Aspose.HTML for .NET 可以免費使用嗎？

A1：Aspose.HTML for .NET 提供免費試用版，但要用於生產用途，您需要購買授權。您可以在以下位置找到許可詳細資訊和選項[Aspose.HTML 購買](https://purchase.aspose.com/buy).

### Q2。如何取得 Aspose.HTML for .NET 的臨時授權？

 A2：您可以從以下位置取得測試目的的臨時許可證：[Aspose.HTML臨時許可證](https://purchase.aspose.com/temporary-license/).

### Q3。我可以在哪裡尋求 Aspose.HTML for .NET 的協助或支援？

 A3：如果您遇到任何問題或有疑問，您可以訪問[Aspose.HTML 論壇](https://forum.aspose.com/)尋求幫助和社區支持。

### Q4。是否有其他資源可用於學習 Aspose.HTML for .NET？

 A4：除了本教學之外，您還可以探索更多有關以下內容的教學和文件：[Aspose.HTML for .NET 文件頁面](https://reference.aspose.com/html/net/).

### Q5. Aspose.HTML for .NET 與最新的 .NET 版本相容嗎？

A5：Aspose.HTML for .NET 會定期更新，以確保與最新的 .NET 版本和技術相容。