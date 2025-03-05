---
title: 使用 Aspose.HTML 在 .NET 中建立文檔
linktitle: 在 .NET 中建立文檔
second_title: Aspose.HTML .NET HTML 操作 API
description: 釋放 Aspose.HTML for .NET 的強大功能。學習輕鬆建立、操作和優化 HTML 和 SVG 文件。探索逐步範例和常見問題。
type: docs
weight: 14
url: /zh-hant/net/html-document-manipulation/creating-a-document/
---

在不斷發展的網路開發世界中，保持領先地位至關重要。 Aspose.HTML for .NET 為開發人員提供了一個強大的工具包來處理 HTML 文件。無論您是從頭開始、從文件加載、從 URL 提取還是處理 SVG 文檔，該庫都能提供您所需的多功能性。

在本逐步指南中，我們將深入研究使用 Aspose.HTML for .NET 的基礎知識，確保您有能力在 Web 開發專案中使用此強大的工具。在深入了解細節之前，讓我們先回顧一下開始您的旅程所需的先決條件和必要的命名空間。

## 先決條件

要成功學習本教學並利用 Aspose.HTML for .NET 的強大功能，您需要滿足以下先決條件：

- 安裝了 .NET Framework 或 .NET Core 的 Windows 電腦。
- 像 Visual Studio 這樣的程式碼編輯器。
- C# 程式設計基礎知識。

現在您已經具備了先決條件，讓我們開始吧。

## 導入命名空間

在開始使用 Aspose.HTML for .NET 之前，您需要匯入必要的命名空間。這些命名空間包含對於處理 HTML 文件至關重要的類別和方法。以下是您應匯入的命名空間清單：

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

匯入這些命名空間後，您現在就可以深入研究逐步範例了。

## 從頭開始建立 HTML 文件

### 第 1 步：初始化一個空 HTML 文檔

```csharp
//初始化一個空的 HTML 文件。
using (var document = new Aspose.Html.HTMLDocument())
{
    //建立文字元素並將其添加到文件中
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    //將文檔儲存到磁碟。
    document.Save("document.html");
}
```

在此範例中，我們首先建立一個空 HTML 文件並新增“Hello World!”給它發短信。然後我們將文檔保存到文件中。

## 從文件建立 HTML 文件

### 第 1 步：準備「document.html」文件

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### 第 2 步：從「document.html」檔案載入

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //將文件內容寫入輸出流。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

在這裡，我們準備一個包含「Hello World!」的文件。內容，然後將其載入為 HTML 文件。我們將文件的內容列印到控制台。

## 從 URL 建立 HTML 文件

### 步驟 1：從網頁載入文檔

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    //將文件內容寫入輸出流。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

在此範例中，我們直接從網頁載入 HTML 文件並顯示其內容。

## 從字串建立 HTML 文件

### 第 1 步：準備 HTML 程式碼

```csharp
var html_code = "<p>Hello World!</p>";
```

### 步驟 2：從字串變數初始化文檔

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    //將文檔儲存到磁碟。
    document.Save("document.html");
}
```

在這裡，我們從字串變數建立一個 HTML 文件並將其保存到文件中。

## 從 MemoryStream 建立 HTML 文檔

### 第一步：建立記憶體流對象

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    //將 HTML 程式碼寫入記憶體對象
    sw.Write("<p>Hello World!</p>");
    //將位置設為開頭
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    //從記憶體流初始化文檔
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        //將文檔儲存到磁碟。
        document.Save("document.html");
    }
}
```

在此範例中，我們從記憶體流建立 HTML 文件並將其儲存到文件中。

## 使用 SVG 文檔

### 第 1 步：從字串初始化 SVG 文檔

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    //將文件內容寫入輸出流。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

在這裡，我們從字串建立並顯示 SVG 文件。

## 非同步載入 HTML 文檔

### 第 1 步：建立 HTML 文件實例

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### 第 2 步：訂閱「ReadyStateChange」事件

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //檢查“ReadyState”屬性的值。
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### 步驟 3：在指定的 Uri 處非同步導航

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

在此範例中，我們非同步載入 HTML 文件並處理「ReadyStateChange」事件以在載入完成時顯示內容。

## 處理“OnLoad”事件

### 第 1 步：建立 HTML 文件實例

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### 第 2 步：訂閱「OnLoad」事件

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### 步驟 3：在指定的 Uri 處非同步導航

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

此範例示範非同步載入 HTML 文件並處理「OnLoad」事件以在完成後顯示內容。

## 綜上所述

在動態的 Web 開發世界中，擁有合適的工具至關重要。 Aspose.HTML for .NET 為您提供了高效能建立、操作和處理 HTML 和 SVG 文件的方法。這份全面的指南向您介紹了基本知識，確保您可以在專案中利用 Aspose.HTML for .NET 的強大功能。

## 常見問題解答

### Q1：什麼是 .NET 的 Aspose.HTML？

A1：Aspose.HTML for .NET 是一個功能強大的 .NET 程式庫，可讓開發人員處理 HTML 和 SVG 文件。它提供了廣泛的功能，從從頭開始建立文件到解析和操作現有的 HTML 和 SVG 文件。

### 問題 2：我可以將 Aspose.HTML for .NET 與 .NET Core 一起使用嗎？

A2：是的，Aspose.HTML for .NET 與 .NET Framework 和 .NET Core 相容，使其成為現代 .NET 應用程式的多功能選擇。

### Q3：Aspose.HTML for .NET 適合網頁抓取和解析嗎？

A3：當然！ Aspose.HTML for .NET 是網頁抓取和解析任務的絕佳選擇，因為它能夠從 URL 和字串載入 HTML 文件。您可以提取數據、執行分析等等。

### 問題 4：如何獲得對 Aspose.HTML for .NET 的支援？

 A4：如果您在使用 Aspose.HTML for .NET 時遇到任何問題或有疑問，您可以訪問[Aspose論壇](https://forum.aspose.com/)感謝社區和 Aspose 專家的支持和幫助。

### A5：在哪裡可以找到詳細的文件和下載選項？

A5：有關完整的文檔和下載選項的訪問，您可以參考以下連結：

- [文件](https://reference.aspose.com/html/net/)
- [下載](https://releases.aspose.com/html/net/)
- [買](https://purchase.aspose.com/buy)
- [免費試用](https://releases.aspose.com/)
- [臨時執照](https://purchase.aspose.com/temporary-license/)