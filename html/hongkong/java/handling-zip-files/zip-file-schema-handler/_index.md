---
date: 2026-06-29
description: 了解如何使用 Aspose.HTML for Java 讀取 zip entry java 並從 zip 壓縮檔提供檔案。本指南展示了 java
  zip archive streaming 以及使用自訂 schema handler 的 java zip file response。
keywords:
- read zip entry java
- serve files from zip
- java zip archive streaming
- custom schema handler
- Aspose.HTML for Java
linktitle: Aspose.HTML 中的 ZIP File Schema Handler
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to read zip entry java using Aspose.HTML for Java and serve
    files from zip archives. This guide shows java zip archive streaming and java
    zip file response with a custom schema handler.
  headline: Read ZIP Entry Java – ZIP Handler in Aspose.HTML
  type: TechArticle
- description: Learn how to read zip entry java using Aspose.HTML for Java and serve
    files from zip archives. This guide shows java zip archive streaming and java
    zip file response with a custom schema handler.
  name: Read ZIP Entry Java – ZIP Handler in Aspose.HTML
  steps:
  - name: '**Java Development Kit (JDK) 8+** installed.'
    text: '**Java Development Kit (JDK) 8+** installed.'
  - name: An IDE such as **IntelliJ IDEA**, **Eclipse**, or **NetBeans**.
    text: An IDE such as **IntelliJ IDEA**, **Eclipse**, or **NetBeans**.
  - name: '**Aspose.HTML for Java** library – download it **[here](https://releases.aspose.com/html/java/)**
      and add the JAR(s) to your project’s classpath.'
    text: '**Aspose.HTML for Java** library – download it **[here](https://releases.aspose.com/html/java/)**
      and add the JAR(s) to your project’s classpath.'
  - name: Basic familiarity with Java collections and exception handling.
    text: Basic familiarity with Java collections and exception handling.
  type: HowTo
- questions:
  - answer: The current implementation targets ZIP files only. You can adapt the logic
      by swapping `java.util.zip.ZipFile` with a library that supports RAR/TAR, but
      you’ll need to handle their specific entry‑lookup APIs.
    question: Can I use this handler for other archive formats like RAR or TAR?
  - answer: A corrupted archive triggers an `IOException` during `GetFile`. Catch
      the exception and return a 500 response with a diagnostic message to keep the
      application stable.
    question: What happens if the ZIP file is corrupted?
  - answer: No. This handler is read‑only; it streams entries to the client. For write‑back
      scenarios you would need a separate writer component that creates a new ZIP
      file.
    question: Is it possible to modify files within the ZIP archive using this handler?
  - answer: Implement HTTP range requests by checking the `Range` header and sending
      partial streams. This allows browsers to request file chunks, reducing perceived
      latency.
    question: How can I improve performance when serving very large files?
  - answer: Yes, provided each request creates its own `ZipFile` instance (as shown).
      Avoid sharing mutable state between threads.
    question: Can this handler be used safely in a multi‑threaded environment?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: 閱讀 ZIP Entry Java – Aspose.HTML 中的 ZIP 處理程式
url: /zh-hant/java/handling-zip-files/zip-file-schema-handler/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 讀取 ZIP 條目 Java – Aspose.HTML 中的 ZIP 處理器

## 介紹
當您建立需要直接從封裝的 ZIP 檔案中提取圖像、腳本或樣式表的 Web 應用程式時，您不想先將壓縮檔解壓縮到暫存資料夾，浪費時間。**Read zip entry java** 讓您將請求的條目直接串流至 HTTP 回應，保持低記憶體使用量與最小延遲。在 Aspose.HTML for Java 中，這透過 `ZIPFileSchemaMessageHandler` 實現，這是一個能理解 `zip-file:` URI 方案並即時提供內容的自訂 schema 處理器。以下我們將逐步說明完整實作，討論串流的重要性，並示範如何使此處理器足以應付生產環境的工作負載。

