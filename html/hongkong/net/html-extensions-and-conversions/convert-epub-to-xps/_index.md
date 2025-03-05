---
title: 使用 Aspose.HTML 將 EPUB 轉換為 .NET 中的 XPS
linktitle: 在 .NET 中將 EPUB 轉換為 XPS
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML for .NET 將 EPUB 轉換為 .NET 中的 XPS。按照我們的逐步指南輕鬆進行轉換。
type: docs
weight: 13
url: /zh-hant/net/html-extensions-and-conversions/convert-epub-to-xps/
---

您是否正在尋找一種在 .NET 應用程式中將 EPUB 檔案轉換為 XPS 格式的無縫方法？ Aspose.HTML for .NET 提供了一個強大的解決方案來輕鬆實現這一目標。在本逐步指南中，我們將引導您完成使用 Aspose.HTML 將 EPUB 轉換為 XPS 的過程。讓我們開始吧！

## 先決條件

在開始 EPUB 到 XPS 轉換過程之前，您需要確保您符合以下先決條件：

### 1.Aspose.HTML for .NET 函式庫

請確定您的專案中安裝了 Aspose.HTML for .NET 程式庫。如果您還沒有這樣做，您可以從[Aspose.HTML for .NET 下載頁面](https://releases.aspose.com/html/net/).

### 2.輸入EPUB文件

您需要一個要轉換為 XPS 的 EPUB 檔案。確保您有可用於轉換的 EPUB 檔案。

### 3..NET開發環境

本指南假設您的電腦上設定了有效的 .NET 開發環境。

## 導入命名空間

首先，您應該為 Aspose.HTML 匯入必要的命名空間：

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## 將 EPUB 轉換為 XPS

讓我們將 EPUB 檔案轉換為 XPS 格式的過程分解為多個步驟。

### 步驟1.1：開啟EPUB文件

首先，使用 FileStream 開啟現有的 EPUB 檔案進行讀取：

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //繼續轉換過程
}
```

### 步驟1.2：建立XpsSaveOptions

建立 XpsSaveOptions 的實例。此步驟對於配置 XPS 輸出至關重要：

```csharp
var options = new XpsSaveOptions();
```

### 步驟1.3：將 EPUB 轉換為 XPS

現在，我們呼叫 ConvertEPUB 方法將 EPUB 轉換為 XPS：

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## 指定自訂 XPS 選項

您可以透過指定頁面大小和背景顏色等自訂選項來進一步自訂 XPS 輸出。

### 步驟2.1：自訂頁面尺寸與背景顏色

建立具有自訂頁面大小和背景顏色的 XpsSaveOptions 實例：

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### 步驟 2.2：使用自訂選項將 EPUB 轉換為 XPS

現在，呼叫 ConvertEPUB 方法，使用自訂選項將 EPUB 轉換為 XPS：

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## 使用自訂流提供者

在此步驟中，我們將使用自訂流程提供者將 EPUB 轉換為 XPS，從而允許您操作結果資料。

### 步驟3.1：建立MemoryStreamProvider

建立 MemoryStreamProvider 的實例：

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    //繼續轉換過程
}
```

### 步驟 3.2：使用 Stream Provider 將 EPUB 轉換為 XPS

使用 MemoryStreamProvider 將 EPUB 轉換為 XPS：

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### 步驟 3.3：存取並儲存結果

檢索包含轉換後的資料的記憶體流並將其儲存到輸出檔案：

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### 類別 MemoryStreamProvider 原始碼

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            //在文件渲染期間建立的 MemoryStream 物件列表
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                //當僅需要一個輸出流時（例如 XPS、PDF 或 TIFF 格式），將呼叫此方法。
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                //當需要建立多個輸出流時呼叫此方法。例如，在渲染 HTML 到圖像檔案清單（JPG、PNG 等）期間
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                //在這裡您可以釋放充滿資料的串流，例如將其刷新到硬碟
            }
            public void Dispose()
            {
                //釋放資源
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
恭喜！您已使用 Aspose.HTML for .NET 成功將 EPUB 檔案轉換為 XPS 格式。

## 結論

在這個綜合教學中，我們探索如何利用 Aspose.HTML for .NET 透過各種自訂選項將 EPUB 檔案轉換為 XPS 格式。無論您是經驗豐富的開發人員還是新手，Aspose.HTML 都能簡化流程，讓您輕鬆處理 EPUB 到 XPS 的轉換。

有任何疑問或遇到問題嗎？查看[Aspose.HTML 文檔](https://reference.aspose.com/html/net/)獲取更多見解或尋求協助[Aspose.HTML 社群論壇](https://forum.aspose.com/).

## 常見問題解答

### 什麼是 .NET 的 Aspose.HTML？
Aspose.HTML for .NET 是一個功能強大的函式庫，使開發人員能夠在 .NET 應用程式中使用 HTML、EPUB 和 XPS 文件。

### 在哪裡可以下載 Aspose.HTML for .NET？
您可以從以下位置下載 Aspose.HTML for .NET[下載頁面](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET 是否有免費試用版？
是的，您可以從以下位置獲得免費試用[這裡](https://releases.aspose.com/).

### 如何取得 Aspose.HTML for .NET 的臨時授權？
要獲得臨時許可證，請訪問[臨時許可證頁面](https://purchase.aspose.com/temporary-license/).

### 在哪裡可以找到有關 Aspose.HTML for .NET 的更多教學和文件？
探索有關的各種教程和詳細文檔[Aspose.HTML 文檔](https://reference.aspose.com/html/net/)頁。