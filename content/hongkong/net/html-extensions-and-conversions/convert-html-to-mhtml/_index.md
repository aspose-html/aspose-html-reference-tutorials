---
title: 使用 Aspose.HTML 將 .NET 中的 HTML 轉換為 MHTML
linktitle: 在 .NET 中將 HTML 轉換為 MHTML
second_title: Aspose.HTML .NET HTML 操作 API
description: 使用 Aspose.HTML 將 .NET 中的 HTML 轉換為 MHTML - 高效 Web 內容歸檔的逐步指南。了解如何使用 Aspose.HTML for .NET 建立 MHTML 檔案。
type: docs
weight: 19
url: /zh-hant/net/html-extensions-and-conversions/convert-html-to-mhtml/
---

在 Web 開發領域，高效的文件轉換至關重要。 Aspose.HTML for .NET 函式庫是一個功能強大的工具，可以簡化 HTML 文件到各種格式（包括 MHTML）的轉換。 MHTML 是「MIME HTML」的縮寫，是一種網頁存檔格式，可讓您將網頁及其資源保存在單一檔案中。在本逐步指南中，我們將引導您完成使用 Aspose.HTML for .NET 將 HTML 文件轉換為 MHTML 的過程。

## 先決條件

在我們深入了解轉換過程之前，請確保您具備以下先決條件：

### 1.Aspose.HTML for .NET 函式庫

您需要安裝 Aspose.HTML for .NET 程式庫。如果您還沒有這樣做，您可以從網站下載[這裡](https://releases.aspose.com/html/net/)。請按照網站上提供的安裝說明進行操作。

### 2. HTML 文件範例

若要執行轉換，您需要使用 HTML 文件。確保您準備好範例 HTML 檔案。您可以使用自己的 HTML 文件或從[Aspose.HTML 文檔](https://reference.aspose.com/html/net/).

現在您已經具備了先決條件，讓我們繼續進行轉換。

## 導入命名空間

首先，您需要將必要的命名空間匯入到 C# 程式碼中。這對於存取 Aspose.HTML 庫提供的類別和方法至關重要。

### 導入所需的命名空間

```csharp
using Aspose.Html;
```

現在您已經匯入了必要的命名空間，您可以繼續進行實際的轉換過程。

為了清楚起見，我們將 HTML 文件到 MHTML 的轉換分解為幾個步驟。

## 載入 HTML 文件

```csharp
string dataDir = "Your Data Directory"; //指定您的資料目錄
HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html"); //載入 HTML 文件
```

在此步驟中，您將提供 HTML 文件的路徑。 Aspose.HTML 載入 HTML 文件，使其準備好進行轉換。

## 初始化 MHTMLSaveOptions

```csharp
MHTMLSaveOptions options = new MHTMLSaveOptions();
```

在這裡，您初始化`MHTMLSaveOptions`類，它提供 MHTML 轉換選項。

## 設定資源處理規則

```csharp
options.ResourceHandlingOptions.MaxHandlingDepth = 1;
```

您可以根據需要設定資源處理規則。在此範例中，我們將最大處理深度限制為 1，這表示 MHTML 檔案中將僅包含主 HTML 文件及其直接資源。

## 指定輸出路徑

```csharp
string outputMHTML = dataDir + "HTMLtoMHTML_Output.mht"; //指定輸出檔案路徑
```

在此步驟中，您指定產生的 MHTML 檔案的路徑。這是儲存轉換後的 MHTML 文件的位置。

## 執行轉換

```csharp
Converter.ConvertHTML(htmlDocument, options, outputMHTML);
```

現在，是時候將 HTML 文件轉換為 MHTML 了。這`ConvertHTML`方法將載入的 HTML 文件、您設定的選項以及輸出檔案路徑作為參數。

恭喜！您已使用 Aspose.HTML for .NET 成功將 HTML 文件轉換為 MHTML。現在您可以存取指定輸出路徑處的 MHTML 檔案。

## 結論

對於 Web 開發人員和內容建立者來說，有效地將 HTML 文件轉換為 MHTML 格式是一項寶貴的技能。 Aspose.HTML for .NET 簡化了這個過程，使其易於存取且用戶友好。透過遵循上述逐步指南，您可以輕鬆建立 Web 內容的 MHTML 檔案。

現在，讓我們解決一些常見問題 (FAQ)，以進一步澄清此主題。

## 常見問題解答

### 什麼是 MHTML？為什麼要使用它？

MHTML 是「MIME HTML」的縮寫，是一種網頁存檔格式，可讓您將網頁及其資源保存在單一檔案中。它通常用於存檔 Web 內容、將網頁作為單一文件共用以及確保包含所有資源（圖像、樣式表等），即使它們託管在不同的伺服器上也是如此。

### 轉換為 MHTML 時可以自訂資源處理嗎？

是的你可以。如範例所示，您可以使用以下命令設定資源處理規則`ResourceHandlingOptions`的`MHTMLSaveOptions`班級。您可以控制 MHTML 檔案中包含資源的深度。

### 在哪裡可以找到有關 Aspose.HTML for .NET 的更多資源和文件？

您可以探索[Aspose.HTML 文檔](https://reference.aspose.com/html/net/)取得深入資訊、教學和 API 參考。此外，[Aspose.HTML 論壇](https://forum.aspose.com/)是尋求幫助和討論您可能遇到的任何問題的好地方。

### Aspose.HTML for .NET 是否有免費試用版？

是的，您可以造訪 Aspose.HTML for .NET 免費試用[這個連結](https://releases.aspose.com/)。試用版可讓您在購買之前探索該庫的功能。

### 如何取得 Aspose.HTML for .NET 的臨時授權？

如果您需要臨時許可證，您可以從[Aspose.購買網站](https://purchase.aspose.com/temporary-license/)。該臨時許可證將授予您在有限的時間內存取該庫的全部功能的權限。

