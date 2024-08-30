---
title: 使用 Aspose.HTML 在 .NET 中設定環境
linktitle: .NET中的環境配置
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML 在 .NET 中處理 HTML 文檔，以執行腳本管理、自訂樣式、JavaScript 執行控制等任務。這個綜合教程提供了逐步範例和常見問題解答，以幫助您入門。
type: docs
weight: 10
url: /zh-hant/net/advanced-features/environment-configuration/
---

在當今的數位世界中，建立和操作 HTML 文件是許多開發人員的基本任務。無論您是建立 Web 應用程式還是需要將 HTML 轉換為 PDF 或圖像等其他格式，Aspose.HTML for .NET 都是您工具包中的強大工具。在本教程中，我們將探討 Aspose.HTML for .NET 的各個方面，包括先決條件、導入命名空間以及帶有詳細說明的分步示例。

## 先決條件

在我們深入使用 Aspose.HTML for .NET 之前，您需要確保滿足以下先決條件：

1. Visual Studio：確保您的開發電腦上安裝了 Visual Studio。 Aspose.HTML for .NET 旨在與 Visual Studio 無縫協作。

2.  Aspose.HTML for .NET：您可以從網站下載 Aspose.HTML for .NET 函式庫。使用以下連結造訪下載頁面：[下載 .NET 的 Aspose.HTML](https://releases.aspose.com/html/net/).

3. 安裝和授權：下載庫後，請按照文件中提供的安裝說明進行操作。您可能還需要有效的許可證才能使用某些高級功能。您可以從 Aspose 網站取得許可證：[購買 Aspose.HTML 許可證](https://purchase.aspose.com/buy).

4. 免費試用：如果您想在購買許可證之前試用 Aspose.HTML，您可以從此連結取得免費試用版：[Aspose.HTML 免費試用](https://releases.aspose.com/).

現在您已經具備了必要的先決條件，讓我們繼續下一部分，我們將匯入所需的命名空間。

## 導入命名空間

為了有效地使用 Aspose.HTML for .NET，您需要將適當的命名空間匯入到您的專案中。下面，我們將列出我們將介紹的範例所需的命名空間：

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

匯入這些命名空間後，您可以存取 Aspose.HTML for .NET 提供的功能。

## 停用腳本執行

讓我們從在 HTML 文件中停用腳本執行並將其轉換為 PDF 的基本範例開始。請依照下列步驟操作：

1. 建立 HTML 程式碼片段並將其儲存到名為「document.html」的檔案中。

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. 初始化 Aspose.HTML 配置，將「腳本」標記為不受信任的資源。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    //使用指定的配置初始化 HTML 文檔
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        //將 HTML 轉換為 PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

在此範例中，我們阻止了 HTML 文件中的腳本執行，從而確保將其轉換為 PDF 時的安全性。現在，讓我們繼續下一個範例。

## 指定使用者樣式表

有時，您可能希望將自訂樣式套用至 HTML 文件中的元素。以下是使用 Aspose.HTML for .NET 實作此操作的方法：

1. 建立 HTML 程式碼片段並將其儲存到名為「document.html」的檔案中。

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2. 為`<span>`使用使用者樣式表的元素。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    //使用指定的配置初始化 HTML 文檔
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        //將 HTML 轉換為 PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

在此範例中，我們將自訂樣式套用至`<span>`元素，將其文字顏色設為綠色。 Aspose.HTML for .NET 可讓您輕鬆操作樣式。

## JavaScript 執行逾時

在處理可能耗時的 JavaScript 程式碼時，設定逾時以防止無限期執行至關重要。您可以這樣做：

1. 建立一個帶有無限循環的 HTML 程式碼片段，並將其儲存到名為「document.html」的檔案中。

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. 將 JavaScript 執行逾時設為 10 秒。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    //使用指定的配置初始化 HTML 文檔
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        //等待所有腳本完成/取消並將 HTML 轉換為 PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

在此範例中，我們將 JavaScript 執行時間限制為 10 秒，以確保腳本不會無限期地運行，否則可能會導致效能問題。

## 自訂訊息處理程序

有時，在載入 HTML 文件時您可能需要處理錯誤訊息或缺少資源。以下是如何建立自訂訊息處理程序的範例：

1. 建立一個缺少圖片檔案引用的 HTML 程式碼片段，並將其儲存到名為「document.html」的檔案中。

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. 將錯誤訊息處理程序新增至網路服務以記錄失敗的請求。

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    //使用指定的配置初始化 HTML 文檔
    //在文件載入期間，應用程式將嘗試載入影像，我們將在控制台中看到此操作的結果。
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        //將 HTML 轉換為 PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

在此範例中，我們新增了一個自訂訊息處理程序（`LogMessageHandler`) 記錄有關失敗請求的資訊。這對於優雅地調試和處理丟失的資源特別有用。

## 結論

Aspose.HTML for .NET 是一個多功能函式庫，使開發人員能夠有效率地處理 HTML 文件。在本教程中，我們介紹了基本概念並提供了常見任務的逐步範例，包括腳本管理、樣式表自訂、JavaScript 執行控制和自訂訊息處理。

透過遵循本教學中概述的步驟，您可以利用 Aspose.HTML for .NET 的強大功能在 .NET 應用程式中自信地建立、操作和轉換 HTML 文件。

## 常見問題解答

### Q1：我可以在不購買許可證的情況下使用 Aspose.HTML for .NET 嗎？

A1：是的，您可以嘗試 Aspose.HTML for .NET 的免費試用版，但某些進階功能可能需要有效的授權。

### 問題 2：如何取得 Aspose.HTML for .NET 的授權？

 A2：您可以從 Aspose 網站購買許可證：[購買 Aspose.HTML 許可證](https://purchase.aspose.com/buy).

### 問題 3：我可以使用 Aspose.HTML for .NET 將 HTML 文件轉換為哪些格式？

A3：Aspose.HTML for .NET 支援轉換為各種格式，包括 PDF、映像等。

### 問題 4：是否有 Aspose.HTML for .NET 的社群或支援論壇？

 A4：是的，您可以在 Aspose 論壇上找到幫助和支援：[Aspose.HTML 支援論壇](https://forum.aspose.com/).

### Q5：Aspose.HTML for .NET 是否提供文件和教學課程？

 A5：是的，您可以在此處存取文件：[Aspose.HTML for .NET 文檔](https://reference.aspose.com/html/net/).