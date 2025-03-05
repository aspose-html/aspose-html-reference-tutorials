---
title: 使用 Aspose.HTML 自訂 HTML 頁邊距
linktitle: CSS 擴充 - 新增標題和頁碼
second_title: 使用 Aspose.HTML 進行 Java HTML 處理
description: 了解如何使用 Aspose.HTML for Java 自訂頁邊距、新增頁碼和標題至 HTML 文件。
type: docs
weight: 10
url: /zh-hant/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML for Java 是一個功能強大的函式庫，用於在 Java 應用程式中處理 HTML 文件。在本教學中，我們將探討如何使用 Aspose.HTML for Java 建立自訂頁邊距以及將頁碼和標題新增至 HTML 文件中。本逐步指南將把流程分解為可管理的步驟，以幫助您輕鬆地將這些功能整合到 HTML 文件中。

## 先決條件

在我們開始之前，請確保您具備以下先決條件：

1. Java 開發環境：確保您的電腦上設定有 Java 開發環境。

2.  Aspose.HTML for Java：下載並安裝 Aspose.HTML for Java 函式庫[這裡](https://releases.aspose.com/html/java/).

## 導入包

首先，您需要從 Aspose.HTML for Java 匯入必要的套件。將以下導入語句加入您的 Java 程式碼：

```java
//導入 Aspose.HTML 包
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

現在，讓我們將新增自訂頁邊距、頁碼和標題的流程分解為可管理的步驟：

## 第 1 步：初始化配置和頁邊距

```java
//初始化配置物件並設定文件的頁邊距
Configuration configuration = new Configuration();
try {
    //取得用戶代理服務
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    //設定自訂邊距的樣式並在其上建立標記
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

在此步驟中，我們初始化配置物件並設定自訂頁邊距，包括頁面計數器和頁面標題的位置。

## 第 2 步：初始化 HTML 文檔

```java
//初始化 HTML 文件
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

在這裡，我們建立一個包含範例內容（在本例中為「Hello World」訊息）的 HTML 文檔，並套用步驟 1 中的配置。

## 步驟 3：初始化輸出設備並渲染文檔

```java
//初始化輸出設備
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //將文件傳送到輸出設備
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

在此步驟中，我們設定輸出裝置並渲染 HTML 文件。文件將被處理並儲存為具有指定頁邊距、頁碼和標題的 XPS 檔案。

## 結論

恭喜！您已經成功學習如何使用 Aspose.HTML for Java 建立自訂頁邊距以及為 HTML 文件新增頁碼和標題。這種自訂可讓您建立更專業且更具視覺吸引力的文件。

如果您有任何疑問或遇到任何問題，請隨時訪問[Aspose.HTML for Java 文檔](https://reference.aspose.com/html/java/)或尋求協助[Aspose 支援論壇](https://forum.aspose.com/).

## 常見問題解答

### Q1：什麼是 Java 版 Aspose.HTML？

A1：Aspose.HTML for Java 是一個 Java 函式庫，它提供了在 Java 應用程式中處理 HTML 文件的強大工具。

### Q2：我可以進一步自訂頁邊距嗎？

A2：是的，您可以在步驟 1 中修改 CSS 樣式，以根據您的要求自訂頁邊距。

### Q3：如何在 HTML 文件中新增更多內容？

A3：您可以修改步驟2中的HTML內容，將範例內容替換為您自己的內容。

### Q4：Aspose.HTML for Java 是否與其他文件格式相容？

A4：是的，Aspose.HTML for Java 可用於將 HTML 文件轉換為各種格式，包括 PDF、XPS 和映像。

### Q5：使用 Aspose.HTML for Java 需要授權嗎？

 A5：是的，您可以從以下位置取得許可證或免費試用版：[這裡](https://purchase.aspose.com/buy)或者[這裡](https://releases.aspose.com/).