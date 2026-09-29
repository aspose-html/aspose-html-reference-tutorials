---
category: general
date: 2026-09-29
description: 在 Aspose.HTML for Java 中設定自訂使用者代理，並了解如何設定虛擬螢幕尺寸以獲得精確的 HTML 呈現。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: zh-hant
lastmod: 2026-09-29
og_description: 在 Aspose.HTML for Java 中設定自訂使用者代理，並了解如何設定虛擬螢幕尺寸，以獲得精確的 HTML 呈現。
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: 在 Aspose.HTML for Java 中設定自訂使用者代理與螢幕尺寸
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: 在 Aspose.HTML for Java 中設定自訂使用者代理與螢幕尺寸
url: /zh-hant/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.HTML for Java 中設定自訂使用者代理與螢幕尺寸

如果您在使用 Aspose.HTML for Java 轉換 HTML 時需要 **設定自訂使用者代理**，本教學將一步步說明如何操作。透過設定 sandbox，您亦可 **設定虛擬螢幕大小**，確保版面配置與真實瀏覽器視窗相符。

完成本教學後，您將得到一個完整、可執行的程式範例，能 **指定使用者代理**、**設定螢幕寬度** 以及 **設定螢幕高度**。不需要額外工具——只要 Aspose.HTML for Java 與 Java 8+ 執行環境即可。

## 您將學會

* 如何建立 `SandboxConfiguration` 以隔離渲染環境。  
* 如何 **設定自訂使用者代理** 以及其對響應式網頁的重要性。  
* 如何 **設定虛擬螢幕尺寸**（螢幕寬度與高度）以取得正確的版面配置。  
* 如何在 sandbox 中載入 HTML 檔案並儲存處理後的結果。  
* 常見陷阱與 sandbox 渲染的最佳實踐。

> **先決條件** – 您需要一份有效的 Aspose.HTML for Java 授權、Java 8 或更新版本，以及一個 IDE（IntelliJ IDEA、Eclipse 或 VS Code）。範例使用本機的 `input.html` 檔案，任何可存取的 URL 皆可使用。

![Sandbox 流程圖](sandbox-flow.png "在 Java 中設定自訂使用者代理的範例")

## 步驟 1：建立 sandbox 設定（基礎）

sandbox 能將渲染環境與主機 JVM 隔離，這在您想 **設定自訂使用者代理** 或變更視口大小時相當重要。

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*為什麼需要這一步？*  
`SandboxConfiguration` 包含所有渲染選項，包括 **螢幕尺寸** 與 **使用者代理** 字串。於載入文件前先行設定，可確保 HTML 引擎從第一個請求起就遵循這些設定。

## 步驟 2：設定螢幕尺寸以模擬真實裝置

響應式網站常會讀取 `window.innerWidth` 與 `window.innerHeight`。若要讓引擎認為自己在 1024 × 768 的螢幕上執行，只需要 **設定虛擬螢幕大小**：

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*此設定的重要性* – 若未 **設定螢幕尺寸**，渲染器可能預設為極小的視口，導致 CSS 媒體查詢套用行動版樣式。透過明確 **設定螢幕寬度** 與 **設定螢幕高度**，您即可掌控哪些 CSS 規則會被觸發。

## 步驟 3：指定自訂使用者代理字串

某些網頁會根據使用者代理標頭提供不同內容。要 **指定使用者代理**，只要在 sandbox 設定上設定即可：

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*為什麼要使用自訂使用者代理？*  
自訂字串可以繞過機器人偵測、觸發僅限桌面版的功能，或測試特定瀏覽器版本的行為。Aspose 引擎會在載入外部資源（CSS、圖片、腳本）時，將此值隨每個 HTTP 請求一起傳送。

## 步驟 4：在 sandbox 中載入 HTML 文件

現在 sandbox 已完成全部設定，接著載入 HTML 檔案。接受檔案路徑與 `SandboxConfiguration` 的建構子會自動套用我們先前定義的所有設定。

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

若需從遠端 URL 載入，只要將檔案路徑改為 URL 字串——Aspose.HTML 仍會遵守 **設定自訂使用者代理** 與 **螢幕尺寸**。

## 步驟 5：儲存處理後的輸出

文件載入完成後，您可以以任何支援的格式儲存。此處我們寫入一個 sandbox 化的 HTML 檔案，讓其反映因自訂設定而產生的 DOM 變更。

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

儲存的檔案仍保留相同的標記，但任何查詢 `navigator.userAgent` 或檢查 `window.innerWidth` 的腳本，現在都會看到您提供的值。

## 完整、可執行的範例

將所有步驟整合，即可得到一個可直接複製、貼上並執行的自包含程式。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### 預期輸出

執行程式後會產生 `sandboxed_output.html`。若在瀏覽器中開啟並於主控台檢查 `navigator.userAgent`，會看到 **AsposeHTML/1.0**。同樣地，`window.innerWidth` 會回傳 **1024**，證明 **設定螢幕尺寸** 已如預期生效。

## 常見問題與邊緣案例處理

| 問題 | 解答 |
|----------|--------|
| **如果頁面從不同網域載入額外資源，會怎樣？** | sandbox 會在每個請求中轉送 **自訂使用者代理**，但跨來源政策仍然適用。若需放寬限制，可使用 `sandboxConfig.setAllowCrossDomain(true)`。 |
| **可以在文件載入後再變更螢幕尺寸嗎？** | 不行。螢幕尺寸會在首次布局階段讀取。若要以不同尺寸渲染，必須建立新的 `SandboxConfiguration` 並重新載入文件。 |
| **需要呼叫 `document.close()` 嗎？** | `HTMLDocument` 實作 `AutoCloseable`。使用 try‑with‑resources 區塊可確保正確清理，但在簡單腳本中明確呼叫 `close()` 並非必要。 |
| **這與在 HTTP 客戶端設定使用者代理有何不同？** | 在 sandbox 上設定使用者代理會影響 **所有** 由 HTML 引擎發出的資源請求，而不僅是最初的 HTML 取得。這更貼近真實瀏覽器的行為。 |
| **sandbox 對不受信任的 HTML 安全嗎？** | 安全。sandbox 隔離檔案系統存取，並根據設定限制網路呼叫，降低惡意腳本影響主機 JVM 的風險。 |

## 專業小技巧

* **重複使用設定** – 若需渲染多頁且視口相同，可建立單一 `SandboxConfiguration` 並重複使用，以減少物件建立開銷。  
* **使用日誌除錯** – 開啟 Aspose.HTML 日誌 (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) 可查看哪些資源是以自訂使用者代理取得的。  
* **結合 CSS 媒體查詢** – 調整 **設定螢幕寬度** 後，即可測試響應式設計在平板、手機或大型桌面上的表現，無需開啟實體瀏覽器。

## 結論

現在您已掌握在 Aspose.HTML for Java 渲染 HTML 時 **設定自訂使用者代理** 與 **設定螢幕尺寸** 的方法。透過 sandbox，您可以隔離環境、控制視口，並確保外部資源收到您指定的標頭。此技巧對於測試響應式版面、繞過機器人封鎖，或在自動化流程中重現桌面專屬功能皆相當重要。

接下來，您可以探索 **設定自訂 Cookie** 或 **捕捉渲染截圖** 的方式——這兩項功能同樣是以相同的 sandbox 設定模式為基礎。

祝開發順利！


## 接下來該學什麼？

以下教學與本篇內容緊密相關，皆以相同的技巧為基礎，提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能或探索其他實作方式。

- [High DPI Rendering in Java – Capture Webpage Screenshots with Custom User Agent](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Create HTML File Java & Set Up Network Service (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}