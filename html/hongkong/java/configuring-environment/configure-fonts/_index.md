---
date: 2026-04-05
description: 學習如何從 HTML 生成 PDF、配置字型、套用自訂 CSS、使用臨時授權，並在 Java 中使用 Aspose.HTML 將 HTML
  轉換為 PDF。
keywords:
- generate pdf from html
- convert html pdf java
- add custom fonts pdf
- fonts not showing pdf
linktitle: 在 Aspose.HTML 中設定字型
second_title: Java HTML Processing with Aspose.HTML
title: 從 HTML 產生 PDF：使用 Aspose.HTML for Java 設定字型
url: /zh-hant/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 設定 HTML‑to‑PDF Java 的字型（使用 Aspose.HTML）

## 簡介
在本教學中，您將學習如何使用 Aspose.HTML **從 HTML 產生 PDF**，以及在 Java 中設定 HTML‑to‑PDF 轉換的字型。處理 HTML 文件時，正確的字型設定可確保產生的 PDF 與原始網頁完全相同——保持品牌色彩、排版與版面配置。無論您是建立報告、發票或任何文件產生流程，正確的字型設定都是打造專業 PDF 的關鍵。讓我們一步步完成整個流程，從環境準備到使用自訂字型與 CSS 轉換 HTML 為 PDF。

## 快速解答
- **此教學的主要目的為何？** 使用 Aspose.HTML 在 Java 中設定 HTML‑to‑PDF 轉換的字型。  
- **哪個函式庫負責轉換？** Aspose.HTML for Java（`Converter` 類別）。  
- **我需要授權嗎？** 臨時 Aspose 授權可移除評估限制；正式環境需使用完整授權。  
- **自訂字型應放置於何處？** 放在 `FontsLookupFolder` 所指向的資料夾，例如專案旁的 `fonts` 目錄。  
- **我能自訂 PDF 輸出嗎？** 可以—使用 `PdfSaveOptions` 調整頁面大小、邊距等。

## 什麼是 **generate PDF from HTML** 以及為何字型設定很重要？
**generate PDF from HTML** 的過程會將 HTML 文件渲染成 PDF 頁面。字型是渲染的關鍵，因為它會影響版面、行距與視覺忠實度。將 Aspose.HTML 指向自訂字型資料夾，即可確保 PDF 使用您為網頁設計的精確字型，避免備用字型，保持品牌一致性。

## 為何使用 Aspose.HTML 進行字型設定？
- **精確渲染：** 支援 CSS2.1 以及許多 CSS3 功能，讓您的 HTML 在 PDF 中保持相同外觀。  
- **跨平台：** 可在任何執行 Java 1.8+ 的作業系統上運作。  
- **授權彈性：** 可先使用臨時授權測試，之後切換至正式授權以供生產環境使用。  
- **效能：** 即使是複雜頁面也能快速轉換。

