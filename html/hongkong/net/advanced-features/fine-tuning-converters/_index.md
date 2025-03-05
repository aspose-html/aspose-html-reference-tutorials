---
title: 使用 Aspose.HTML 微調 .NET 中的轉換器
linktitle: 在 .NET 中微調轉換器
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML for .NET 將 HTML 轉換為 PDF、XPS 和映像。包含程式碼範例和常見問題的逐步教學。
type: docs
weight: 16
url: /zh-hant/net/advanced-features/fine-tuning-converters/
---

## 介紹

Aspose.HTML for .NET 是一個功能強大的程式庫，允許開發人員操作和轉換各種格式的 HTML 文件。無論您需要將 HTML 轉換為 PDF、XPS 或映像，還是執行其他與 HTML 相關的任務，Aspose.HTML 都提供了一組強大的工具來幫助您完成工作。

在本教程中，我們將探索 Aspose.HTML for .NET 的一些基本功能，並為每個範例提供逐步說明。學完本教學後，您將深入了解如何在 .NET 應用程式中使用 Aspose.HTML for .NET。

## 先決條件

在我們深入研究範例之前，請確保您具備以下先決條件：

-  Aspose.HTML for .NET：您應該安裝 Aspose.HTML for .NET 程式庫。您可以從[下載連結](https://releases.aspose.com/html/net/).

- 臨時許可證（可選）：如果您沒有有效許可證，您可以從以下位置取得臨時許可證：[這裡](https://purchase.aspose.com/temporary-license/).

現在，讓我們來探索 Aspose.HTML for .NET 的一些常見用例。

## 導入命名空間

在 C# 程式碼中，首先匯入必要的命名空間：

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## 將 HTML 轉換為 PDF

### 第 1 步：準備 HTML 程式碼

```csharp
var code = @"<span>Hello World!!</span>";
```

### 第 2 步：初始化 HTML 文檔

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步驟3：建立PDF設備並指定輸出文件

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### 第 4 步：將 HTML 渲染為 PDF

```csharp
document.RenderTo(device);
```

此範例將 HTML 片段轉換為 PDF 文件。您可以根據需要自訂 HTML 程式碼和輸出檔案。

## 設定自訂頁面尺寸

### 第 1 步：準備 HTML 程式碼

```csharp
var code = @"<span>Hello World!!</span>";
```

### 第 2 步：初始化 HTML 文檔

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 第 3 步：建立 PDF 渲染選項

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### 步驟 4：建立 PDF 裝置並指定選項和輸出文件

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 第 5 步：將 HTML 渲染為 PDF

```csharp
document.RenderTo(device);
```

此範例示範如何為產生的 PDF 文件設定自訂頁面大小。

## 調整解析度

### 第 1 步：準備 HTML 程式碼並儲存到文件

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### 第 2 步：初始化 HTML 文檔

```csharp
using (var document = new HTMLDocument("document.html"))
```

### 步驟 3：建立低解析度 PDF 渲染選項

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### 步驟 4：建立 PDF 裝置並指定低解析度選項和輸出文件

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### 第 5 步：將 HTML 渲染為低解析度 PDF

```csharp
document.RenderTo(device);
```

### 第 6 步：建立高解析度 PDF 渲染選項

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### 步驟 7：建立 PDF 裝置並指定高解析度的選項和輸出文件

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### 第 8 步：將 HTML 渲染為高解析度 PDF

```csharp
document.RenderTo(device);
```

此範例說明了在將 HTML 渲染為 PDF 時如何調整分辨率，同時考慮低解析度和高解析度螢幕。

## 指定背景顏色

### 第 1 步：準備 HTML 程式碼並儲存到文件

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### 第 2 步：初始化 HTML 文檔

```csharp
using (var document = new HTMLDocument("document.html"))
```

### 步驟 3：使用背景顏色初始化 PDF 渲染選項

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### 步驟 4：建立 PDF 裝置並指定選項和輸出文件

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 第 5 步：將 HTML 渲染為 PDF

```csharp
document.RenderTo(device);
```

此範例示範如何在將 HTML 轉換為 PDF 時指定背景顏色。

## 設定左右頁面尺寸

### 第 1 步：準備 HTML 程式碼

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### 第 2 步：初始化 HTML 文檔

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步驟 3：建立具有左右頁面尺寸的 PDF 渲染選項

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### 步驟 4：建立 PDF 裝置並指定選項和輸出文件

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 第 5 步：將 HTML 渲染為 PDF

```csharp
document.RenderTo(device);
```

此範例示範在將 HTML 轉換為 PDF 時如何為左右頁設定不同的頁面大小。

## 根據內容調整頁面大小

### 第 1 步：準備 HTML 程式碼

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### 第 2 步：初始化 HTML 文檔

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 第 3 步：建立 PDF 渲染選項

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### 步驟 4：建立 PDF 裝置並指定選項和輸出文件

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 第 5 步：將 HTML 渲染為 PDF

```csharp
document.RenderTo(device);
```

此範例示範在將 HTML 轉換為 PDF 時如何將頁面大小調整為最寬的內容。

## 指定 PDF 權限

### 第 1 步：準備 HTML 程式碼

```csharp
var code = @"<div>Hello World!!</div>";
```

### 第 2 步：初始化 HTML 文檔

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步驟 3：建立具有權限的 PDF 渲染選項

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### 步驟 4：建立 PDF 裝置並指定選項和輸出文件

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 第 5 步：將 HTML 渲染為 PDF

```csharp
document.RenderTo(device);
```

此範例示範了在將 HTML 轉換為受保護的 PDF 時如何指定權限和加密。

## 指定特定於影像的選項

### 第 1 步：準備 HTML 程式碼

```csharp
var code = @"<div>Hello World!!</div>";
```

### 第 2 步：初始化 HTML 文檔

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 第 3 步：建立影像渲染選項

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### 步驟 4：建立影像設備並指定選項和輸出文件

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### 第 5 步：將 HTML 渲染為圖像

```csharp
document.RenderTo(device);
```

此範例示範如何將 HTML 轉換為具有特定渲染選項（例如格式、解析度和平滑模式）的影像。

## 指定 XPS 渲染選項

### 第 1 步：準備 HTML 程式碼

```csharp
var code = @"<span>Hello World!!</span>";
```

### 第 2 步：初始化 HTML 文檔

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步驟 3：使用頁面大小建立 XPS 渲染選項

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### 步驟 4：建立 XPS 設備並指定選項和輸出文件

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### 第 5 步：將 HTML 渲染為 XPS

```csharp
document.RenderTo(device);
```

此範例示範如何使用自訂頁面大小和呈現選項將 HTML 轉換為 XPS。

## 將多個 HTML 文件合併為 PDF

### 第 1 步：為多個文件準備 HTML 程式碼

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### 第 2 步：建立要合併的 HTML 文件

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### 第 3 步：初始化 HTML 渲染器

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### 步驟 4：為合併輸出建立 PDF 設備

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### 步驟 5：將 HTML 文件合併為 PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

此範例示範如何使用 Aspose.HTML for .NET 將多個 HTML 文件合併為一個 PDF 檔案。

## 設定渲染超時

### 第 1 步：使用 JavaScript 準備 HTML 程式碼

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### 第 2 步：初始化 HTML 文檔

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 第 3 步：初始化 HTML 渲染器

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### 步驟4：建立PDF設備並設定渲染超時

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### 第 5 步：使用逾時將 HTML 渲染為 PDF

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

此範例示範如何在將 HTML 轉換為 PDF 時設定渲染逾時，這在處理動態內容或長時間運行的腳本時非常有用。

## 結論

Aspose.HTML for .NET 是一個多功能函式庫，使開發人員能夠有效率地處理 HTML 文件。在本教程中，我們介紹了各種範例，從基本的 HTML 到 PDF 轉換到更高級的功能（例如自訂頁面大小、解析度和權限）。遵循這些範例，您可以在 .NET 應用程式中充分利用 Aspose.HTML for .NET 的潛力。

如果您有任何疑問或需要進一步協助，請隨時訪問[Aspose.HTML 論壇](https://forum.aspose.com/)尋求支持和指導。

## 常見問題解答

### Q1.什麼是 .NET 的 Aspose.HTML？
   
A1：Aspose.HTML for .NET 是一個 .NET 函式庫，使開發人員能夠以程式設計方式操作和轉換 HTML 文件。它提供了廣泛的用於處理 HTML 內容的功能，包括 HTML 到 PDF、XPS 和圖像轉換，以及高級渲染選項。

### Q2。在哪裡可以下載 Aspose.HTML for .NET？

 A2：您可以從下列位置下載 Aspose.HTML for .NET[下載連結](https://releases.aspose.com/html/net/).

### Q3。我需要許可證才能使用 Aspose.HTML for .NET 嗎？

A3：雖然您可以在沒有許可證的情況下使用 Aspose.HTML for .NET，但建議您取得用於生產用途的許可證，以解鎖所有功能並刪除任何浮水印或限制。

### Q4。如何保護使用 Aspose.HTML for .NET 產生的 PDF 檔案？

A4：使用 Aspose.HTML for .NET 將 HTML 渲染為 PDF 時，您可以指定 PDF 權限和加密設定。這使您可以控制誰可以存取和修改生成的 PDF 文件。

### Q5.我可以將 HTML 轉換為其他格式（例如 XPS 或圖像）嗎？

A5：是的，Aspose.HTML for .NET 支援將 HTML 轉換為各種格式，包括 PDF、XPS 和映像（例如 JPEG）。您可以自訂轉換設定以滿足您的特定要求。