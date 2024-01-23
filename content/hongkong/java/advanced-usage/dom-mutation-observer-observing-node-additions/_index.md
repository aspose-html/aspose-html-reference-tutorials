---
title: 使用 Aspose.HTML for Java 進行 DOM 突變觀察
linktitle: DOM Mutation Observer - 觀察節點添加
second_title: 使用 Aspose.HTML 進行 Java HTML 處理
description: 在此逐步指南中了解如何使用 Aspose.HTML for Java 來實作 DOM Mutation Observer。有效監控 DOM 變更並做出反應。
type: docs
weight: 11
url: /zh-hant/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

您是 Java 開發人員，希望觀察 HTML 文件的文檔物件模型 (DOM) 中的變更並對其做出反應嗎？ Aspose.HTML for Java 為這項任務提供了強大的解決方案。在本逐步指南中，我們將探索如何使用 Aspose.HTML for Java 建立 HTML 文件並使用 Mutation Observer 觀察節點新增。本教學將引導您完成整個過程，將每個範例分解為多個步驟。最後，您將能夠在 Java 專案中輕鬆實作 DOM Mutation Observers。

## 先決條件

在我們深入使用 Aspose.HTML for Java 之前，讓我們確保您具備必要的先決條件：

1. Java 開發環境：確保您的系統上安裝了 Java 開發工具包 (JDK)。

2.  Aspose.HTML for Java：您需要下載並安裝 Aspose.HTML for Java。你可以找到下載鏈接[這裡](https://releases.aspose.com/html/java/).

3. IDE（整合開發環境）：使用您首選的 Java IDE（例如 IntelliJ IDEA 或 Eclipse）來編寫和執行 Java 程式碼。

## 導入包

要開始使用 Aspose.HTML for Java，您需要將所需的套件匯入到您的 Java 程式碼中。您可以這樣做：

```java
//導入必要的套件
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

//建立一個空的 HTML 文檔
HTMLDocument document = new HTMLDocument();
```

現在您已經匯入了所需的套件，讓我們繼續學習如何在 Java 中實作 DOM Mutation Observer 的分步指南。

## 第 1 步：創建突變觀察者實例

首先，您需要建立一個 Mutation Observer 實例。該觀察者將監視 DOM 中的變化，並在發生變化時執行回調函數。

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

在此步驟中，我們建立一個具有回調函數的觀察者，該函數在將節點新增至 DOM 時列印一條訊息。

## 第2步：配置觀察者

現在，讓我們使用所需的選項來配置觀察者。我們想要觀察子清單的變化和子樹的變化，以及字元資料的變化。

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

//傳入目標節點以指定配置進行觀察
observer.observe(document.getBody(), config);
```

在這裡，我們設定`config`物件以啟用觀察子清單、子樹和字元資料變更。然後我們傳入目標節點（在本例中為文件的`<body>`）和觀察者的配置。

## 第三步：修改DOM

現在，我們將對 DOM 進行一些更改以觸發觀察者。我們將建立一個段落元素並將其附加到文件的正文中。

```java
//建立一個段落元素並將其附加到文件正文
Element p = document.createElement("p");
document.getBody().appendChild(p);

//建立文字並將其附加到段落中
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

在此步驟中，我們建立一個 HTML 段落元素並將其新增至文件的正文中。然後，我們創建一個內容為「Hello World」的文字節點並將其附加到該段落中。

## 第 4 步：等待觀察結果（非同步）

由於突變是非同步觀察的，因此我們需要等待一段時間才能讓觀察者捕捉變化。我們將使用`synchronized`和`wait`為此，如下圖所示。

```java
//由於突變在非同步模式下工作，因此請等待幾秒鐘
synchronized (this) {
    wait(5000);
}
```

在這裡，我們等待 5 秒鐘以確保觀察者有機會捕獲任何突變。

## 第五步：停止觀察

最後，當您完成觀察時，您必須斷開觀察者的連結以釋放資源。

```java
//停止觀察
observer.disconnect();
```

透過這一步，您已經完成了觀察並可以清理資源。

## 結論

在本教程中，我們介紹了使用 Aspose.HTML for Java 實作 DOM 突變觀察器的過程。您已經學習如何創建觀察者、配置它、更改 DOM、等待觀察以及停止觀察。現在，您已經掌握了在 Java 專案中應用 DOM Mutation Observers 來有效監視 HTML 文件 DOM 變化並做出反應的技能。

如果您有任何疑問或遇到問題，請隨時尋求協助[Aspose.HTML 論壇](https://forum.aspose.com/)。此外，您還可以訪問[文件](https://reference.aspose.com/html/java/)有關 Java 版 Aspose.HTML 的詳細資訊。

## 常見問題解答

### Q1：什麼是 DOM 突變觀察者？

A1：DOM 突變觀察器是一項 JavaScript 功能，可讓您監視 HTML 文件的文檔物件模型 (DOM) 中的變更。它提供了一種即時回應 DOM 節點的新增、刪除或修改的方法。

### Q2：我可以在我的商業專案中使用 Aspose.HTML for Java 嗎？

 A2：是的，您可以在商業專案中使用Aspose.HTML for Java。您可以找到許可和購買訊息[這裡](https://purchase.aspose.com/buy).

### 問題 3：Aspose.HTML for Java 是否有免費試用版？

A3：是的，您可以免費試用 Aspose.HTML for Java[這裡](https://releases.aspose.com/)。這使您可以在購買之前探索其特性和功能。

### Q4：使用變異觀察器觀察角色資料變化有什麼好處？

A4：觀察字元資料變化對於您想要監控 HTML 元素文字內容變化並做出反應的場景非常有用。例如，您可以使用它來追蹤和回應 Web 表單中的使用者輸入。

### Q5：使用Aspose.HTML for Java時如何處理資源？

 A5：完成後釋放資源很重要。在我們的範例中，我們使用了`document.dispose()`清理與 HTML 文件關聯的資源。確保處置您創建的任何物件和資源以避免記憶體洩漏。