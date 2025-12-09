---
date: 2025-12-09
description: 學習如何使用 Java 建立 HTML 檔案、設定 Runtime Service、將 HTML 轉換為 PNG，並在防止無限迴圈的同時提升應用程式效能。
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 如何在 Java 中建立 HTML 檔案並在 Aspose.HTML 中設定 Runtime Service
url: /zh-hant/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.HTML for Java 中配置 Runtime Service

## 介紹
有沒有想過如何 **create html file java** 專案能跑得更快、更可靠？無論你是在構建複雜的網站入口網站，還是僅僅在玩 HTML 文件，控制腳本執行都能產生巨大的差異。在本教學中，你將學習如何在 Java 中建立 HTML 檔案、設定 Aspose.HTML 的 Runtime Service 以 **limit script execution**，以及 **convert html to png**——同時 **improving application performance** 並 **preventing infinite loops**。讓我們開始吧！

## 快速解答
- **Runtime Service** 做什麼？它會限制 JavaScript 的執行時間，停止執行過長的腳本。  
- **Why create an HTML file in Java first?** 它提供一個具體的文件，讓你測試 Runtime Service 與轉換功能。  
- **How long can a script run before it’s stopped?** 本範例中我們設定 5 秒的逾時時間。  
- **Can I generate a PNG from the HTML?** 可以——Aspose.HTML 能渲染頁面並儲存為 PNG 圖片。  
- **Will this improve my app’s performance?** 絕對會；限制失控腳本可減少 CPU 使用率與記憶體壓力。

## 前置條件
在深入細節之前，先確保你已備妥所有必需品。

1. **Java Development Kit (JDK)** – 確保系統已安裝 JDK。你可以從 [Oracle's website](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。  
2. **Aspose.HTML for Java Library** – 從 [Aspose releases page](https://releases.aspose.com/html/java/) 下載最新版本。  
3. **Integrated Development Environment (IDE)** – 需要使用如 IntelliJ IDEA、Eclipse 或 NetBeans 等 IDE 來編寫與執行 Java 程式碼。  
4. **Basic Knowledge of Java and HTML** – 熟悉 Java 程式設計與基本 HTML，才能順利跟隨教學。

## 匯入套件
首先，先談談匯入必要的套件。要使用 Aspose.HTML for Java，需要匯入多個類別。這些匯入很重要，因為它們讓你能存取 Aspose.HTML 所提供的各種功能與服務。

```java
import java.io.IOException;
```

## 步驟 1：使用 JavaScript 程式碼建立 HTML 檔案
第一步是 **create html file java**，其中包含一個簡單的 JavaScript 迴圈。若不加以干預，這個迴圈 (`while(true) {}`) 會永遠執行下去，非常適合用來示範 Runtime Service 如何 **prevent infinite loops**。

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

## 步驟 2：設定 Configuration 物件
HTML 檔案準備好後，接下來要設定一個 `Configuration` 物件。此物件將作為管理 Runtime Service 及其他設定的核心。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## 步驟 3：設定 Runtime Service
現在就是關鍵所在！我們將設定 Runtime Service，將 **limit script execution** 為安全的時間長度。這可防止 JavaScript 迴圈卡住你的應用程式。

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

## 步驟 4：使用 Configuration 載入 HTML 文件
Runtime Service 設定完成後，我們使用相同的 configuration 載入 HTML 文件。這可確保檔案內的腳本遵守我們設定的逾時時間。

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

## 步驟 5：將 HTML 轉換為 PNG
如果無法將 HTML 文件轉成可視化的內容，那還有什麼用？在此步驟中，我們 **convert html to png**，產生可嵌入其他地方或用於測試的點陣圖像。

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

## 步驟 6：清理資源
最後，我們清理資源以避免記憶體洩漏。釋放 `document` 與 `configuration` 物件可釋放 Aspose.HTML 所佔用的所有原生資源。

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

## 為何這很重要
- **Improve application performance**：透過停止失控腳本，釋放 CPU 時間給其他任務。  
- **Prevent infinite loops**：Runtime Service 的逾時機制可阻止腳本鎖住應用程式。  
- **Generate PNG from HTML**：轉換為 PNG 可用於建立縮圖、預覽或網頁內容的存檔快照。  

## 常見問題與解決方案
| Issue | Solution |
|-------|----------|
| 腳本仍然執行時間過長 | 確認從用於載入文件的相同 `Configuration` 中取得 `IRuntimeService`。 |
| PNG 輸出為空白 | 確保 HTML 檔案正確寫入，且 `runtime-service.html` 的路徑正確。 |
| 大型文件導致記憶體不足錯誤 | 增加 JVM 堆積大小或將 HTML 分成較小的區塊處理。 |

## 常見問答

**Q: Runtime Service 在 Aspose.HTML for Java 中的目的為何？**  
A: Runtime Service 允許你 **limit script execution**，協助 **prevent infinite loops** 並保持應用程式的回應性。

**Q: 如何下載 Aspose.HTML for Java？**  
A: 你可以從 [releases page](https://releases.aspose.com/html/java/) 下載最新版本的 Aspose.HTML for Java。

**Q: 是否需要釋放 `document` 和 `configuration` 物件？**  
A: 是的，釋放這些物件對於釋放資源與防止記憶體洩漏至關重要。

**Q: 可以將 JavaScript 逾時設定為除 5 秒以外的其他值嗎？**  
A: 當然可以！只要修改 `TimeSpan.fromSeconds()` 的參數，即可設定任何符合需求的逾時值。

**Q: 若在使用 Aspose.HTML for Java 時遇到問題，該向哪裡尋求支援？**  
A: 如需支援，可前往 [Aspose.HTML forum](https://forum.aspose.com/c/html/29)。

**最後更新：** 2025-12-09  
**測試環境：** Aspose.HTML for Java 24.11  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}