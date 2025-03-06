---
title: 使用 Aspose.HTML 在 .NET 中套用計量許可證
linktitle: 在 .NET 中應用計量許可證
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何在 Aspose.HTML for .NET 中套用計量許可證。有效管理您的 HTML 操作需求。現在就開始吧！
weight: 10
url: /zh-hant/net/licensing-and-initialization/apply-metered-license/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML 在 .NET 中套用計量許可證

在本教程中，我們將指導您完成使用 Aspose.HTML 在 .NET 應用程式中應用計量授權的過程。計量許可證是管理您的 HTML 操作需求的許可的便捷方法。透過執行下列步驟，您將能夠將計量許可證套用至您的 Aspose.HTML for .NET 專案。

## 先決條件

在繼續之前，請確保滿足以下先決條件：

- 有效的 Aspose.HTML for .NET 授權。您可以從以下位置獲取它：[提出購買](https://purchase.aspose.com/buy).
-  Aspose.HTML for .NET 函式庫，您可以從下列位置下載[這裡](https://releases.aspose.com/html/net/).
- 儲存輸入 HTML 檔案的資料目錄路徑。

現在，讓我們分解範例程式碼並詳細解釋每個步驟：

## 導入命名空間

在您的 .NET 專案中，您需要包含必要的命名空間。在 C# 檔案頂部加入以下 using 語句：

```csharp
using Aspose.Html;
```

## 逐步指南

在這裡，我們將範例程式碼分解為多個步驟，並詳細解釋每個步驟。

### 設定資料目錄路徑：

   首先，您應該設定輸入 HTML 檔案所在的資料目錄的路徑。您需要更換`"Your Data Directory"`與實際路徑。

   ```csharp
   string dataDir = "Your Data Directory";
   ```

### 設定計量公鑰和私鑰：

   要申請計量許可證，您需要提供您的公鑰和私鑰。當您從 Aspose 購買計量許可證時，您可以獲得這些金鑰。代替`"*****"`使用您實際的公鑰和私鑰。

   ```csharp
   Aspose.Html.Metered metered = new Aspose.Html.Metered();
   metered.SetMeteredKey("YOUR_PUBLIC_KEY", "YOUR_PRIVATE_KEY");
   ```

### 載入 HTML 文件：

   使用 HTMLDocument 類別從資料目錄載入 HTML 文件。確保更換`"input.html"`與實際的檔案名稱。

   ```csharp
   HTMLDocument document = new HTMLDocument(dataDir + "input.html");
   ```

### 列印內部 HTML：

   載入HTML文件後，您可以存取文件內部的HTML並將其列印到控制台進行驗證。

   ```csharp
   Console.WriteLine(document.Body.InnerHTML);
   ```

就是這樣！您已成功將計量許可證套用到 .NET 專案並載入了 HTML 文件。

## 結論

在本教學中，我們示範如何使用 Aspose.HTML for .NET 應用計量授權。透過執行以下步驟，您可以將 Aspose.HTML 無縫整合到 .NET 應用程式中以進行 HTML 操作。

---

## 常見問題 (FAQ)

### 什麼是 Aspose.HTML for .NET 中的計量許可證？
計量許可證可讓您根據您的使用情況以即用即付的方式支付 Aspose.HTML 費用。這是一種靈活的許可選項。

### 在哪裡可以獲得 Aspose.HTML for .NET 的計量許可證？
您可以從以下位置購買計量許可證[提出購買](https://purchase.aspose.com/buy).

### 如何下載 Aspose.HTML for .NET 函式庫？
您可以從以下位置下載該程式庫[這裡](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET 是否有免費試用選項？
是的，您可以從以下位置取得免費試用版[這裡](https://releases.aspose.com/).

### 我可以在哪裡獲得有關 Aspose.HTML for .NET 的支援或提出問題？
您可以加入社群並尋求支持[Aspose 論壇](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