## 快速回答
- **此處理器的功能是什麼？** 它直接從 ZIP 壓縮檔提供檔案，無需解壓至磁碟，使用串流回應。  
- **使用哪種 URI 方案？** `zip-file:` – 一個在 Aspose.HTML 網路層註冊的自訂方案。  
- **我需要授權嗎？** 免費試用可用於開發；商業授權則是生產環境的必要條件。  
- **能處理大型檔案嗎？** 能 – 它串流條目內容，即使是數百 MB 的資產也能以低記憶體佔用處理。  
- **它是執行緒安全的嗎？** 處理器本身是無狀態的；只需確保底層 ZIP 檔案不會同時被修改。

## 什麼是 read zip entry java？
在 Java 中讀取 ZIP 條目表示在 `.zip` 容器內定位特定檔案並以串流方式取得其資料。`java.util.zip.ZipFile` 類別提供隨機存取讀取，讓您能在不載入整個壓縮檔的情況下抽取單一條目。Aspose.HTML 允許您透過自訂 schema 處理器將此邏輯插入 HTTP 管線，將簡單的 `zip-file:` URL 轉換為完整的 HTTP 回應。

## 為何使用 Java ZIP 壓縮檔串流？
串流 ZIP 條目可避免將整個壓縮檔載入記憶體，這對高流量應用或大型資產（如高解析度影像或影片片段）至關重要。Aspose.HTML 能提供最高 **2 GB** 的檔案，並能處理包含數萬條目的壓縮檔，同時保持 JVM 堆積使用量低。ZIP 格式的隨機存取特性意味著只會讀取所需的位元組。

