---
date: 2026-05-04
description: 學習如何使用 Aspose.HTML for Java 執行 HTML 轉 PNG 轉換、攔截 Java 網路請求，以及處理 Java 中的斷開連結。
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: 在 Aspose.HTML 中使用訊息處理程式
second_title: Java HTML Processing with Aspose.HTML
title: 使用 Aspose.HTML 訊息處理程式在 Java 中將 HTML 轉換為 PNG
url: /zh-hant/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML 訊息處理程式的 Java HTML 轉 PNG 轉換

## HTML 轉 PNG 轉換簡介
在本教學中，您將了解 **如何將 HTML 轉換為 PNG**，同時使用 Aspose.HTML for Java 優雅地處理遺失的資源。我們將示範如何建立一個指向不存在圖片的簡易 HTML 頁面，設定 **自訂訊息處理程式** 以 **攔截網路請求**，配置 **網路服務**，載入文件，最後執行 **HTML 轉圖像轉換**。完成後，您將擁有一套完整的模式，既能 **處理 Java 中的斷裂連結**，又能產生高品質的 PNG 輸出——非常適合報告、縮圖或電子郵件預覽。

## 快速解答
- **訊息處理程式的功能是什麼？** 它會攔截網路操作（例如圖片請求），讓您對 404 等狀態碼作出回應。  
- **Aspose.HTML 能將 HTML 轉換為 PNG 嗎？** 可以——`Converter.convertHTML` 只需一次呼叫即可完成轉換。  
- **此範例是否需要授權？** 臨時授權可移除評估限制；正式使用則需永久授權。  
- **支援哪個 Java 版本？** 任意 JDK 8 以上（範例在 JDK 11 上執行）。  
- **我可以設定網路服務嗎？** 當然可以——使用 `configuration.getService(INetworkService.class)` 來加入您的處理程式。  

## 什麼是 HTML 轉 PNG 轉換？
HTML 轉 PNG 轉換會將網頁（或 HTML 片段）渲染成點陣圖像。當您需要動態內容的靜態預覽、為電子報產生縮圖，或將網頁存檔為圖像時，這項功能非常實用。

## 為何在 Java 中使用訊息處理程式攔截網路請求？
訊息處理程式讓您對每個網路請求擁有 **細緻的控制**——無論是圖片、CSS、JavaScript 或字型檔案。透過攔截這些請求，您可以 **記錄遺失的資源**、提供備援內容，甚至重新嘗試下載失敗的檔案，從而使您的 HTML 處理流程 **穩健**且 **可投入生產**。

## 前置條件
在開始之前，請確保您已準備好以下項目：

1. **Java Development Kit (JDK)** – 從 [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。  
2. **Aspose.HTML for Java** – 從 [Aspose releases page](https://releases.aspose.com/html/java/) 取得程式庫。  
3. **IDE** – IntelliJ IDEA、Eclipse 或 NetBeans 均可。  
4. **Basic Java knowledge** – 您應熟悉類別、try‑with‑resources 以及例外處理。  
5. **Temporary License** – 若您使用試用版，請取得 [temporary license](https://purchase.aspose.com/temporary-license/) 以避免浮水印。  

## 匯入套件
首先，匯入我們在檔案處理時需要的 Java I/O 類別。其餘的 Aspose 類別稍後會以全限定名稱引用，保持匯入清單簡潔。

```java
import java.io.IOException;
```

## 步驟 1：準備 HTML 程式碼
我們建立一段最小的 HTML 片段，故意引用不存在的圖片。當引擎嘗試取得該資源時，將觸發我們的處理程式。

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
現在我們建立一個 **自訂訊息處理程式**，檢查每個網路請求的 HTTP 狀態。若回應不是 `200`，我們會記錄友善的警告。請注意最後呼叫 `invoke(context);`——此呼叫會將請求轉交給鏈中的下一個處理程式，避免遞迴。

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
配置完成後，我們載入 *document.html*。引擎現在會使用我們的網路服務，因此缺失的圖片請求會被剛才加入的處理程式攔截。

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
以下是 **html to image conversion** 流程的核心。`Converter.convertHTML` 方法接受已載入的 `HTMLDocument`、可選的 `ImageSaveOptions`（您可以在此調整 DPI 或品質），以及輸出檔名。

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

## 常見問題與解決方案
- **處理程式遞迴** – 只呼叫一次 `invoke(context);` 以避免無限迴圈。  
- **缺少授權** – 若未持有有效授權，輸出的 PNG 會出現浮水印。  
- **檔案路徑錯誤** – 載入 `document.html` 時使用絕對路徑或正確設定工作目錄。  
- **不支援的資源類型** – 確認您想攔截的資源（圖片、CSS 等）確實由 HTML 引擎請求。  

## 常見問答

**Q: 我可以串接多個訊息處理程式嗎？**  
A: 可以，您可以將多個處理程式加入 `network.getMessageHandlers()` 集合；它們會依加入的順序執行。

**Q: 處理程式也會對 CSS 或腳本資源生效嗎？**  
A: 當然會——任何由 HTML 引擎發出的網路請求（圖片、CSS、JS、字型）都會經過此處理程式。

**Q: 我該如何在發送前變更 HTTP 請求？**  
A: 實作一個在呼叫 `invoke(context)` 前修改 `context.getRequest()` 的處理程式。

**Q: 有沒有方法對特定 URL 抑制警告？**  
A: 在處理程式內檢查 `context.getRequest().getRequestUri()`，並根據條件跳過記錄。

**Q: 這些 API 需要哪個版本的 Aspose.HTML？**  
A: 此程式碼相容於 Aspose.HTML for Java 22.10 及以上版本。

---

**最後更新：** 2026-05-04  
**測試環境：** Aspose.HTML for Java 24.11  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}