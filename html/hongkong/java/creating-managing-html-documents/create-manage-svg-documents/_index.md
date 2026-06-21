---
date: 2026-04-12
description: 學習如何使用 Aspose.HTML for Java 建立 SVG 檔案並儲存 SVG 檔案。本指南涵蓋動態生成 SVG、設定 SVG
  填色以及匯出 SVG 文件。
keywords:
- how to create svg
- save svg file
- set svg fill color
- dynamic svg generation
- create svg java
linktitle: 在 Aspose.HTML 中建立與管理 SVG 文件
second_title: Java HTML Processing with Aspose.HTML
title: 如何使用 Aspose.HTML for Java 建立 SVG 文件
url: /zh-hant/java/creating-managing-html-documents/create-manage-svg-documents/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.HTML for Java 建立 SVG 文件

Scalable Vector Graphics (SVG) 為您提供清晰、解析度無關的圖形，能在任何裝置上自動縮放。在本教學中，您將學習 **如何建立 SVG** 圖像的程式化產生方式，使用 Aspose.HTML for Java 設定 SVG 填色、動態產生形狀，最後將 SVG 文件匯出為檔案。無論您是建立報表工具、圖表函式庫，或只是需要即時的向量圖形，本指南都會一步步帶您完成。

## 快速解答
- **需要的函式庫是什麼？** Aspose.HTML for Java。  
- **我可以在執行時產生 SVG 嗎？** 是 – API 支援動態 SVG 產生。  
- **如何設定形狀的顏色？** 使用 `setAttribute("fill", "yourColor")`。  
- **輸出格式為何？** 將文件儲存為 `.svg` 檔案（匯出 SVG 文件）。  
- **正式環境需要授權嗎？** 非試用情況下需要商業授權。

## 什麼是 SVG 以及為何使用它？
SVG 是一種基於 XML 的向量圖像格式，可在不失真情況下縮放。由於它是文字型別，您可以使用程式碼操作、以 CSS 進行樣式設定，並以 JavaScript 進行動畫。使用 Aspose.HTML，您可以在伺服器端建立 SVG，這使其非常適合自動化報表產生、客製化圖示，或任何需要 **動態 SVG 產生** 的情境。

## 為何選擇 Aspose.HTML for Java？
- **完整控制** SVG DOM – 可程式化地新增、編輯或移除元素。  
- **跨平台** – 可在任何相容 Java 的環境執行。  
- **無外部相依性** – 函式庫會為您處理解析與序列化。  
- **效能最佳化** – 適合快速產生大量 SVG 檔案。

## 先決條件
在深入使用 Aspose.HTML 處理 SVG 文件的細節之前，您需要先具備以下先決條件：

1. **Java 環境**：確保您的機器已安裝 Java Development Kit（JDK）。若尚未安裝，可從 [Oracle website](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) 下載。  
2. **Aspose.HTML for Java 函式庫**：您需要取得 Aspose.HTML 函式庫。可在 [此處下載](https://releases.aspose.com/html/java/) 或在 [此處](https://releases.aspose.com/) 取得免費試用版。  
3. **IDE 設定**：一個良好的整合開發環境（IDE），如 IntelliJ IDEA、Eclipse 或 NetBeans，用於編寫與執行 Java 程式碼。  
4. **基本 Java 知識**：熟悉 Java 程式設計與物件導向概念，將對後續操作非常有幫助。

既然先決條件已備妥，讓我們開始建立 SVG 文件吧！

## 逐步指南

### 步驟 1：建立 SVG 文件
建立 SVG 文件是讓圖形活起來的第一步。此處我們使用簡單的 XML 字串建立 `SVGDocument`，該字串會繪製一個圓形。

```java
com.aspose.html.dom.svg.SVGDocument document = new com.aspose.html.dom.svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", ".");
```

第二個參數設定任何外部資源的基礎路徑。

### 步驟 2：存取文件元素
文件已建立後，我們需要取得根 `<svg>` 元素的參考，以便進行修改。

```java
document.getDocumentElement();
```

可以將其想像成打開 SVG 房子的前門——其他所有內容都位於此元素內。

### 步驟 3：輸出 SVG 內容
讓我們透過將標記印到主控台，驗證 SVG 是否正確建立。

```java
System.out.println(document.getDocumentElement().getOuterHTML());
```

`getOuterHTML()` 方法會回傳完整的 SVG 標記，讓您快速檢視目前的狀態。

### 步驟 4：設定 SVG 填色
若要變更視覺外觀，您可以為任意元素設定屬性。此處我們將圓形的填色改為紅色。

```java
document.getDocumentElement().setAttribute("fill", "red");
```

此範例示範如何以程式方式 **設定 SVG 填色**，讓您即時自訂圖形。

### 步驟 5：新增 SVG 形狀
讓我們透過新增藍色矩形來豐富圖像。我們建立新元素、設定屬性，並將其附加到根元素。

```java
document.getDocumentElement().appendChild(
    document.createElement("rect").setAttribute("x", "10").setAttribute("y", "10")
    .setAttribute("width", "80").setAttribute("height", "80").setAttribute("fill", "blue")
);
```

這樣的動態 SVG 產生讓您能在不需手動編輯的情況下構建複雜的插圖。

### 步驟 6：儲存 SVG 文件
完成所有修改後，將 SVG 文件匯出為檔案，以便在網頁、報表或其他應用程式中使用。

```java
document.save("output.svg");
```

此步驟 **儲存 SVG 檔案**，即將您剛建立的 SVG 文件匯出。

## 常見問題與解決方案
- **缺少命名空間錯誤：** 確認 SVG 字串包含 `xmlns='http://www.w3.org/2000/svg'`。  
- **檔案未儲存：** 檢查應用程式是否對目標目錄具寫入權限。  
- **屬性未套用：** 記得 `setAttribute` 作用於您呼叫的元素；若要影響根元素，請使用 `document.getDocumentElement()`。

## 常見問答

### 什麼是 SVG？
SVG 代表可縮放向量圖形（Scalable Vector Graphics），是一種基於 XML 的向量圖像，可在不失真情況下縮放。

### 哪裡可以下載 Aspose.HTML for Java？
您可從 [此處](https://releases.aspose.com/html/java/) 下載。

### 我可以取得 Aspose.HTML for Java 的免費試用嗎？
可以，您可在 [此處](https://releases.aspose.com/) 取得免費試用版。

### 使用 Aspose.HTML 可以建立哪些形狀？
您可以建立任何 SVG 形狀，包括圓形、矩形、多邊形與路徑。

### 如何取得 Aspose.HTML 的支援？
您可在 [Aspose 論壇](https://forum.aspose.com/c/html/29) 獲得支援。

---

**最後更新：** 2026-04-12  
**測試環境：** Aspose.HTML for Java 24.12  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}