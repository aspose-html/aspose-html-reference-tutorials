---
date: 2026-01-02
description: 學習如何使用 Aspose.HTML for Java 從 EPUB 中提取圖像，並將 EPUB 轉換為圖像檔案，請參考此分步指南。
linktitle: Specifying Custom Stream Provider for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: 從 EPUB 中提取圖像 – 指定自訂流提供者
url: /zh-hant/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 EPUB 提取圖像 – 為 EPUB 轉圖像指定自訂串流提供者

您是否已準備好利用 Aspose.HTML for Java 的強大功能來 **從 EPUB 提取圖像**？本完整指南將一步一步帶領您完成整個流程。無論您是希望 **將 EPUB 轉換為圖像** 格式的資深開發者，或是剛入門，我們都能提供協助。

## 快速解答
- **本教學教什麼？** 如何使用自訂串流提供者從 EPUB 提取圖像並儲存為 JPEG 檔案。  
- **需要哪個函式庫？** Aspose.HTML for Java。  
- **是否需要授權？** 生產環境使用需取得臨時或正式授權。  
- **示範的輸出格式為何？** JPEG（您可以透過變更 `ImageFormat` 改為 PNG、BMP 等）。  
- **程式碼行數多少？** 只有五個簡潔的程式碼區塊，其餘皆為純文字說明。

## 如何使用自訂串流提供者從 EPUB 提取圖像？
在深入程式碼之前，先了解為何 **自訂串流提供者** 很有用。將轉換輸出導向記憶體串流而非檔案系統，可完全掌控圖像資料的存放位置與方式——非常適合 Web 服務、雲端函式，或任何想避免產生暫存檔的情境。

## 前置條件

在開始使用 Aspose.HTML for Java 之前，您需要先準備以下項目：

1. **Java 開發環境** – 確保系統已正確安裝 Java。您可從官方網站下載 Java。  
2. **Aspose.HTML for Java 函式庫** – 您需要取得 Aspose.HTML for Java 函式庫。可在此處取得 [here](https://releases.aspose.com/html/java/)。  
3. **Aspose.HTML 文件** – Aspose.HTML for Java 的文件可在此處取得 [here](https://reference.aspose.com/html/java/)。  
4. **IDE（整合開發環境）** – 您可選擇任何相容 Java 的 IDE，例如 Eclipse 或 IntelliJ IDEA。

## 匯入套件

本節將指導您匯入必要的套件，以便開始使用 Aspose.HTML for Java。

## 開啟現有的 EPUB 檔案

首先，您需要開啟一個現有的 EPUB 檔案以供讀取。以下是操作方式：

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

## 建立 MemoryStreamProvider

若要將 EPUB 轉換為圖像，您需要建立 `MemoryStreamProvider` 的實例：

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

## 轉換 EPUB 為圖像

現在，使用 `MemoryStreamProvider` 將 EPUB 檔案轉換為圖像。此步驟 **將 EPUB 轉為 JPEG**（如有需要，可改為 PNG 或 BMP）。

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

## 取得記憶體串流

您可以取得包含最終圖像資料的記憶體串流：

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

## 將頁面寫入輸出檔案

最後，您需要將每個圖像串流寫入實體檔案。此範例會將頁面分別儲存為 JPEG 檔案：

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## 為何將 EPUB 轉為 JPEG？

- **通用相容性** – JPEG 圖像可在幾乎所有裝置或平台上顯示。  
- **易於整合** – 可在網頁、行動應用或文件中使用提取的圖像，無需 EPUB 閱讀器。  
- **效能** – 渲染靜態圖像比載入完整 EPUB 更快，適用於縮圖或預覽。

## 常見陷阱與技巧

- **記憶體管理** – 必須始終關閉串流（上述已使用 `try‑with‑resources`），以避免記憶體洩漏。  
- **大型 EPUB** – 對於頁數眾多的書籍，建議分批處理串流，以降低記憶體使用量。  
- **圖像品質** – 如需更高解析度的輸出，可調整 `ImageSaveOptions`（例如 `Quality` 屬性）。

## 結論

恭喜！您已成功學會如何使用 Aspose.HTML for Java 以及自訂串流提供者 **從 EPUB 提取圖像**。此強大方法讓您能彈性地在需要的地方處理圖像資料——無論是儲存至磁碟、透過網路傳送，或存入資料庫。

## 常見問答

### 1. 什麼是 Aspose.HTML for Java？

Aspose.HTML for Java 是一套讓 Java 開發者能處理 HTML、EPUB 以及其他網頁相關格式的函式庫。

### 2. 在哪裡可以找到 Aspose.HTML for Java 的文件？

您可在此處取得文件 [here](https://reference.aspose.com/html/java/)。

### 3. 是否提供免費試用？

是的，您可在此處取得 Aspose.HTML for Java 的免費試用版 [here](https://releases.aspose.com/)。

### 4. 如何取得 Aspose.HTML for Java 的臨時授權？

您可在此處取得臨時授權 [here](https://purchase.aspose.com/temporary-license/)。

### 5. 在哪裡可以取得 Aspose.HTML for Java 的支援？

您可在 [Aspose forums](https://forum.aspose.com/) 獲得支援。

## 其他常見問答

**Q: 如何將 EPUB 轉換為 PNG 而非 JPEG？**  
A: 將 `ImageSaveOptions` 中的 `ImageFormat` 改為 `ImageFormat.Png`，並相應調整檔案副檔名。

**Q: 我可以只提取 EPUB 的特定頁面嗎？**  
A: 可以，透過遍歷 `lStream` 集合，於寫入檔案前選取所需的索引。

**Q: 能否在雲端函式中執行此轉換而不寫入磁碟？**  
A: 完全可以。因為轉換輸出存於記憶體串流，您可以直接從雲端函式回傳位元組陣列。

**Q: Aspose.HTML 是否支援受 DRM 保護的 EPUB 檔案？**  
A: 此函式庫只能開啟未加密的 EPUB。對於受 DRM 保護的檔案，您需先移除保護才能轉換。

**Q: 此功能需要哪個版本的 Aspose.HTML？**  
A: `MemoryStreamProvider` 類別自 Aspose.HTML 22.9 版起即提供。

---

**最後更新：** 2026-01-02  
**測試環境：** Aspose.HTML for Java 23.10  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}