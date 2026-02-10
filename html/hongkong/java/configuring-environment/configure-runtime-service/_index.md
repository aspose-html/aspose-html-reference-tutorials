---
date: 2026-02-10
description: 了解如何在 Aspose.HTML for Java 中設定逾時、配置 Runtime Service 以將 HTML 轉換為 PNG、避免無限迴圈，並提升效能。
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

## Introduction
如果你正在尋找在使用 Aspose.HTML for Java 時 **如何設定逾時** 以控制腳本執行，你來對地方了。控制腳本執行不僅能防止無限迴圈，還能讓你更快 **將 html 轉換為 png**，並保持應用程式的回應性。在本教學中，我們將逐步說明如何配置 Runtime Service、限制腳本執行，最終從 HTML 產生 PNG 圖片而不會使程式掛起。

## 在 Aspose.HTML Runtime Service 中設定逾時的方法
了解 Runtime Service 的目的有助於說明為何逾時是必要的。該服務充當客戶端程式碼的沙盒，讓你能在 JavaScript 失控、佔用全部 CPU 前將其停止。設定逾時可保護伺服器免於拒絕服務攻擊，並確保 **html to png conversion** 在可預測的時間內完成。

## Quick Answers
- **Runtime Service 的功能是什麼？** 它讓你在處理 HTML 時控制腳本執行時間並管理資源。  
- **如何為 JavaScript 設定逾時？** 使用 `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`。  
- **我能防止無限迴圈嗎？** 可以——逾時會停止超過設定限制的迴圈。  
- **這會影響 HTML‑to‑PNG 轉換嗎？** 不會，轉換會在腳本完成或被逾時終止後繼續。  
- **需要哪個版本的 Aspose.HTML？** 只要使用 Aspose 下載頁面上的最新發佈版即可。  

## Prerequisites
在深入細節之前，請確保你已具備以下條件：

1. **Java Development Kit (JDK)** – 從 [Oracle 的網站](https://www.oracle.com/java/technologies/javase-downloads.html) 下載並安裝。  
2. **Aspose.HTML for Java Library** – 從 [Aspose 釋出頁面](https://releases.aspose.com/html/java/) 取得最新版本。  
3. **IDE** – IntelliJ IDEA、Eclipse 或 NetBeans 都可使用。  
4. **基本的 Java 與 HTML 知識** – 讀懂程式碼範例所必需。  

## Import Packages
首先，匯入你需要的類別。`java.io.IOException` 的匯入是處理檔案時必須的。

```java
import java.io.IOException;
```

## Step 1: Create an HTML File with JavaScript Code
我們先產生一個簡單的 HTML 檔案，內含 JavaScript 迴圈。如果不設定逾時，該迴圈會無限執行，這正好可用來示範 Runtime Service。

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

## Step 2: Set Up the Configuration Object
接著，建立一個 `Configuration` 實例。此物件是所有 Aspose.HTML 服務（包括 Runtime Service）的基礎。

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Step 3: Configure the Runtime Service
這裡就是實際 **設定逾時** 的地方。透過從 Configuration 取得 `IRuntimeService`，即可定義 JavaScript 的執行上限。

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` 將腳本執行上限設定為 **5 秒**，有效 **防止無限迴圈**。  
- 同時也 **限制任何繁重的客戶端程式碼** 執行時間。  

## Step 4: Load the HTML Document with the Configuration
現在使用包含逾時規則的 Configuration 載入 HTML 檔案。

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- 文件會遵守先前設定的逾時，因此無限迴圈會在 5 秒後被停止。  

## Step 5: Convert the HTML to PNG
在文件安全載入後，我們即可 **將 html 轉換為 png**。轉換僅在腳本完成或被逾時終止後才會執行。

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` 告訴 Aspose.HTML 輸出 PNG 圖像。  
- 產生的檔案 **runtime-service_out.png** 會顯示已渲染的 HTML，且不會卡住。  

## Step 6: Clean Up Resources
最後，釋放物件以釋放記憶體並避免泄漏。

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

## 為什麼這很重要
設定逾時不僅是安全網，還能直接提升 **html to png conversion** 工作流程的可靠性。當你將 Aspose.HTML 整合到處理使用者產生 HTML 的 Web 服務時，惡意腳本可能會無限佔用執行緒。適度的逾時（例如 5 秒）讓合法腳本有足夠時間執行，同時阻止濫用行為。

## Common pitfalls & troubleshooting
- **逾時設定過短** – 資源豐富、結構複雜的頁面可能需要更長的上限。如果發現過早終止，請增加 `TimeSpan` 的數值。  
- **未釋放資源** – 忘記呼叫 `dispose()` 會導致原生記憶體泄漏，特別是在迴圈中處理大量文件時。  
- **Configuration 物件錯誤** – 必須從用來載入文件的同一個 `Configuration` 實例取得 `IRuntimeService`，否則逾時不會生效。  

## Frequently Asked Questions

**Q: Aspose.HTML for Java 的 Runtime Service 有什麼用途？**  
A: 它讓你控制腳本執行時間，協助 **防止無限迴圈**，並保持轉換的回應性。

**Q: 我要如何下載 Aspose.HTML for Java？**  
A: 從 [releases page](https://releases.aspose.com/html/java/) 取得最新版本。

**Q: 是否必須釋放 `document` 與 `configuration` 物件？**  
A: 必須，釋放可釋出原生資源並防止記憶體泄漏。

**Q: 我可以將 JavaScript 逾時設定為非 5 秒的值嗎？**  
A: 當然可以——只要將 `TimeSpan.fromSeconds()` 的參數改成符合你需求的時間即可。

**Q: 若遇到問題，該去哪裡尋求協助？**  
A: 前往 [Aspose.HTML 論壇](https://forum.aspose.com/c/html/29) 尋求社群與官方人員的協助。

---

**最後更新:** 2026-02-10  
**測試環境:** Aspose.HTML for Java 24.11 (latest)  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}