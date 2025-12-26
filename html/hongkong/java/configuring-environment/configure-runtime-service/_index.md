---
date: 2025-12-10
description: 學習如何在 Aspose.HTML for Java 中設定逾時，配置 Runtime Service 以將 HTML 轉換為 PNG，防止無限迴圈，並提升效能。
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 如何在 Aspose.HTML for Java 執行時服務中設定逾時
url: /zh-hant/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose.HTML for Java Runtime Service 中設定逾時

## 簡介
如果你正在尋找在使用 Aspose.HTML for Java 時 **如何設定逾時** 於腳本，恭喜你來對地方了。控制腳本執行不僅能防止無限迴圈，還能讓你更快 **將 html 轉換為 png**，並保持應用程式的回應性。在本教學中，我們將逐步說明如何設定 Runtime Service、限制腳本執行，最終從 HTML 產生 PNG 圖片而不會讓程式卡住。

## 快速答覆
- **Runtime Service 的功能是什麼？** 它讓你在處理 HTML 時控制腳本執行時間並管理資源。  
- **如何為 JavaScript 設定逾時？** 使用 `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`。  
- **我可以防止無限迴圈嗎？** 可以——逾時會停止超出設定上限的迴圈。  
- **這會影響 HTML 轉 PNG 的轉換嗎？** 不會，轉換會在腳本完成或被逾時終止後繼續。  
- **需要哪個版本的 Aspose.HTML？** 只要使用 Aspose 下載頁面上的最新發佈版即可。

## 先決條件
在深入細節之前，請確保你已具備以下項目：

1. **Java Development Kit (JDK)** – 從 [Oracle 的網站](https://www.oracle.com/java/technologies/javase-downloads.html) 下載並安裝。  
2. **Aspose.HTML for Java Library** – 從 [Aspose 發佈頁面](https://releases.aspose.com/html/java/) 取得最新版本。  
3. **IDE** – IntelliJ IDEA、Eclipse 或 NetBeans 都可使用。  
4. **基本的 Java 與 HTML 知識** – 讀懂程式碼範例所必需。

## 匯入套件
首先，匯入你需要的類別。`java.io.IOException` 的匯入是處理檔案所必需的。

```java
import java.io.IOException;
```

## 步驟 1：建立含 JavaScript 程式碼的 HTML 檔案
我們先產生一個簡單的 HTML 檔案，內含 JavaScript 迴圈。如果不設定逾時，該迴圈會無限執行，正好成為 Runtime Service 的示範範例。

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- `while(true) {}` 程式碼代表可能的無限迴圈。  
- `FileWriter` 將 HTML 內容寫入 **runtime-service.html**。

## 步驟 2：設定 Configuration 物件
接著，建立 `Configuration` 實例。此物件是所有 Aspose.HTML 服務（包括 Runtime Service）的核心。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## 步驟 3：設定 Runtime Service
這裡就是實際 **設定逾時** 的地方。透過從 configuration 取得 `IRuntimeService`，我們可以定義 JavaScript 的執行上限。

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` 將腳本執行時間上限設定為 **5 秒**，有效 **防止無限迴圈**。  
- 同時也 **限制任何繁重的客戶端程式碼** 的執行時間。

## 步驟 4：使用 Configuration 載入 HTML 文件
現在使用包含逾時規則的 configuration 載入 HTML 檔案。

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- 文件會遵守先前設定的逾時，因此無限迴圈會在 5 秒後被停止。

## 步驟 5：將 HTML 轉換為 PNG
在文件安全載入後，我們即可 **將 html 轉換為 png**。轉換僅在腳本完成或被逾時終止後才會執行。

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` 告訴 Aspose.HTML 輸出 PNG 圖像。  
- 產生的檔案 **runtime-service_out.png** 顯示已渲染的 HTML，且不會卡住。

## 步驟 6：清理資源
最後，釋放物件以釋放記憶體並避免資源洩漏。

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- 正確的釋放對於長時間執行的應用程式至關重要。

## 結論
你剛剛學會了 Aspose.HTML for Java 中 **設定 JavaScript 逾時**、**防止無限迴圈**，以及安全地 **將 html 轉換為 png**。透過設定 Runtime Service，你可以細緻地控制腳本行為，從而縮短啟動時間並提升轉換的可靠性。請嘗試不同的逾時值以符合你的工作負載，你將會看到明顯的效能提升。

## 常見問題

**Q: Aspose.HTML for Java 的 Runtime Service 有什麼用途？**  
A: 它讓你控制腳本執行時間，協助 **防止無限迴圈**，並保持轉換的回應性。

**Q: 我要如何下載 Aspose.HTML for Java？**  
A: 從 [releases page](https://releases.aspose.com/html/java/) 取得最新版本。

**Q: 是否需要釋放 `document` 與 `configuration` 物件？**  
A: 必須，釋放可釋出原生資源並防止記憶體洩漏。

**Q: 我可以將 JavaScript 逾時設定為非 5 秒的值嗎？**  
A: 當然可以——只要將 `TimeSpan.fromSeconds()` 的參數改成符合你需求的上限即可。

**Q: 若遇到問題，該去哪裡尋求協助？**  
A: 前往 [Aspose.HTML 論壇](https://forum.aspose.com/c/html/29) 尋求社群與官方人員的協助。

---

**最後更新：** 2025-12-10  
**測試環境：** Aspose.HTML for Java 24.11 (latest)  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}