---
category: general
date: 2026-04-03
description: 學習如何在 Aspose.HTML Java 中使用沙盒來設定使用者代理、設定尺寸，並即時取得視口大小。提供完整程式碼、說明與技巧。
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: zh-hant
og_description: 了解如何在 Aspose.HTML Java 中使用沙盒設定使用者代理、設定尺寸，並即時取得視口大小。完整指南，附程式碼與最佳實踐。
og_title: 如何使用 Sandbox – 設定使用者代理與取得視口大小
tags:
- AsposeHTML
- Java
- Sandbox
title: 如何使用沙盒 – 設定使用者代理與取得視口大小
url: /zh-hant/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Sandbox – 設定 User Agent 及取得 Viewport 大小

有沒有想過在使用 Aspose.HTML for Java 渲染 HTML 時 **如何使用 sandbox**？也許你在嘗試模擬特定螢幕尺寸或需要偽造 user‑agent 字串，使頁面表現得像是從行動瀏覽器存取。

好消息是 sandbox API 正好可以做到這一點，且在頁面載入後還能取得計算出的 viewport 大小。在本教學中，我們將一步步說明如何建立 sandbox、設定尺寸、設定自訂 user agent、載入遠端頁面，最後讀取 viewport 尺寸。完成後，你將了解 **如何設定尺寸**、**如何取得 viewport**，以及這些步驟為何對可靠的無頭渲染如此重要。

> **快速上手：** 你將擁有一個可執行的 Java 類別，能在幾秒鐘內印出類似 `Viewport: 1280×800` 的結果。

---

## 需要的條件

- **Aspose.HTML for Java** 版本 24.6 或更新（我們使用的 API 於 24.5 版首次推出）。  
- Java 17+ 開發套件（任何近期的 JDK 都可）。  
- IDE 或簡易文字編輯器——不需要特別的外掛。  
- 若要載入外部 URL（例如 `https://example.com`），需要有網路連線。

就這樣。並不一定要使用 Maven/Gradle，只要手動將 JAR 放入 classpath 亦可。

---

## 如何使用 Sandbox – 概觀

sandbox 會將渲染引擎與主機作業系統隔離，讓你可以定義虛擬螢幕（寬度、高度、DPI）以及自訂的 **user agent** 字串。它就像一個完全存在於記憶體中的小型瀏覽器視窗。之後當你向 `HTMLDocument` 取得預設視圖時，引擎會回報根據 sandbox 設定計算出的 **viewport 大小**。

以下是高階流程：

1. **建立** `DocumentSandbox`，並設定寬度、高度、DPI 與 user‑agent。  
2. **載入** 在該 sandbox 內的 `HTMLDocument`。  
3. **查詢** 文件的預設視圖以取得 viewport 大小。  

接下來逐步說明每個步驟。

---

## Step 1: Create a Sandbox and Set Size

首先，我們啟動一個 sandbox，並告訴它虛擬螢幕的大小。這就是回答 **如何設定尺寸** 的關鍵步驟。

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **專業提示：** 若在測試響應式版面，試著使用 `360` 的窄寬來模擬手機，或 `1920` 的寬度來模擬桌面。sandbox 會遵守你設定的 DPI，故高密度螢幕（例如 144 DPI）會影響使用 `device-pixel-ratio` 的 media query。

---

## Step 2: Set User Agent for the Sandbox

為什麼要使用自訂 **user agent**？某些網站會根據報告的瀏覽器提供不同的標記或腳本。呼叫 `setUserAgent` 後，你可以讓頁面以為自己是由 Chrome、Firefox 或行動裝置存取。

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

現在頁面會認為自己正於 iPhone 上渲染。若需要 **設定 user agent** 回預設值，只要再次使用先前的 “AsposeHTML/24.6 …” 字串即可。

---

## Step 3: Load an HTML Document Inside the Sandbox

sandbox 準備好後，我們即可載入任意 URL 或本機 HTML 檔案。`HTMLDocument` 建構子接受 sandbox 作為第二個參數，將兩者綁定。

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

`try‑with‑resources` 區塊確保文件能正確釋放，釋放 Aspose.HTML 在底層分配的原生資源。

---

## Step 4: Get Viewport Size from the Document

以下就是你期待已久的時刻：取得渲染引擎計算出的 **viewport 大小**。這回答了 **如何取得 viewport** 的問題。

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

執行程式後，你應該會看到類似以下的輸出：

```
Viewport: 1280×800
```

如果在 Step 1 中更改了 sandbox 的尺寸，印出的數字會反映新的設定——非常適合用於驗證響應式斷點的自動化測試。

---

## Full Working Example

以下是完整、可直接執行的類別，將所有步驟整合在一起。將程式碼貼到名為 `SandboxExample.java` 的檔案中，將 Aspose.HTML JAR 加入 classpath，然後執行 `java SandboxExample`。

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**預期輸出**（假設使用上述 sandbox 設定）：

```
Viewport: 1280×800
```

若在 sandbox 中設定了不同的寬度/高度，輸出會相應變化——這正是測試響應式設計時所需要的。

---

## Edge Cases & Common Questions

### 如果頁面使用 `window.innerWidth` 而非 CSS media queries，會怎樣？

sandbox 的虛擬螢幕尺寸同時影響 CSS 版面配置與 JavaScript 的 `window.innerWidth/innerHeight`。因此透過 JavaScript **取得 viewport** 時，會回傳與 Java 主控台相同的數值。

### 可以同時執行多個 sandbox 嗎？

可以。每個 `DocumentSandbox` 實例都是獨立的，你可以建立執行緒池，為每個執行緒分配不同尺寸的 sandbox，並行渲染多頁。只要確保 JAR 本身是執行緒安全的（它們確實是）。

### DPI 設定會影響影像縮放嗎？

絕對會。較高的 DPI 會讓一個 CSS 像素對應更多裝置像素，從而使高解析度圖片看起來更銳利。若在測試 Retina 風格的資源，建議使用 `sandbox.setDeviceDpi(144)`。

### 如何處理自簽的 HTTPS 憑證

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}