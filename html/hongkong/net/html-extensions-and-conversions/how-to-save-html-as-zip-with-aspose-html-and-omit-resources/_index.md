---
category: general
date: 2026-10-21
description: 學習如何使用 Aspose.HTML 將 HTML 儲存為 ZIP、將 HTML 轉換為 ZIP，並剝除資源以獲得乾淨的封裝。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: zh-hant
lastmod: 2026-10-21
og_description: 使用 Aspose.HTML 將 HTML 儲存為 ZIP，了解如何將 HTML 轉換為 ZIP 並剝除資源，以獲得輕量化的壓縮檔。
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: 使用 Aspose.HTML 將 HTML 儲存為 ZIP – 一次省略資源
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: 如何使用 Aspose.HTML 將 HTML 儲存為 ZIP 並省略資源
url: /zh-hant/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.HTML 將 HTML 儲存為 ZIP 並省略資源

如果您需要 **將 HTML 儲存為 ZIP** 並移除外部檔案，本指南提供完整、可直接執行的解決方案。完成本教學後，您將能夠 **將 HTML 轉換為 ZIP**、控制保留哪些資源，並產生只包含核心標記的乾淨壓縮檔。

許多網頁自動化情境需要將頁面打包供離線使用、電子郵件附件或歸檔保存。若同時包含圖片、字型或腳本，往往會不必要地膨脹壓縮檔大小。以下步驟說明 **如何省略資源** 以及 **如何從輸出中剔除資源**，讓最終的 ZIP 保持輕量。

## 前置條件

開始之前，請確保您已具備：

- 已安裝 .NET 6.0 或更新版本  
- Aspose.HTML for .NET 授權（或免費評估版）  
- 基本的 C# 開發環境（Visual Studio、VS Code 或 Rider）  

除 `Aspose.Html` 之外，無需額外的 NuGet 套件。

## 步驟 1：建立自訂資源處理器

**如何省略資源** 的核心在於繼承 `ResourceHandler` 的子類別。Aspose.HTML 會在每個外部資產（圖片、CSS、腳本）時呼叫此處理器。回傳空的串流即等同於告訴轉換器跳過該資產。

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**為什麼這很重要：** 預設行為會將所有連結的檔案複製到 ZIP 中，可能會使檔案大小加倍或三倍。覆寫 `HandleResource` 可讓您在不修改原始 HTML 的前提下，精細控制資源的處理。

## 步驟 2：載入 HTML 文件

使用 `HTMLDocument` 載入來源檔案。建構函式接受檔案路徑、URL 或串流。本範例讀取本機的 `input.html`。

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

如果您的 HTML 位於記憶體中或來自 Web 請求，也可以傳入 `MemoryStream` 或 URL 字串。API 的使用方式相同。

## 步驟 3：設定儲存選項

建立 `HtmlSaveOptions` 實例，並指派在步驟 1 中建立的自訂處理器。這樣 Aspose.HTML 在遇到資源時就會使用該處理器。

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

您也可以在此調整其他選項，例如若想保留影像資料但仍省略其他資產，可將 `CompressImages = false`。範例保留預設的壓縮設定。

## 步驟 4：將文件儲存為 ZIP 壓縮檔

最後，呼叫 `Save` 並傳入目標路徑與先前設定的選項。輸出檔案將是一個 `.zip`，內含 `index.html`（或原始檔名）且 **不含外部資源**。

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### 預期結果

- `output.zip` → 只包含單一的 `index.html` 檔案。  
- 所有圖片、CSS 檔案與 JavaScript 參考皆被省略，因為自訂處理器對每個資源回傳了空的串流。  

您可以使用任何 ZIP 檢視器打開驗證。HTML 頁面仍會引用原始 URL，但這些檔案不會出現在壓縮檔內，從而保持最小化的封裝。

## 完整可執行範例

以下是完整程式碼，您可以直接複製、貼上並執行。將 `YOUR_DIRECTORY` 替換為您機器上的實際資料夾路徑。

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

執行此程式後，即會產生前述的 ZIP 檔。您現在可以在不捆綁不必要資產的情況下分發 HTML 頁面。

## 常見變化與邊緣案例

| 情境 | 調整方式 |
|----------|------------|
| **保留圖片但移除 CSS/JS** | 在 `CustomResourceHandler` 中檢查 `info.MimeType`。僅對 `text/css` 與 `application/javascript` 回傳 `MemoryStream`，其他則回傳空串流。 |
| **保留外部字型** | 對 `font/woff2` MIME 類型回傳原始串流，其他則回傳空串流。 |
| **產生自訂條目名稱的 ZIP** | 使用 `HtmlSaveOptions` 的 `Save(string path, SaveOptions options, string entryName)` 重載，指定不同的根檔名。 |
| **將多個 HTML 檔案合併成單一 ZIP** | 迭代每個檔案，分別建立 `HTMLDocument`，然後使用 `System.IO.Compression` 手動將每個文件加入同一個 `ZipArchive`。 |

這些變化說明了 **如何有選擇地剔除資源**，讓您完整掌控最終壓縮檔的大小。

## 專業小技巧

- **驗證結果**：儲存後，開啟 ZIP 並在瀏覽器載入 `index.html`。缺少的資源會顯示斷裂的連結，證明處理器已正確運作。  
- **效能**：回傳空的 `MemoryStream` 成本低廉，但若資產數量達千級，建議快取決策（例如使用 `HashSet<string>` 來記錄要跳過的 MIME 類型）。  
- **授權**：免費評估版的 Aspose.HTML 會在 HTML 中加入水印註解。部署正式版授權即可移除，適用於生產環境。  

## 結論

您現在已掌握如何 **將 HTML 儲存為 ZIP**、**將 HTML 轉換為 ZIP**，以及使用 Aspose.HTML for .NET **剔除資源**。透過自訂 `ResourceHandler`，您可以省略不需要的檔案，讓壓縮檔保持輕量。請自行調整處理器邏輯，只保留真正需要的資源，並將此模式整合至更大的自動化流程中。

---

**後續步驟**

- 探索 `HtmlSaveOptions` 的其他功能，例如 `EmbedImages` 直接將圖片嵌入 HTML。  
- 結合此方法與 `Aspose.PDF`，在建立 ZIP 後再將相同的 HTML 轉換為 PDF。  
- 研究伺服器端情境，於需求時即時產生 ZIP 並串流給客戶端，而不寫入磁碟。  

祝開發順利！

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，能進一步深化您對相關 API 的運用與實作方式。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您在專案中靈活運用。

- [如何使用 ZipArchive – 將 HTML 與資源儲存為 ZIP 檔](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [如何在 C# 中儲存 HTML – 自訂資源處理器與 ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [如何在 C# 中將 HTML 儲存為 ZIP – 完整 Aspose.HTML 教學](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}