---
date: 2026-03-24
description: '學習如何使用 Aspose.HTML for Java 設定圖片背景顏色、自訂頁面尺寸，並將 EPUB 轉換為圖片。#JavaDevelopment
  #WebDevelopment #DocumentConversion'
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: 設定 EPUB 轉換為圖像的背景顏色
url: /zh-hant/java/converting-epub-to-pdf/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 設定 EPUB 轉換為影像的圖像背景顏色

在現代的網頁與文件工作流程中，**Aspose.HTML for Java** 為您提供將 EPUB 等電子書轉換為點陣圖的能力，同時讓您完整掌控視覺輸出。透過結合 **set image background color** 選項與 **custom page size**，您可以產生與 UI 元件、列印版面或任何後續處理需求完美匹配的影像。本指南將逐步說明整個流程——從先決條件到最終轉換——讓您能夠自信地 **convert EPUB to image**。

## 快速解答
- **custom page size** 會影響什麼？它定義了產生影像的寬度與高度（以像素為單位）。  
- **可以將 EPUB 轉換成哪種格式？** 任何 `ImageSaveOptions` 支援的影像格式，例如 JPEG、PNG 或 BMP。  
- **如何設定影像背景顏色？** 使用 `options.setBackgroundColor(Color.getAliceBlue())`（或任何其他 `Color`）。  
- **開發是否需要授權？** 免費試用版可用於評估；正式上線需商業授權。  
- **需要哪個 Java 版本？** 需要 Java 8 或以上，並搭配 Aspose.HTML for Java 函式庫。

## 什麼是 “set image background color”？

設定影像背景顏色會告訴渲染引擎在繪製頁面內容之前，以哪種顏色填滿畫布。當來源 EPUB 含有透明元素，或您希望所有頁面都有統一的背景時，這特別有用。

## 如何在 Java 中設定影像背景顏色與自訂頁面大小？

以下我們將步驟逐一說明。每一步都包含簡短說明以及您將使用的完整程式碼片段（程式碼本身保持與原教學相同）。