## 前置條件
1. 已安裝 **Java Development Kit (JDK) 8+**。  
2. 如 **IntelliJ IDEA**、**Eclipse** 或 **NetBeans** 等 IDE。  
3. **Aspose.HTML for Java** 程式庫 – 前往 **[here](https://releases.aspose.com/html/java/)** 下載，並將 JAR 加入專案的 classpath。  
4. 具備 Java 集合與例外處理的基本知識。

## 匯入套件
以下的匯入讓您可以使用 Aspose.HTML 的網路工具、MIME 處理以及標準的 Java I/O 類別。

```java
import com.aspose.html.MimeType;
import com.aspose.html.net.INetworkOperationContext;
import com.aspose.html.net.ResponseMessage;
import com.aspose.html.net.StreamContent;
import com.aspose.html.utils.Stream;
```

## 步驟 1：建立 ZIP 檔案 Schema 處理器類別
`CustomSchemaMessageHandler` 是 Aspose.HTML 用於處理自訂 URI 方案的基底類別。透過繼承它，我們可以註冊 `zip-file` 方案並指向磁碟上的實體 ZIP 壓縮檔。

**定義說明：** `ZIPFileSchemaMessageHandler` 為具體的處理器，將 `zip-file:` URI 映射至特定 ZIP 檔案內的條目。  

建構子會儲存 ZIP 壓縮檔的絕對路徑，並使用 `MessageHandlerRegistry` 註冊該方案。此註冊使處理器在 Aspose.HTML 內部的請求路由器中全域可用。

```java
public class ZIPFileSchemaMessageHandler extends CustomSchemaMessageHandler {
    private final String archive;
    protected ZIPFileSchemaMessageHandler(String archive) {
        super("zip-file");
        this.archive = archive;
    }
}
```

## 步驟 2：覆寫 `invoke` 方法
`invoke` 方法會在每個符合 `zip-file:` 方案的請求時被呼叫。它從請求 URI 中提取相對路徑，查找對應的條目，並建立一個串流條目資料回傳給客戶端的 HTTP 回應。

**定義說明：** `invoke` 是 Aspose.HTML 在需要處理自訂方案請求時呼叫的入口點。  

若請求的條目不存在，方法會回傳 404 回應並附上說明文字訊息。否則，它會建立 `MessageResponse` 物件，設定適當的 MIME 類型，並附加條目串流。

```java
@Override
public void invoke(INetworkOperationContext context) {
    String pathInsideArchive = context.getRequest().getRequestUri().getPathname().substring(1).replaceAll("\\\\", "/");
    Stream stream = GetFile(pathInsideArchive);
    if (stream != null) {
        // If the file is found, return it as a response
        ResponseMessage response = new ResponseMessage(200);
        response.setContent(new StreamContent(stream));
        response.getHeaders().getContentType().setMediaType(MimeType.fromFileExtension(context.getRequest().getRequestUri().getPathname()));
        context.setResponse(response);
    } else {
        // If the file is not found, return a 404 error
        context.setResponse(new ResponseMessage(404));
    }
    // Invoke the next handler in the chain
    invoke(context);
}
```

## 步驟 3：實作 `GetFile` 方法
`GetFile` 使用標準的 `java.util.zip.ZipFile` API 於壓縮檔內定位條目，並以 Aspose `Stream` 回傳。這就是實際執行 **read zip entry java** 操作的地方。

**定義說明：** `GetFile` 開啟 ZIP 壓縮檔，尋找符合請求路徑的 `ZipEntry`，並將其 `InputStream` 包裝成 Aspose `Stream`。  

此方法亦根據檔案副檔名判斷正確的 MIME 類型，確保瀏覽器能正確呈現圖像、腳本或樣式。

```java
Stream GetFile(String path) {
    try (ZipFile zipFile = new ZipFile(archive)) {
        ZipEntry entry = zipFile.getEntry(path);
        if (entry != null) {
            InputStream inputStream = zipFile.getInputStream(entry);
            return new Stream(inputStream);
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
    return null;
}
```

## 常見問題與解決方案
| 問題 | 發生原因 | 解決方式 |
|-------|----------------|-----|
| **`IOException` on large files** | 預設緩衝區可能太小。 | 將緩衝區大小調大或使用 `java.nio` 通道進行串流。 |
| **Incorrect MIME type** | `MimeType.fromFileExtension` 可能對未知副檔名回傳 `application/octet-stream`。 | 根據已知的內容類型手動設定 MIME 類型。 |
| **Thread‑safety concerns** | 在多執行緒間共享單一 `ZipFile` 實例可能導致 `ZipException`。 | 在 `GetFile` 中開啟新的 `ZipFile`（如示範），確保每個請求都有自己的句柄。 |
| **Missing entry returns 404** | 路徑正規化問題（例如，前導斜線）。 | `substring(1)` 會去除前導斜線；請確保請求 URI 與壓縮檔內部結構相符。 |

### 效能提示
- **重複使用緩衝區：** 配置可重用的 64 KB `byte[]`，在串流複製迴圈中傳入，以減少 GC 壓力。  
- **啟用延遲載入：** 處理大於 4 GB 的壓縮檔時，將 `ZipFile` 的 `useZip64` 標誌設為 `true`。  
- **快取 MIME 對映：** 建立常見副檔名到 MIME 類型的靜態映射，以避免重複查詢。

## 常見問答

**Q: 我可以將此處理器用於其他壓縮格式，如 RAR 或 TAR 嗎？**  
A: 目前的實作僅針對 ZIP 檔案。您可以透過將 `java.util.zip.ZipFile` 換成支援 RAR/TAR 的函式庫來調整邏輯，但必須自行處理它們的條目查找 API。

**Q: 若 ZIP 檔案損毀會發生什麼情況？**  
A: 損毀的壓縮檔會在 `GetFile` 時拋出 `IOException`。請捕捉例外並回傳 500 回應，附上診斷訊息以保持應用程式穩定。

**Q: 能否使用此處理器修改 ZIP 壓縮檔內的檔案？**  
A: 不能。此處理器為唯讀，僅將條目串流至客戶端。若需寫回，必須使用建立新 ZIP 檔的獨立寫入元件。

**Q: 如何在提供極大檔案時提升效能？**  
A: 透過檢查 `Range` 標頭並傳送部分串流來實作 HTTP range 請求。這讓瀏覽器能請求檔案片段，降低感知延遲。

**Q: 此處理器能安全用於多執行緒環境嗎？**  
A: 可以，只要每個請求如示範般建立自己的 `ZipFile` 實例。避免在執行緒間共享可變狀態。

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [Aspose.HTML for Java 中的 ZIP 壓縮檔訊息處理器](/html/java/handling-zip-files/zip-archive-message-handler/)
- [如何使用 Aspose.HTML for Java 建立自訂 schema 處理器](/html/java/custom-schema-message-handling/custom-schema-message-handler/)
- [Aspose.HTML for Java 中的自訂 Schema 篩選與訊息處理](/html/java/custom-schema-message-handling/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}