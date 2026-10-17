---
category: general
date: 2026-02-16
description: 如何在 Java 中載入 HTML、設定裝置 DPI、定義虛擬螢幕尺寸，並讀取任意元素的計算後背景顏色。
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: zh-hant
og_description: 如何在 Java 中載入 HTML、設定裝置 DPI、定義虛擬螢幕尺寸，並讀取任何元素的計算背景顏色。
og_title: 如何載入 HTML、設定裝置 DPI 並讀取背景顏色
tags:
- Aspose.HTML
- Java
title: 如何載入 HTML、設定裝置 DPI 與讀取背景顏色
url: /zh-hant/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何載入 HTML、設定裝置 DPI 以及讀取背景顏色

有沒有想過在 Java 應用程式中**載入 HTML**並檢查頁面的樣式？你並不孤單——開發者常常需要在螢幕外渲染網頁、取得最終的 CSS 值，並將其用於 PDF 轉換、螢幕截圖，甚至自動化測試。  

本指南將一步步說明：載入 HTML 檔案、**設定裝置 DPI**、定義**虛擬螢幕尺寸**，最後從 `<body>` 元素**讀取背景顏色**。完成後，你將擁有一段可直接執行的程式碼，會印出**計算後的背景顏色**——沒有神祕，只是純粹的 Java。

## 需求條件

在開始之前，請確認你已具備：

* Java 17 或更新版本（程式碼相容於任何較新的 JDK）。  
* Aspose.HTML for Java 23.9 或更新版本——從 Aspose 官方網站下載 JAR，或透過 Maven 加入。  
* 一個簡單的 HTML 檔案（例如 `responsive.html`），在 CSS 中定義背景顏色。

就這樣——不需要額外框架，也不需要瀏覽器驅動程式。準備好了嗎？讓我們開始吧。

![說明如何載入 HTML 並擷取計算後樣式的圖示](/images/load-html-diagram.png){alt="說明如何載入 HTML 並擷取計算後樣式的圖示"}

## 步驟 1：載入 HTML 並設定渲染選項

首先，你需要建立一個 `HtmlLoadOptions` 物件。此物件告訴 Aspose.HTML **如何載入 HTML**——包括虛擬螢幕尺寸與欲模擬的 DPI。

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**為何這很重要：**  
設定虛擬螢幕尺寸可確保如 `@media (max-width: 600px)` 之媒體查詢的行為，如同在實體螢幕上渲染一般。DPI 會影響 CSS `px` 單位映射到實體像素的方式——在之後產生影像或 PDF 時至關重要。

## 步驟 2：使用設定好的選項載入 HTML 檔案

現在我們實際載入檔案。請注意，我們傳入先前設定好的 `loadOptions`。

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

若找不到檔案，Aspose 會拋出明確的 `FileNotFoundException`。在正式環境中，你可能需要將其包在 try‑catch 中，並回退至預設的 HTML 字串。

## 步驟 3：明確設定虛擬螢幕尺寸與裝置 DPI

即使我們已在上方呼叫 `setScreenSize` 與 `setDeviceDpi`，仍值得說明 **設定虛擬螢幕尺寸** 與 **設定裝置 DPI** 可以在渲染前的任何時點調整。例如，你可以提升 DPI 以取得高解析度的螢幕截圖：

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

若在首次載入後變更這些設定，請記得重新載入文件——Aspose 在 `Document` 建立後會將其視為不可變。

## 步驟 4：讀取背景顏色並取得計算後的背景顏色

文件載入記憶體後，你可以查詢任意元素的計算樣式。此處以 `<body>` 標籤為例，但相同方法同樣適用於 `<div>`、`<p>`，甚至偽元素。

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**你會看到的結果：** 若 `responsive.html` 內含 `body { background: #ff5722; }`，控制台會印出類似以下內容：

```
Computed background color: rgba(255,87,34,1)
```

這就是 **取得計算後背景顏色** 的結果——Aspose 會先解析所有 CSS 層疊規則、媒體查詢，甚至 `!important` 宣告，才回傳最終值。

## 完整範例

將上述步驟整合起來，以下是一個完整、可直接複製貼上的程式：

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### 預期輸出

```
Computed background color: rgba(255,255,255,1)
```

*(實際的 RGBA 數值取決於你 HTML 檔案中的 CSS。)*

## 常見陷阱與專業提示

* **遺漏 DPI 設定？** Aspose 預設為 96 DPI，可能導致高解析度螢幕截圖模糊。若需要清晰輸出，務必明確設定。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}