### 先決條件
1. **Java 開發環境** – 已安裝 JDK 8 或更新版本。  
2. **Aspose.HTML for Java** – 從官方網站 [here](https://releases.aspose.com/html/java/) 下載函式庫。  
3. **程式碼編輯器** – IntelliJ IDEA、Eclipse、VS Code，或您偏好的任何 IDE。  
4. **基本的 Java 知識** – 熟悉 Java 語法與專案設定。  
5. **熱情** – 準備好探索自訂頁面大小與其他影像儲存選項。  

現在您已準備就緒，讓我們進入實作階段。

## 匯入套件

首先，匯入渲染與轉換所需的類別。

### 步驟 1：匯入 Aspose.HTML 類別

```java
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
```

這些匯入讓您可以使用 `ImageSaveOptions`、頁面佈局物件以及 `Converter` 工具。

## 範例說明：將 EPUB 轉換為影像

以下是逐步說明 **如何將 EPUB 轉換**，同時套用 **custom page size** 與 **set image background color** 選項。

### 步驟 2：開啟 EPUB 檔案

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
```

`FileInputStream` 讀取來源 EPUB。將 `"input.epub"` 替換為您自己的檔案路徑。

### 步驟 3：以自訂頁面大小初始化 ImageSaveOptions

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
Size size = new Size(Length.fromPixels(3000), Length.fromPixels(1000));
anyPage.setSize(size);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Custom Page Size**：`Size` 以寬度 3000 像素、高度 1000 像素建立。依需求調整這些數值以符合您的版面需求。  
- **Set Image Background Color**：`Color.getAliceBlue()` 會以淡藍色填滿畫布；您也可以替換為任何想要的 `Color`，例如 PNG 透明度可使用 `Color.getTransparent()`。

### 步驟 4：將 EPUB 轉換為影像

```java
Converter.convertEPUB(fileInputStream, options, Resources.output("output.jpg"));
```

`convertEPUB` 方法使用已設定的 `options` 執行轉換，結果會儲存為 `output.jpg`。

> **專業提示：** 若需要 **epub 轉 png**，請以 `ImageFormat.Png` 建立 `ImageSaveOptions`，而非 `ImageFormat.Jpeg`。

恭喜！您已成功 **convert epub to image**，同時掌控頁面尺寸與背景顏色。

## 如何設定頁面大小（custom page size java）——深入探討

若每本 EPUB 需要不同的頁面大小，您可以根據內容的 CSS 或中繼資料動態計算尺寸。`PageSetup` 物件可在多次轉換間重複使用，只需在每次呼叫 `Converter.convertEPUB` 前調整 `Size` 即可。

## 常見問題與解決方案

| 問題 | 原因 | 解決方式 |
|-------|--------|-----|
| 輸出影像被裁切 | 自訂頁面大小小於內容 | 增加 `Size` 的寬度/高度，或啟用 `options.setFitToPage(true)`。 |
| 背景顯示為黑色 | 未設定顏色或格式不支援 | 確保在轉換前呼叫 `options.setBackgroundColor(...)`。 |
| 轉換時拋出 `NullPointerException` | 缺少 `Resources.input` 檔案 | 確認路徑正確且 EPUB 檔案存在。 |

## 常見問答 (FAQs)

### 1. 在哪裡可以找到 Aspose.HTML for Java 的文件說明？
您可以在 [here](https://reference.aspose.com/html/java/) 存取文件說明。它提供完整資訊與範例，協助您快速上手。

### 2. 是否提供 Aspose.HTML for Java 的免費試用版？
是的，您可在 [here](https://releases.aspose.com/) 下載免費試用版。讓您在購買前先體驗函式庫功能。

### 3. 如何取得 Aspose.HTML for Java 的臨時授權？
若需要臨時授權，您可在 [here](https://purchase.aspose.com/temporary-license/) 取得。

### 4. Aspose.HTML for Java 能處理其他文件轉換嗎？
可以，Aspose.HTML for Java 支援多種轉換，包括 HTML → PDF、HTML → image 等。

### 5. Aspose.HTML for Java 是否適合新手與有經驗的開發者？
絕對適合！新手可從簡單範例入手，進階使用者則能利用完整 API 處理複雜工作流程。

**Additional Q&A**

**Q: 我可以將多個 EPUB 頁面轉換為獨立的影像嗎？**  
A: 可以。對頁面索引使用迴圈，為每頁調整 `options.setPageSetup(pageSetup)`，並重複呼叫 `Converter.convertEPUB`。

**Q: 如何調整 JPEG 輸出的影像品質？**  
A: 在呼叫轉換前設定 `options.setQuality(90)`（值介於 0‑100）。

**Q: 函式庫是否支援透明背景？**  
A: 對於 PNG 輸出，可使用 `options.setBackgroundColor(Color.getTransparent())`。

## 相關主題您可能感興趣
- **如何將 EPUB 轉換為 PNG** – 改用 `ImageFormat.Png`，並可選擇設定透明背景。  
- **批次轉換多個 EPUB 檔案** – 迭代 EPUB 目錄，重複使用同一個 `ImageSaveOptions` 實例。  
- **優化網頁影像大小** – 使用 `options.setQuality()` 與 `options.setResolution()`，在視覺品質與檔案大小之間取得平衡。

## 結論

Aspose.HTML for Java 為 EPUB 轉影像提供細緻的控制。透過設定 **custom page size**、**set image background color** 以及其他 `ImageSaveOptions`，您可以產生完全符合專案視覺需求的影像。歡迎嘗試不同格式、尺寸與背景顏色，並在應用程式中探索 Aspose.HTML for Java 更廣泛的功能。

如有任何問題或需要協助，請前往 [Aspose.HTML community](https://forum.aspose.com/) 尋求支援。

---

**Last Updated:** 2026-03-24  
**Tested With:** Aspose.HTML for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}