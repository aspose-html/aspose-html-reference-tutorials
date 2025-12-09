---
date: 2025-12-05
description: 學習如何使用 Aspose.HTML for Java 建立 HTML 檔案、管理網路資源，並在自訂錯誤處理下將 HTML 轉換為 PNG。
linktitle: Set Up Network Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 建立 HTML 檔案與設定網路服務 (Aspose.HTML Java)
url: /zh-hant/java/configuring-environment/setup-network-service/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 HTML 檔案與設定網路服務 (Aspose.HTML Java)

## Introduction
如果你需要 **create html file** 從網路抓取圖片，然後將該頁面轉成圖片，你來對地方了。在本教學中，我們會逐步說明如何設定 Aspose.HTML for Java、**manage network resources**、使用自訂錯誤處理程式處理遺失的資產、**convert html to png**，最後 **clean up resources** 以確保應用程式保持健康。無論你是要建立報表引擎、自動縮圖產生器，或只是試驗 HTML‑to‑image 轉換，這裡示範的模式都能為你省下時間與麻煩。

## Quick Answers
- **What is the first step?** Create an HTML file that references network‑hosted images.  
  **第一步是什麼？** 建立一個參考網路託管圖片的 HTML 檔案。  
- **Which class configures networking?** `com.aspose.html.Configuration`.  
  **哪個類別負責設定網路？** `com.aspose.html.Configuration`。  
- **How do I capture load errors?** Add a custom `MessageHandler` to the `INetworkService`.  
  **如何捕捉載入錯誤？** 為 `INetworkService` 加入自訂的 `MessageHandler`。  
- **What output format does this example produce?** A PNG image (`output.png`).  
  **此範例產生的輸出格式為何？** PNG 圖片（`output.png`）。  
- **Do I need to release objects?** Yes – call `dispose()` on both the document and configuration.  
  **是否需要釋放物件？** 需要 – 在文件與設定上皆呼叫 `dispose()`。

## Prerequisites
在深入設定之前，先確保你已具備所有必要的環境：

- **Java Development Kit (JDK)** 1.8 或更新版本。  
- **Aspose.HTML for Java** 函式庫 – 從 [官方發佈頁面](https://releases.aspose.com/html/java/) 下載最新版本。  
- **IDE**（依你喜好選擇，如 IntelliJ IDEA、Eclipse、NetBeans 等）。  
- 具備基本的 Java 語法與 Maven/Gradle 專案設定知識。

## Import Packages
首先，你需要在 Java 專案中匯入所需的套件。這些套件讓你能使用 Aspose.HTML for Java 的各項功能。

```java
import java.io.IOException;
```

這些匯入是我們將討論功能的基礎，請確保它們正確放置於 Java 檔案的最前端。

## Step 1: Create an HTML File with Network‑Dependent Images
要 **create html file** 並引用外部資源，請撰寫一小段程式碼，插入幾個指向公開可用圖片的 `<img>` 標籤。

```java
String code = "<img src=\"https://docs.aspose.com/svg/net/drawing-basics/filters-and-gradients/park.jpg\" >\r\n" +
        "<img src=\"https://docs.aspose.com/html/net/missing1.jpg\" >\r\n" +
        "<img src=\"https://docs.aspose.com/html/net/missing2.jpg\" >\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

此 HTML 檔案是網路服務的入口點；當文件載入時，圖片會透過 HTTP 取得。

## Step 2: Initialize the Configuration Object
現在讓我們建立 **configuration**，用來放置網路服務的設定。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

`Configuration` 物件是你指定 Aspose.HTML 如何處理網路流量、記錄與錯誤處理的地方。

## Step 3: Add a Custom Error Message Handler
自訂的 `MessageHandler` 能讓你看見遺失圖片或逾時等問題。

```java
com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
com.aspose.html.net.MessageHandler logHandler = new LogMessageHandler();
network.getMessageHandlers().addItem(logHandler);
```

透過附加 `LogMessageHandler`，所有與網路相關的警告或錯誤都會被捕捉，使除錯變得簡單。

## Step 4: Load the HTML Document with the Configuration
網路服務就緒後，載入先前建立的 HTML 檔案。

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

當文件載入時，Aspose.HTML 會使用自訂的網路設定，並在有問題時呼叫我們的訊息處理程式。

## Step 5: Convert HTML to PNG
現在我們要 **convert html to png**，將載入的頁面（包括成功取得的圖片）轉為點陣圖。

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

最終會得到單一的 PNG 檔案（`output.png`），可嵌入其他地方或提供給使用者。

## Step 6: Clean Up Resources
適當的資源管理至關重要。轉換完成後，釋放物件以 **clean up resources**，避免記憶體洩漏。

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

可以把它想成餐後洗碗——若資源未釋放，日後可能導致效能問題。

## Common Issues and Solutions
| 問題 | 為何發生 | 解決方法 |
|------|----------|----------|
| 圖片載入失敗 | 網路逾時或 URL 錯誤 | 檢查 URL、透過 `NetworkService` 設定增加逾時時間，或在 `LogMessageHandler` 中加入備援邏輯。 |
| PNG 為空白 | 文件在轉換前尚未完全載入 | 確認使用包含自訂處理程式的設定建立 `HTMLDocument`；若使用非同步載入，可選擇呼叫 `document.waitForLoad()`。 |
| 記憶體不足錯誤 | HTML 過大或大量高解析度圖片 | 使用 `ImageSaveOptions.setMaxWidth/MaxHeight` 限制輸出尺寸，或及時釋放中間物件。 |

## Frequently Asked Questions

**Q: 在 Aspose.HTML for Java 中設定網路服務的主要目的為何？**  
A: 它讓你 **manage network resources** 如遠端圖片、腳本或樣式表，並提供錯誤處理與記錄的控制權。

**Q: 我可以使用此設定產生其他影像格式嗎（例如 JPEG、BMP）？**  
A: 可以，只要將 `ImageSaveOptions` 的 format 屬性改為想要的輸出類型即可。

**Q: 自訂的 `MessageHandler` 與預設的 logger 有何不同？**  
A: 自訂處理程式允許你將訊息導向自己的記錄框架、過濾特定警告或觸發警報，而預設 logger 只會輸出到主控台。

**Q: 必須在文件與設定上都呼叫 `dispose()` 嗎？**  
A: 必須。釋放會釋除原生資源，並 **cleans up resources**，即清除程式庫內部保留的資源。

**Q: 我可以在哪裡找到更多 Java 中將 HTML 轉為影像的範例？**  
A: 請參閱 Aspose.HTML for Java 文件與官方 GitHub 範例頁面，裡面有 PDF 轉換、SVG 渲染、批次處理等其他使用案例。

---

**最後更新：** 2025-12-05  
**測試環境：** Aspose.HTML for Java 24.12（最新）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}