## 前置條件
1. **Java Development Kit (JDK) 1.8+** – 程式碼可在任何現代 JDK 上執行。  
2. **Aspose.HTML for Java** – 從 [Aspose 官方網站](https://releases.aspose.com/html/java/) 下載最新的 JAR。  
3. **IDE** – IntelliJ IDEA、Eclipse 或任何相容 Java 的編輯器。  
4. **基本 Java 知識** – 您應熟悉類別、方法與檔案 I/O。  
5. **Aspose.HTML 授權** – 使用 [臨時授權](https://purchase.aspose.com/temporary-license/) 可解除評估限制。

## 匯入套件
首先，匯入您需要的核心 Java 與 Aspose.HTML 類別。  

```java
import java.io.IOException;
```

這些匯入讓您可以使用檔案處理與 Aspose.HTML API。

## 如何加入自訂字型以產生 PDF
以下說明字型處理的重要性、如何套用自訂 CSS，以及如何 **使用臨時授權** 以在測試解決方案時解鎖完整功能。

## 步驟指南

### 步驟 1：建立 HTML 內容
我們將先產生一個簡單的 HTML 檔，稍後再將其轉換為 PDF。

#### 1.1 撰寫 HTML 程式碼
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

此程式碼片段定義了標題與段落。若需測試其他樣式，可自行擴充 HTML 加入更多元素。

#### 1.2 儲存 HTML 至檔案
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

`FileWriter` 會將字串寫入專案資料夾中的 `user-agent-fontsetting.html`。完成此步驟後，即可取得可供處理的實體 HTML 檔案。

### 步驟 2：設定 Aspose.HTML 環境
現在我們將設定 Aspose.HTML 的 `Configuration` 物件，以控制 HTML 的渲染方式。

#### 2.1 建立 Configuration 實例
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

`Configuration` 物件是自訂渲染選項（如字型處理與使用者代理行為）的入口點。

#### 2.2 取得 User Agent 服務
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

`IUserAgentService` 管理樣式表、字型與其他渲染細節。我們將使用它注入自訂 CSS 並指向字型資料夾。

### 步驟 3：套用自訂樣式與字型
環境就緒後，我們即可新增 CSS 規則，並告訴 Aspose.HTML 在哪裡尋找字型。

#### 3.1 設定自訂 CSS
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

此 CSS 將標題設為棕色、段落設為灰色。您可以在此加入任何有效的 CSS 規則—Aspose.HTML 支援完整的 CSS2.1 規範與許多 CSS3 功能。*(這是一個 **apply custom css** 的範例。)*

#### 3.2 指向自訂字型資料夾
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

將您想使用的 `.ttf` 或 `.otf` 檔案放入專案根目錄下名為 `fonts` 的資料夾。Aspose.HTML 會在渲染時自動載入這些字型。

> **專業提示：** 若有多個字型系列，請將它們整理於子資料夾，並使用分號分隔的方式將每個父資料夾加入 `FontsLookupFolder`。

### 步驟 4：使用 Configuration 載入 HTML 文件
現在載入先前建立的 HTML 檔，並套用剛剛建立的自訂設定。

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

`HTMLDocument` 物件現在代表已套用樣式的 HTML，準備進行轉換。

### 步驟 5：將 HTML 轉換為 PDF
最後，我們執行 **aspose html pdf conversion**，產生遵循自訂字型與樣式的 PDF 檔案。

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

`PdfSaveOptions` 物件讓您調整輸出設定，如頁面大小、壓縮與中繼資料。對於基本轉換，預設選項已足夠。

### 步驟 6：清理資源
適當的釋放可防止記憶體洩漏，特別是在長時間執行的應用程式中處理大量文件時。

#### 6.1 釋放 HTMLDocument
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 釋放 Configuration
```java
if (configuration != null) {
    configuration.dispose();
}
```

這些呼叫會釋放 Aspose.HTML 所分配的原生資源。

## 常見問題與解決方案
| Issue | Solution |
|-------|----------|
| **字型未顯示** | 確認 `fonts` 資料夾已正確被參照且內含有效的 `.ttf`/`.otf` 檔案。若資料夾位於專案目錄外，請使用絕對路徑。 |
| **PDF 顯示空白** | 確保 HTML 檔案路徑正確且檔案可讀取。檢查 `Configuration` 物件是否已傳入 `HTMLDocument` 建構子。 |
| **授權例外** | 在呼叫任何 Aspose API 前先套用臨時或正式授權。將授權檔放入 classpath，並以 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` 載入。 |
| **CSS 渲染異常** | Aspose.HTML 支援大多數 CSS，但不支援所有最新特性（例如 CSS Grid）。請簡化樣式或使用受支援的 CSS 屬性。 |

## 常見問答

**Q: 我可以在 Aspose.HTML for Java 中使用任何字型嗎？**  
A: 可以，任何作業系統支援的 TrueType（`.ttf`）或 OpenType（`.otf`）字型皆可使用。只需將檔案放入您於 `FontsLookupFolder` 設定的資料夾即可。

**Q: 使用 Aspose.HTML for Java 是否需要授權？**  
A: 雖然可以在未授權的情況下評估此函式庫，但 [臨時 Aspose 授權](https://purchase.aspose.com/temporary-license/) 可解除評估限制。正式環境必須使用完整授權。

**Q: 我該如何自訂 PDF 輸出？**  
A: 將已設定好的 `PdfSaveOptions` 實例傳遞給 `convertHTML`。您可以設定頁面大小、邊距、壓縮等。 

**Q: 能否套用更複雜的 CSS 樣式？**  
A: 可以，Aspose.HTML 支援廣泛的 CSS。複雜的選擇器、媒體查詢與偽類如同在瀏覽器中運作，儘管某些最新的 CSS3/4 特性可能尚未完整支援。

**Q: 我在哪裡可以找到更多範例與文件？**  
A: 前往官方的 [Aspose.HTML for Java 文件頁面](https://reference.aspose.com/html/java/)，取得詳細的 API 參考與更多程式碼範例。

**Q: 臨時 Aspose 授權如何影響轉換？**  
A: 臨時授權會解除評估模式下的 10 頁限制與浮水印，讓您能完整測試 **aspose html pdf conversion** 工作流程。

**最後更新：** 2026-04-05  
**測試環境：** Aspose.HTML for Java 24.12（撰寫時的最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}