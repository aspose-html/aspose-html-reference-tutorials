---
date: 2025-12-08
description: 學習如何使用 Aspose.HTML for Java 將 HTML 轉換為 PNG，同時處理斷開的連結，並透過自訂訊息處理程式捕捉缺失的資源。
language: zh-hant
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 如何將 HTML 轉換為 PNG 並在 Aspose.HTML for Java 中使用訊息處理程式
url: /java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML for Java 轉換 HTML 為 PNG – 使用訊息處理程式

## 介紹  
在本教學中，您將學習 **如何使用 Aspose.HTML for Java 將 HTML 轉換為 PNG**，同時了解如何使用自訂訊息處理程式 **處理斷裂連結或遺失資源**。我們將逐步示範建立簡易 HTML 檔案、寫入磁碟、載入檔案，以及捕捉任何網路錯誤——非常適合需要在正式環境 Java 應用程式中執行可靠 **html to image conversion** 的開發者。

## 快速回答
- **本教學涵蓋什麼內容？** 轉換 HTML 為 PNG 以及使用訊息處理程式處理遺失資源。  
- **使用哪個函式庫？** Aspose.HTML for Java。  
- **需要授權嗎？** 建議使用臨時授權以進行試用建置。  
- **可以從 Java 寫入 HTML 檔案嗎？** 可以——請參考「write html file java」步驟。  
- **處理程式會捕捉斷裂連結嗎？** 當然會；它會記錄任何非 200 的回應。

## 什麼是 Aspose.HTML 的訊息處理程式？  
訊息處理程式是介入網路堆疊的掛鉤，讓您 **在遺失資源（例如斷裂的圖片 URL）導致例外之前** 先捕捉它。透過檢查回應的狀態碼，您可以記錄、取代或重試請求，從而完整掌控網路操作。

## 為什麼要將 HTML 轉換為 PNG？  
將 HTML 轉為影像可用於產生縮圖、電子郵件預覽，或在不需要完整 PDF 轉換時的 PDF‑類似快照。Aspose.HTML 提供快速、伺服器端的 **html to image conversion** 引擎，且不需瀏覽器。

## 前置條件
1. **Java Development Kit (JDK)** – 從 [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。  
2. **Aspose.HTML for Java** – 從 [Aspose releases page](https://releases.aspose.com/html/java/) 取得最新 JAR。  
3. **IDE** – IntelliJ IDEA、Eclipse 或 NetBeans。  
4. **基本的 Java 知識** – 您應熟悉 try‑with‑resources 以及物件釋放。  
5. **臨時授權**（可選）– 透過 [temporary license](https://purchase.aspose.com/temporary-license/) 避免試用限制。

## 匯入套件
在開始之前，先匯入所需的 Java 類別：

```java
import java.io.IOException;
```

這些匯入讓我們能使用檔案 I/O 與 Aspose.HTML 的網路 API。

## 步驟 1：寫入 HTML 檔案（write html file java）  
首先，建立一段小型 HTML 片段，內含一個 **不存在的** 圖片 URL，以測試處理程式。

```java
String code = "<img src='missing.jpg'>";
```

## 步驟 2：將 HTML 持久化至磁碟  
將上述片段儲存為 `document.html`。稍後會使用 Aspose.HTML 引擎載入此檔案。

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## 步驟 3：建立自訂訊息處理程式（catch missing resource）  
現在定義一個處理程式，檢查 HTTP 狀態碼。若不是 `200`，則記錄友善訊息。

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

## 步驟 4：將處理程式註冊至網路服務  
將自訂處理程式加入 Aspose.HTML 的網路服務，使其參與每一次請求。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## 步驟 5：載入 HTML 文件（load html document java）  
設定完成後，載入 HTML 檔案。遺失的圖片會觸發剛才加入的處理程式。

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

## 步驟 6：轉換 HTML 為 PNG（convert html to png）  
最後，將載入的文件轉換為 PNG 影像。這展示了完整的 **html to image conversion** 工作流程。

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## 步驟 7：清理資源  
務必釋放 `Configuration` 物件，以釋放原生資源並避免記憶體泄漏。

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## 常見問題與技巧
- **遞迴呼叫 invoke：** 自訂處理程式必須在您的邏輯之後呼叫 `invoke(context);`，才能讓鏈中的其他處理程式繼續執行。忘記此步會導致其他處理程式被阻斷。  
- **遺失授權警告：** 若未使用有效授權，轉換可能會加上浮水印或限制輸出大小。  
- **路徑問題：** `document.html` 已寫入工作目錄，或提供絕對路徑。

## 常見問答

**Q: 什麼是 Aspose.HTML for Java？**  
A: 它是一套功能強大的函式庫，讓 Java 開發者在不使用瀏覽器的情況下建立、操作與轉換 HTML 文件。

**Q: 為什麼在 Aspose.HTML for Java 中使用訊息處理程式？**  
A: 它們讓您 **處理斷裂連結**、記錄遺失資源，或即時修改請求/回應。

**Q: 可以串接多個訊息處理程式嗎？**  
A: 可以——將每個處理程式加入 `network.getMessageHandlers()` 清單；它們會依加入順序依次執行。

**Q: 必須釋放 Configuration 與 HTMLDocument 物件嗎？**  
A: 必須；釋放可釋出原生記憶體，防止長時間執行的應用程式發生泄漏。

**Q: 除了遺失圖片，處理程式還能管理哪些錯誤？**  
A: 任何非 200 的 HTTP 回應——逾時、404 頁面、驗證失敗等，都可以被攔截並處理。

## 結論  
現在您已掌握一個完整、可投入生產環境的 **HTML 轉 PNG** 範例，同時透過 Aspose.HTML for Java **處理斷裂連結**與 **捕捉遺失資源**。將此模式整合至更大型的專案，即可細緻控制網路操作，並產生可靠的 HTML 影像快照。

---

**最後更新：** 2025-12-08  
**測試環境：** Aspose.HTML for Java 24.12（最新）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}