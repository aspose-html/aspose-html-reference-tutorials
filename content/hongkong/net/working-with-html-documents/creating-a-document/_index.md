---
title: 使用 Aspose.HTML 在 .NET 中建立 HTML 文檔
linktitle: 在 .NET 中建立 HTML 文檔
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML 在 .NET 中從頭開始或從 URL 建立 HTML 文件。面向 Web 開發人員的綜合教程。
type: docs
weight: 10
url: /zh-hant/net/working-with-html-documents/creating-a-document/
---

在 Web 開發和資料操作領域，擁有一個強大的工具來建立、修改和處理 HTML 文件是必不可少的。 Aspose.HTML for .NET 就是這樣一種工具，可以簡化與 HTML 相關的任務。在這個綜合教學中，我們將逐步探索如何使用 Aspose.HTML for .NET 建立 HTML 文件。在深入研究範例之前，我們先介紹一些先決條件。

## 先決條件

在開始此旅程之前，請確保滿足以下先決條件：

1. Visual Studio：確保您的系統上安裝了 Visual Studio。

2.  Aspose.HTML for .NET：下載並安裝 Aspose.HTML for .NET 函式庫。你可以找到下載鏈接[這裡](https://releases.aspose.com/html/net/).

3. C# 基礎知識：熟悉 C# 程式語言基礎。

現在我們已經滿足了先決條件，讓我們開始建立 HTML 文件。

## 導入命名空間

首先，您需要匯入必要的命名空間，以便在 C# 專案中使用 Aspose.HTML。將以下 using 指令加入您的程式碼檔案：

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## 建立 SVG 文件

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        //在此處對 SVG 文檔執行操作...
    }
}
```

在此範例中，我們透過提供 SVG 內容和基本 URL 來建立 SVG 文件。這`SVGDocument`Aspose.HTML for .NET 中的類別可讓您輕鬆地操作 SVG 文件。

## 從頭開始建立 HTML 文件

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        //在此處對 HTML 文件執行操作...
    }
}
```

此範例示範如何從頭開始建立 HTML 文件。這`HTMLDocument`類別為您的 HTML 內容提供了一個空白畫布。

## 從本機文件建立 HTML 文檔

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        //在此處對 HTML 文件執行操作...
    }
}
```

如果本機系統上已有 HTML 文件，則可以使用下列命令載入它`HTMLDocument`類，如本例所示。

## 從遠端 URL 建立 HTML 文檔

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://your.site.com/"))
    {
        //在此處對 HTML 文件執行操作...
    }
}
```

有時，您可能需要使用遠端伺服器上託管的 HTML 內容。此範例示範如何從遠端 URL 建立 HTML 文件。

## 從遠端 URL 建立 HTML 文件（替代）

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://your.site.com/")))
    {
        //在此處對 HTML 文件執行操作...
    }
}
```

此替代方法還展示瞭如何使用不同的建構函式從遠端 URL 建立 HTML 文件。

## 從 HTML 內容建立 HTML 文件

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        //在此處對 HTML 文件執行操作...
    }
}
```

如果您有字串格式的 HTML 內容，則可以使用它來建立 HTML 文檔，如本範例所示。

## 從串流建立 HTML 文件

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            //在此處對 HTML 文件執行操作...
        }
    }
}
```

在此範例中，我們展示瞭如何從記憶體流中的資料建立 HTML 文件。當您在流程中包含 HTML 內容並想要對其進行操作時，這會很有用。

## 結論

Aspose.HTML for .NET 提供了一組強大的工具，可在 .NET 應用程式中建立和使用 HTML 文件。透過本教學中提供的範例，您可以輕鬆開始建立 HTML 文檔，無論是從頭開始、本機文件、遠端 URL 還是現有 HTML 內容。

有疑問或需要協助嗎？請造訪 Aspose.HTML 社群論壇以取得支援：[https://forum.aspose.com/](https://forum.aspose.com/).

## 常見問題解答

### Q1：Aspose.HTML for .NET 可以免費使用嗎？
 A1：Aspose.HTML for .NET 提供免費試用版，但要完全使用，您需要購買授權。您可以在以下位置找到更多詳細資訊：[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### 問題 2：如何取得 Aspose.HTML for .NET 的臨時授權？
A2：如果您需要臨時許可證，您可以在[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### 問題 3：在哪裡可以找到 Aspose.HTML for .NET 的文件？
 A3：文件可以在以下位置找到：[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### Q4：還有其他用於.NET 開發的Aspose 函式庫嗎？
 A4：是的，Aspose 為各種文件格式和文件操作任務提供了一系列函式庫。查看他們的產品[https://products.aspose.com/](https://products.aspose.com/).

### Q5：我可以在我的 Web 應用程式中使用 Aspose.HTML for .NET 嗎？
A5：是的，Aspose.HTML for .NET 與 Web 應用程式相容，使其成為桌面和基於 Web 專案的多功能選擇。
