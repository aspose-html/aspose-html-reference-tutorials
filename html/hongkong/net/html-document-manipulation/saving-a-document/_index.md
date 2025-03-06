---
title: 使用 Aspose.HTML 在 .NET 中儲存文檔
linktitle: 在 .NET 中儲存文檔
second_title: Aspose.HTML .NET HTML 操作 API
description: 透過我們的逐步指南釋放 Aspose.HTML for .NET 的強大功能。學習建立、操作和轉換 HTML 和 SVG 文檔
weight: 16
url: /zh-hant/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML 在 .NET 中儲存文檔


在當今的數位時代，建立和操作 HTML 和 SVG 文件對於許多軟體開發人員和企業來說至關重要。 Aspose.HTML for .NET 是一個功能強大的函式庫，可以簡化這些任務，提供各種功能來處理 HTML、SVG 等。在這份綜合指南中，我們將深入探討 Aspose.HTML for .NET 的基本知識，並將每個範例分解為易於遵循的步驟。無論您是經驗豐富的開發人員還是剛入門，您都會發現本指南對於利用 Aspose.HTML 的功能非常有價值。

## 先決條件

在我們踏上這段旅程之前，讓我們確保您擁有所需的一切：

- 開發環境：確保您的電腦上安裝了 Visual Studio 或任何其他 .NET 開發環境。

- Aspose.HTML for .NET：您需要取得Aspose.HTML for .NET 函式庫。您可以從以下位置下載：[這裡](https://releases.aspose.com/html/net/).

- C# 知識：熟悉 C# 程式語言是有益的，但不是強制性的。本指南旨在適合初學者。

## 導入命名空間

要開始使用 Aspose.HTML for .NET，您需要將必要的命名空間匯入到您的專案中。在您的 C# 程式碼中，包含以下命名空間：

### 步驟1：導入Aspose.HTML命名空間
```csharp
using Aspose.Html;
```

此命名空間將授予您存取各種 HTML 和 SVG 操作功能的權限。

## HTML 到文件

### 第 1 步：初始化一個空 HTML 文檔
```csharp
//初始化一個空的 HTML 文件。
using (var document = new Aspose.Html.HTMLDocument())
{
    //建立文字元素並將其添加到文件中
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    //將 HTML 儲存到磁碟上的檔案中。
    document.Save("document.html");
}
```

在此範例中，我們建立一個 HTML 文件並新增一個簡單的“Hello World!”給它發短信。然後我們將 HTML 儲存到磁碟上的檔案中。

## 沒有連結文件的 HTML

### 步驟 1： 準備一個簡單的 HTML 文件
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

在這裡，我們建立一個基本的 HTML 文件，其中包含指向另一個文件的錨定連結。

### 第 2 步：將“document.html”載入到記憶體中
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //建立保存選項實例
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //將最大處理深度設為 0 以切斷連結的 HTML 檔案。
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    //儲存文件
    document.Save(@".\html-to-file-example\document.html", options);
}
```

在此範例中，我們將 HTML 文件載入到記憶體中，設定最大處理深度以切斷連結文件，然後儲存文件。 

## HTML 到 MHTML

### 步驟 1： 準備一個簡單的 HTML 文件
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

就像範例 2 中一樣，我們會建立一個基本 HTML 文件，其中包含指向另一個文件的錨定連結。

### 步驟 2：將「document.html」載入記憶體並另存為 MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //將文件儲存為 MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

在這裡，我們將 HTML 文件載入到記憶體中並以 MHTML 格式儲存。

## HTML 到 Markdown

### 第 1 步：準備 HTML 程式碼
```csharp
var html_code = "<H2>Hello World!</H2>";
```

在此步驟中，我們定義一個 HTML 程式碼片段，其中包含`<H2>`元素。

### 步驟 2：從 HTML 程式碼初始化文件並另存為 Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    //將文件另存為 Markdown 文件。
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

我們從程式碼片段建立一個 HTML 文件並將其儲存為 Markdown 文件。

## SVG 到文件

### 第 1 步：準備 SVG 程式碼
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' 高度='80' 寬度='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

在這裡，我們創建了一個 SVG 程式碼來繪製一個簡單的彩色圖形。

### 步驟 2：從程式碼初始化 SVG 文件並儲存到磁碟
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    //將 SVG 檔案儲存到磁碟
    document.Save("document.svg");
}
```

在此步驟中，我們從程式碼建立一個 SVG 文件並將其儲存為 SVG 檔案。

## 結論

Aspose.HTML for .NET 是一個多功能函式庫，可簡化 .NET 應用程式中的 HTML 和 SVG 文件處理。在本指南中，我們介紹了五個基本範例，並將每個範例分解為逐步說明。無論您是建立、操作還是轉換文檔，Aspose.HTML 都能滿足您的需求。透過執行這些步驟，您就可以很好地掌握這個強大的工具。

## 常見問題解答

### Q1：什麼是 .NET 的 Aspose.HTML？

A1：Aspose.HTML for .NET 是一個 .NET 函式庫，它提供了處理 HTML 和 SVG 文件的廣泛功能，包括建立、操作和轉換。

### Q2：哪裡可以下載 Aspose.HTML for .NET？

 A2：您可以從下列位置下載 Aspose.HTML for .NET[這裡](https://releases.aspose.com/html/net/).

### Q3：Aspose.HTML for .NET 適合初學者嗎？

A3：是的，Aspose.HTML for .NET 可供初學者和經驗豐富的開發人員使用。本指南中的範例旨在適合初學者。

### Q4：我可以使用 Aspose.HTML for .NET 將 HTML 轉換成其他格式嗎？

A4：是的，Aspose.HTML for .NET 支援轉換為各種格式，包括 MHTML 和 Markdown，如範例所示。

### 問題 5：在哪裡可以獲得 Aspose.HTML for .NET 的支援？

 A5：您可以在 Aspose.HTML 社群論壇中找到問題的支援和答案[這裡](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
