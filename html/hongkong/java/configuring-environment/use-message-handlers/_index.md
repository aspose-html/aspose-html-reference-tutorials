---
date: 2025-12-10
description: 學習如何使用 Aspose 處理 Java 中的斷開連結、將 HTML 轉換為 PNG，以及使用 Aspose.HTML for Java
  在 Java 中載入 HTML 文件。
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 如何在 Java 中使用 Aspose.HTML 訊息處理器
url: /zh-hant/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.HTML 訊息處理程式

## Introduction
在本教學中，我們將逐步示範 **how to use aspose** 來處理 HTML 中缺失的資源。我們會建立一個簡單的 HTML 文件，引用一個遺失的圖片，附加自訂訊息處理程式，並示範如何在 **load html document java** 時優雅地處理斷裂的連結。最後，您還會看到如何使用 Aspose.HTML **convert html to png**，為您提供在 Java 中 HTML 轉圖片的完整示例。

## Quick Answers
- **訊息處理程式的主要目的為何？** 用於攔截網路操作並對如缺失資源等狀態碼作出回應。  
- **Aspose.HTML 能將 HTML 轉換為 PNG 嗎？** 可以，使用 `Converter.convertHTML` 即可執行 HTML 到影像的轉換。  
- **此範例是否需要授權？** 臨時授權可移除評估限制；正式環境需使用永久授權。  
- **支援哪個 Java 版本？** 任意 JDK 8 以上（本教學使用 JDK 11）。  
- **是否能處理多個斷裂連結？** 當然可以——您可以串接多個處理程式以因應不同情況。

## Prerequisites
在深入逐步指南之前，請先確保您已具備以下所有項目：

1. Java Development Kit（JDK）：確保您的系統已安裝 JDK。可從 [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。  
2. Aspose.HTML for Java：需要安裝 Aspose.HTML for Java。可從 [Aspose releases page](https://releases.aspose.com/html/java/) 下載。  
3. IDE：使用您喜愛的 Java 整合開發環境（IDE），如 IntelliJ IDEA、Eclipse 或 NetBeans。  
4. Java 基礎知識：熟悉 Java 程式設計是順利跟隨本教學的前提。  
5. 臨時授權：若使用 Aspose.HTML 試用版，建議取得 [temporary license](https://purchase.aspose.com/temporary-license/) 以避免開發期間的限制。

## Import Packages
在開始之前，請確保已在 Java 專案中匯入必要的套件。以下為您需要的關鍵匯入語句：
```java
import java.io.IOException;
```
這些匯入讓您能使用處理網路操作、建立 HTML 文件以及執行 HTML‑to‑PNG 轉換所需的類別與方法。

## Step 1: Prepare the HTML Code
首先，我們需要一段簡單的 HTML 片段，內含對圖片檔案的引用。我們會刻意引用一個不存在的圖片，以觸發錯誤處理機制。
```java
String code = "<img src='missing.jpg'>";
```
此程式碼會產生指向 `missing.jpg` 的 `<img>` 標籤。由於圖片遺失，網路服務會回傳非 200 的狀態碼，我們的自訂處理程式將捕捉到它。

## Step 2: Write the HTML Code to a File
接著，我們需要將 HTML 片段寫入檔案，以便 Aspose.HTML 載入作為文件。
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
透過 `FileWriter` 我們將 HTML 儲存為 **document.html**。此檔案將成為稍後 **load html document java** 步驟的來源。

## Step 3: Create a Custom Message Handler
現在讓我們建立一個自訂訊息處理程式，於圖片找不到時作出回應。該處理程式會檢查 HTTP 狀態碼並輸出友善訊息。
```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```
`invoke` 方法會檢查 `context.getResponse().getStatusCode()`。若不是 **200**，我們會輸出明確的警告，指出檔案遺失。最後的 `invoke(context);` 呼叫會將控制權傳遞給鏈中的下一個處理程式。

## Step 4: Configure the Network Service
為了讓 Aspose.HTML 知悉我們的處理程式，我們透過 `Configuration` 類別將其註冊至網路服務。
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
此處我們建立 `Configuration` 實例，取得 `INetworkService`，並將自訂處理程式加入其集合。這確保在任何網路請求（例如載入圖片）時都會執行此處理程式。

## Step 5: Load the HTML Document
設定完成後，我們即可載入先前建立的 HTML 檔案。此步驟示範 **load html document java**，同時遺失的圖片會觸發我們的處理程式。
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
`HTMLDocument` 建構子同時接受檔案路徑與自訂的 `configuration`。當文件解析 `<img>` 標籤時，網路服務會嘗試取得 `missing.jpg`，收到 404 後，我們的處理程式會印出警告。

## Step 6: Convert HTML to PNG
為了展示 Aspose.HTML 更廣泛的功能，我們將把載入的文件轉換為 PNG 影像。這是一個典型的 **convert html to png** 情境。
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` 接受 `HTMLDocument`、可選的 `ImageSaveOptions`（可設定 DPI、品質等）以及輸出檔名。最終會得到渲染後 HTML 的點陣圖。

## Step 7: Clean Up Resources
在任何 Java 應用程式中，妥善的資源管理都是必須的。我們會釋放 `Configuration` 與 `HTMLDocument`，以避免記憶體洩漏。
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
將清理程式碼放在 `finally` 區塊中，可確保即使先前拋出例外仍會執行。

## Why Use Message Handlers?
訊息處理程式讓您能對網路操作（例如 **handle broken links java**）進行精細控制。與其讓函式庫靜默失敗，您可以記錄、重試、替換資源或提供備援內容，使 HTML 處理更穩健且適合上線使用。

## Common Issues and Solutions
- **處理程式遞迴** – 確保只呼叫一次 `invoke(context);`，以免產生無限迴圈。  
- **授權遺失** – 若未持有有效授權，轉換結果可能會帶有浮水印。  
- **檔案路徑錯誤** – 載入 `document.html` 時請使用絕對路徑或正確設定工作目錄。

## Frequently Asked Questions

**Q: 我可以串接多個訊息處理程式嗎？**  
A: 可以，您可以將多個處理程式加入 `network.getMessageHandlers()` 集合，它們會依加入的順序依次執行。

**Q: 處理程式也會對 CSS 或腳本資源生效嗎？**  
A: 當然會——HTML 引擎發出的任何網路請求（圖片、CSS、JS、字型）皆會經過此處理程式。

**Q: 如何在發送前變更 HTTP 請求？**  
A: 實作一個在呼叫 `invoke(context)` 前修改 `context.getRequest()` 的處理程式。

**Q: 有沒有方法對特定 URL 抑制警告？**  
A: 在處理程式內檢查 `context.getRequest().getRequestUri()`，並根據條件跳過記錄。

**Q: 需要哪個版本的 Aspose.HTML 才能使用這些 API？**  
A: 此程式碼相容於 Aspose.HTML for Java 22.10 及之後的版本。

## Conclusion
以上即為在 Java 中使用 **how to use aspose** 訊息處理程式的完整指南。我們說明了如何建立 HTML 檔案、將自訂處理程式連結至 **handle broken links java**、載入文件，以及執行 **convert html to png**。透過此模式，您能自信地管理遺失資源、套用自訂政策，並在任何 Java 應用程式中擴充 Aspose.HTML 的網路功能。

**最後更新：** 2025-12-10  
**測試環境：** Aspose.HTML for Java 24.11  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}