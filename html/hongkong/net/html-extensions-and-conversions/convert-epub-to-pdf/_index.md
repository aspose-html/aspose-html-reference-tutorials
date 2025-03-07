---
title: 使用 Aspose.HTML 將 EPUB 轉換為 .NET 中的 PDF
linktitle: 在 .NET 中將 EPUB 轉換為 PDF
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML for .NET 將 EPUB 轉換為 PDF。本逐步指南涵蓋了無縫文件轉換的自訂選項、常見問題等。
weight: 12
url: /zh-hant/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML 將 EPUB 轉換為 .NET 中的 PDF


在本教學中，我們將探討如何使用 Aspose.HTML for .NET 將 EPUB 檔案轉換為 PDF。 Aspose.HTML 是一個功能強大的.NET 函式庫，提供了處理 HTML 和 EPUB 文件的各種功能。我們將介紹先決條件，導入必要的命名空間，並分解多個範例，詳細解釋每個步驟。

## 先決條件

在開始之前，請確保您具備以下先決條件：

1. Aspose.HTML for .NET：請確定您的 .NET 專案中安裝了 Aspose.HTML for .NET。您可以從以下位置下載：[這裡](https://releases.aspose.com/html/net/).

2. 您的資料目錄：您將需要一個用於儲存 EPUB 檔案的資料目錄。

現在，讓我們深入了解使用 Aspose.HTML for .NET 將 EPUB 轉換為 PDF 的逐步過程。

## 將 EPUB 轉換為 PDF

### 第 1 步：初始化您的項目

請確定您已設定 .NET 項目，並安裝了 Aspose.HTML for .NET。

### 步驟2：導入所需的命名空間

在您的 C# 程式碼檔案中，匯入必要的命名空間：

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### 步驟 3：開啟 EPUB 文件

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //繼續下一步...
}
```

- 代替`"Your Data Directory"`與 EPUB 檔案所在的實際目錄。
- 此程式碼開啟 EPUB 檔案進行閱讀。

### 步驟 4：設定 PDF 選項並執行轉換

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

- 建立一個實例`PdfSaveOptions`指定 PDF 轉換設定。
- 使用`Converter.ConvertEPUB`使用給定選項將 EPUB 轉換為 PDF 的方法。
- 將產生的 PDF 儲存為“output.pdf”。

## 指定 PDF 儲存選項

### 第 1 步：初始化您的項目

請確定您已設定 .NET 專案並安裝了 Aspose.HTML for .NET。

### 步驟2：導入所需的命名空間

在 C# 程式碼中導入必要的命名空間：

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### 步驟 3：開啟 EPUB 文件

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //繼續下一步...
}
```

- 代替`"Your Data Directory"`與 EPUB 檔案的實際目錄。
- 開啟 EPUB 檔案進行閱讀。

### 第 4 步：自訂 PDF 選項

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

- 建立一個實例`PdfSaveOptions`並根據您的要求進行客製化。
- 在此範例中，我們將頁面大小設定為寬度 3000 像素、高度 1000 像素，背景顏色設定為 Alice Blue。

### 第5步：執行轉換

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

- 使用`Converter.ConvertEPUB`使用自訂選項將 EPUB 轉換為 PDF 的方法。
- 將產生的 PDF 儲存為“output.pdf”。

## 使用自訂流提供者

### 第 1 步：初始化您的項目

設定 .NET 專案並安裝 Aspose.HTML for .NET。

### 步驟2：導入所需的命名空間

在您的 C# 程式碼中，匯入必要的命名空間：

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### 步驟 3：開啟 EPUB 文件

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //繼續下一步...
}
```

- 代替`"Your Data Directory"`與 EPUB 檔案的實際目錄。
- 開啟 EPUB 檔案進行閱讀。

### 第 4 步：使用自訂流程提供程序

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    //繼續下一步...
}
```

- 創建一個`MemoryStreamProvider`將轉換結果作為記憶體流進行管理。
- 使用`Converter.ConvertEPUB`方法與自訂流提供者。

### 第 5 步：儲存結果

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- 存取包含轉換後的資料的記憶體流。
- 將流位置設定為開頭。
- 建立一個輸出 PDF 檔案並將內容從記憶體流複製到其中。

### MemoryStreamProvider 類別原始碼。 

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
現在，您已經學習如何使用 Aspose.HTML for .NET 將 EPUB 檔案轉換為 PDF，並具有各種選項和自訂可能性。 Aspose.HTML 簡化了流程，提供了對文件轉換的靈活性和控制。

## 結論

Aspose.HTML for .NET 是一款用於將 EPUB 檔案轉換為 PDF 的多功能工具，提供自訂選項以根據您的需求自訂產生的 PDF 文件。無論您需要簡單的轉換還是進階自訂，Aspose.HTML 都能滿足您的需求。

如果您還沒有下載 Aspose.HTML for .NET，您可以從[網站](https://releases.aspose.com/html/net/)立即開始在您的 .NET 應用程式中使用它。

---

## 常見問題解答

### Aspose.HTML for .NET 可以免費使用嗎？
    Aspose.HTML for .NET 是一個商業產品，但可以免費試用[這裡](https://releases.aspose.com/).

### 我可以自訂轉換後的 PDF 的外觀嗎？
   是的，您可以透過調整頁面大小和背景顏色等選項來自訂 PDF 外觀，如範例 2 所示。

### 如何獲得 Aspose.HTML for .NET 支援？
   您可以在以下位置找到支援和資源[Aspose.HTML 論壇](https://forum.aspose.com/).

### 我可以使用 Aspose.HTML for .NET 轉換其他格式嗎？
   是的，Aspose.HTML for .NET 支援各種文件格式，包括 HTML、EPUB 等。

### Aspose.HTML for ..NET適合大規模文件轉換嗎？
   Aspose.HTML for .NET 旨在有效處理大規模文件轉換，使其適用於廣泛的應用程式。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
