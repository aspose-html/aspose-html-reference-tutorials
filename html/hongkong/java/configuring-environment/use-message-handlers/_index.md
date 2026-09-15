---
date: 2026-02-10
description: 學習如何使用 Aspose 處理 Java 中的斷開連結、將 HTML 轉換為 PNG，以及使用 Aspose.HTML for Java
  載入 HTML 文件。
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 在 Java 中使用 Aspose.HTML 訊息處理器將 HTML 轉換為 PNG
url: /zh-hant/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML 訊息處理程式在 Java 中將 HTML 轉換為 PNG

## 介紹
在本教學中，您將學習 **如何將 HTML 轉換為 PNG**，同時使用 Aspose.HTML for Java 優雅地處理遺失的資源。我們將示範如何建立一個指向不存在圖片的簡易 HTML 頁面，設定 **custom message handler** 以 **intercept network requests**，配置 **network service**，載入文件，最後執行 **html to image conversion**。完成後，您將掌握一套同時 **handle broken links java** 與產生高品質 PNG 輸出的可靠模式——非常適合報告、縮圖或電子郵件預覽。

## 快速解答
- **訊息處理程式的作用是什麼？** 它會攔截網路操作（例如圖片請求），讓您能對 404 等狀態碼作出回應。  
- **Aspose.HTML 能將 HTML 轉換為 PNG 嗎？** 能——`Converter.convertHTML` 只需一次呼叫即可完成轉換。  
- **此範例是否需要授權？** 臨時授權可移除評估限制；正式使用時需購買永久授權。  
- **支援哪個 Java 版本？** 任意 JDK 8 以上皆可（範例在 JDK 11 上執行）。  
- **我可以設定網路服務嗎？** 當然可以——使用 `configuration.getService(INetworkService.class)` 來加入您的處理程式。

## 前置條件
1. **Java Development Kit (JDK)** – 從 [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。  
2. **Aspose.HTML for Java** – 從 [Aspose releases page](https://releases.aspose.com/html/java/) 取得程式庫。  
3. **IDE** – IntelliJ IDEA、Eclipse 或 NetBeans 都可使用。  
4. **Basic Java knowledge** – 您應該熟悉類別、try‑with‑resources 以及例外處理。  
5. **Temporary License** – 若您使用試用版，請取得 [temporary license](https://purchase.aspose.com/temporary-license/) 以避免浮水印。

## 匯入套件
首先，匯入我們在檔案處理上需要的 Java I/O 類別。其餘 Aspose 類別稍後會以完整限定名稱使用，保持匯入清單簡潔。

```java
import java.io.IOException;
```

## 步驟 1：準備 HTML 程式碼
我們建立一段最小的 HTML 片段，特意引用一個不存在的圖片。當引擎嘗試取得該資源時，會觸發我們的處理程式。

```java
String code = "<img src='missing.jpg'>";
```

## 步驟 2：將 HTML 程式碼寫入檔案
接著，我們將片段寫入 *document.html*。使用 try‑with‑resources 區塊可確保 `FileWriter` 正確關閉。

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## 步驟 3：撰寫自訂訊息處理程式
現在我們建立一個 **custom message handler**，檢查每個網路請求的 HTTP 狀態碼。若回應不是 `200`，我們會記錄友善的警告。請留意最後呼叫的 `invoke(context);`——它會將請求轉交給鏈中的下一個處理程式，避免遞迴。

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

## 步驟 4：設定網路服務
為了讓 Aspose.HTML 知道我們的處理程式，我們從 `Configuration` 實例取得 **network service**，並將處理程式加入其集合。這一步即是 **configure network service** 以實現自訂行為。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## 步驟 5：載入 HTML 文件
設定完成後，我們載入 *document.html*。引擎現在會使用我們的 network service，因此缺失的圖片請求會被剛才加入的處理程式攔截。

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

## 步驟 6：將 HTML 轉換為 PNG
以下是 **html to image conversion** 流程的核心。`Converter.convertHTML` 方法接受已載入的 `HTMLDocument`、可選的 `ImageSaveOptions`（可在此調整 DPI 或品質），以及輸出檔名。

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## 步驟 7：清理資源
良好的 Java 實踐是釋放所有原生資源。`finally` 區塊確保即使拋出例外，`Configuration` 仍會被釋放。

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## 為何使用訊息處理程式？
訊息處理程式讓您對每個網路請求都有 **細緻的控制**——無論是圖片、CSS、JavaScript 或字型檔。與其讓函式庫靜默失敗，您可以記錄遺失的資源、提供備援內容，甚至重新嘗試請求。這使您的 HTML 處理流程 **穩健**、**可投入生產**，且更易除錯。

## 常見問題與解決方案
- **Handler recursion** – 只呼叫一次 `invoke(context);` 以避免無限迴圈。  
- **Missing license** – 若未持有有效授權，輸出的 PNG 會出現浮水印。  
- **Incorrect file paths** – 載入 `document.html` 時請使用絕對路徑或正確設定工作目錄。  
- **Unsupported resource types** – 確認您想攔截的資源（圖片、CSS 等）確實是 HTML 引擎所請求的。

## 常見問答

**Q: 我可以串接多個訊息處理程式嗎？**  
A: 可以，您可以將多個處理程式加入 `network.getMessageHandlers()` 集合；它們會依加入的順序依次執行。

**Q: 處理程式也會作用於 CSS 或腳本資源嗎？**  
A: 當然會——HTML 引擎發出的任何網路請求（圖片、CSS、JS、字型）都會經過此處理程式。

**Q: 我該如何在發送前變更 HTTP 請求？**  
A: 實作一個在呼叫 `invoke(context)` 前修改 `context.getRequest()` 的處理程式。

**Q: 有辦法對特定 URL 抑制警告嗎？**  
A: 在處理程式內檢查 `context.getRequest().getRequestUri()`，並根據條件跳過記錄。

**Q: 這些 API 需要哪個版本的 Aspose.HTML？**  
A: 此程式碼相容於 Aspose.HTML for Java 22.10 及之後的版本。

## 結論
現在您已擁有一個完整的端對端範例，示範 **how to convert HTML to PNG**，同時使用 **custom message handler** 來 **intercept network requests** 以及 **handle broken links java**。透過設定 network service、載入文件並呼叫轉換器，您可以在任何 Java 應用程式中可靠地產生 PNG 縮圖或全頁截圖。

---

**最後更新：** 2026-02-10  
**測試環境：** Aspose.HTML for Java 24.11  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}