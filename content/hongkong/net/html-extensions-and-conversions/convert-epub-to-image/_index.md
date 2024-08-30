---
title: 使用 Aspose.HTML 將 EPUB 轉換為 .NET 中的映像
linktitle: 將 EPUB 轉換為 .NET 中的影像
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML for .NET 將 EPUB 轉換為映像。包含程式碼範例和可自訂選項的逐步教學。
type: docs
weight: 11
url: /zh-hant/net/html-extensions-and-conversions/convert-epub-to-image/
---

在當今的數位時代，操作和轉換各種文件格式的能力是一項寶貴的技能。 Aspose.HTML for .NET 是一個功能強大的工具，可讓開發人員輕鬆處理 HTML 和 EPUB 文件。在本教程中，我們將深入研究 Aspose.HTML for .NET 的世界，並引導您完成將 EPUB 文件轉換為各種圖像格式的過程。我們將把每個範例分解為多個步驟，並解釋整個過程中的每個步驟。

## 先決條件

在我們深入了解 Aspose.HTML for .NET 的世界之前，您應該確保滿足以下先決條件：

1. Visual Studio：確保您的系統上安裝了 Visual Studio。您可以從網站下載。

2.  Aspose.HTML for .NET：您可以從 Aspose 網站取得該程式庫[這裡](https://releases.aspose.com/html/net/).

3. 您的資料目錄：準備一個用於儲存 EPUB 檔案和保存輸出影像的目錄。

4. C# 基礎知識：熟悉 C# 程式設計對於理解和實作本教學中提供的程式碼範例至關重要。

## 導入必要的命名空間

在我們開始使用 Aspose.HTML for .NET 之前，您需要將所需的命名空間匯入到您的 C# 程式碼中。這些命名空間提供對 Aspose.HTML for .NET 功能的存取。

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

現在我們已經具備了先決條件和命名空間，讓我們繼續討論逐步範例。

## 將 EPUB 轉換為 JPEG

```csharp
    string dataDir = "Your Data Directory";
    //開啟現有的 EPUB 檔案進行閱讀。
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        //呼叫ConvertEPUB方法將EPUB檔案轉換為圖片。
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### 步驟

1. 在 dataDir 變數中提供 EPUB 檔案的路徑。
2. 使用 FileStream 開啟 EPUB 檔案進行閱讀。
3. 呼叫 ConvertEPUB 方法，傳遞 EPUB 流、指定輸出格式 (JPEG) 的 ImageSaveOptions 以及輸出檔名（「output.jpg」）。
5. EPUB 檔案將轉換為 JPEG 影像。

在此範例中，我們開啟一個 EPUB 文件，讀取其內容，並將其轉換為 JPEG 影像格式。輸出影像儲存為“output.jpg”。

## 將 EPUB 轉換為 PNG

您可以使用類似的程式碼結構輕鬆將 EPUB 檔案轉換為各種影像格式，例如 PNG、BMP、GIF 和 TIFF。以下是轉換為 PNG 的範例：

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### 步驟
1. 使用 FileStream 開啟 EPUB 檔案進行閱讀。
2. 使用所需的輸出格式（在本例中為 PNG）初始化 ImageSaveOptions 物件。
3. 呼叫 ConvertEPUB 方法，傳遞 EPUB 流、映像保存選項和輸出檔名。
4. EPUB 檔案將轉換為指定的影像格式。

## 指定影像保存選項

您可以透過指定頁面大小和背景顏色等選項來自訂影像輸出。這是一個例子：

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### 步驟

1. 在中提供 EPUB 檔案的路徑`dataDir`多變的。
2. 使用以下命令開啟 EPUB 檔案進行閱讀`FileStream`.
3. 創建一個`ImageSaveOptions`物件並指定所需的輸出格式 (JPEG)。
4. 如果需要，自訂頁面大小和背景顏色。
5. 致電`ConvertEPUB`方法，傳遞 EPUB 流、圖像保存選項和輸出檔名。
6. EPUB 檔案將轉換為具有指定選項的影像。

## 指定自訂串流提供者

如果需要操作輸出流，可以使用自訂流提供者。這是一個例子：

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
MemoryStreamProvider 類別原始碼。

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

### 步驟
1. 在中提供 EPUB 檔案的路徑`dataDir`多變的。
2. 使用以下命令開啟 EPUB 檔案進行閱讀`FileStream`.
3. 創建一個`MemoryStreamProvider`處理自訂輸出流。
4. 致電`ConvertEPUB`方法，傳遞 EPUB 流、圖像保存選項 (JPEG) 和自訂流提供者。
5. 迭代自訂提供者中的記憶體流，將它們儲存到單獨的檔案中。
6. 此範例可讓您根據需要操作和儲存多個輸出流。

## 結論

Aspose.HTML for .NET 是一個多功能函式庫，可簡化 EPUB 和 HTML 文件的使用。它能夠將 EPUB 文件轉換為各種圖像格式和可自訂選項，為開發人員提供了廣泛的應用程式。

---

## 常見問題解答

### 1. 在哪裡可以下載 Aspose.HTML for .NET？

您可以從發佈頁面下載 Aspose.HTML for .NET[這裡](https://releases.aspose.com/html/net/).

### 2. 如何取得 Aspose.HTML for .NET 的臨時授權？

要取得臨時許可證，請造訪臨時許可證頁面[這裡](https://purchase.aspose.com/temporary-license/).

### 3. 在哪裡可以找到 Aspose.HTML for .NET 的其他支援？

如有任何疑問或問題，您可以在支援論壇上向 Aspose 社群尋求協助[這裡](https://forum.aspose.com/).

### 4. 我可以將 EPUB 文件轉換為 PDF 或 XPS 等其他格式嗎？

是的，您可以使用 Aspose.HTML for .NET 將 EPUB 文件轉換為各種格式，包括 PDF 和 XPS。

### 5. Aspose.HTML for .NET 適合小型和大型專案嗎？

絕對地！ Aspose.HTML for .NET 的設計具有可擴充性，使其成為各種規模專案的絕佳選擇。
