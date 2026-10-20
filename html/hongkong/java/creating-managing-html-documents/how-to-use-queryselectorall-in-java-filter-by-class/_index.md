---
category: general
date: 2026-04-23
description: 如何在 Java 中使用 querySelectorAll 依類別篩選元素、讀取屬性值，並遍歷 NodeList 以提取產品資料。
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: zh-hant
og_description: 如何在 Java 中使用 querySelectorAll 依類別篩選元素、讀取屬性值，並遍歷 NodeList 以提取產品資料。
og_title: 如何在 Java 中使用 querySelectorAll – 依類別篩選
tags:
- Java
- HTML parsing
- DOM manipulation
title: 在 Java 中使用 querySelectorAll – 按類別篩選
url: /zh-hant/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 querySelectorAll – 依類別篩選

在需要從 HTML 文件中抓取特定元素時，如何在 Java 中使用 querySelectorAll 是關鍵。本教學將示範如何依類別篩選元素、讀取屬性值，並遍歷 NodeList 以取得目錄頁面的商品價格。

有沒有曾經面對龐大的 HTML 檔案，卻不知道如何只挑出「特價」卡片，而不必自行寫解析器？這正是我們在此要解決的問題——不需要額外的函式庫，僅使用 Aspose.HTML，搭配幾個簡單步驟即可完成。

完成本教學後，你將得到一個完整、可執行的程式，具備以下功能：

* **使用 CSS 選擇器選取元素**（`select elements css selector`）  
* **依類別篩選**（`filter elements by class`）  
* **讀取自訂屬性**（`how to read attribute`）  
* **遍歷取得的 NodeList**（`iterate nodelist java`）

不需要事先了解 Aspose.HTML，只要有基本的 Java 環境與一個測試用的 HTML 檔案即可。

![how to use querySelectorAll in Java example](https://example.com/images/queryselectorall-java.png "how to use querySelectorAll in Java")

---

## 需要的工具

| Requirement | Why it matters |
|-------------|----------------|
| **Java 17+** | 提供現代語言功能與更佳的模組管理。 |
| **Aspose.HTML for Java**（最新版本） | 提供 `Document` 類別與 CSS 選擇器引擎。 |
| **catalog.html**（範例 HTML） | 我們要查詢的來源檔案。 |
| **IDE 或純 `javac`** | 用來編譯與執行示範程式。 |

如果尚未將 Aspose.HTML 加入專案，只要把 JAR 放到 `libs` 資料夾，並加入 classpath 即可：

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## 步驟 1 – 載入 HTML 文件

在能執行查詢之前，需要先建立代表 HTML 檔案的 `Document` 物件。這就像在讀取試算表前先打開檔案一樣。

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **為什麼這很重要：** `Document` 類別會將標記解析成 DOM 樹，讓 CSS 選擇器引擎得以運作。若省略此步，手上只會是一個純字串，無法使用 `querySelectorAll`。

---

## 步驟 2 – 使用 CSS 選擇器選取元素

接下來就是重點：**如何使用 querySelectorAll**。此方法接受任何有效的 CSS 選擇器，讓你可以精確或寬鬆地指定目標。對於本範例，我們想取得同時符合以下條件的商品卡片：

* 具備 `product-card` 類別，  
* 同時具備 `sale` 類別，  
* 且帶有 `data-price` 屬性。

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **說明：**  
> * `.product-card.sale` → 篩選同時擁有 **兩個**類別的元素。  
> * `[data-price]` → 確保屬性存在，等同於在一次呼叫中 **依類別與屬性** 共同篩選。  
> * 結果會回傳 `NodeList`，這是一個有序集合，可供遍歷。

若日後需要 **select elements css selector** 其他模式，只要修改字串即可，無需重寫程式碼。

---

## 步驟 3 – 在 Java 中遍歷 NodeList

`NodeList` 的行為類似陣列，但它並未實作 `Iterable` 介面。因此我們使用傳統的 `for` 迴圈——非常適合 **iterate nodelist java** 的情境。

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **為什麼使用 `for` 迴圈？**  
> 它能直接取得索引，方便記錄或條件分支。如果你偏好 `while` 迴圈，邏輯完全相同，只要改變迴圈寫法即可。

---

## 步驟 4 – 讀取 `data-price` 屬性

現在終於可以回答 **how to read attribute** 的問題了。在 DOM API 中，`getAttribute` 會回傳原始字串，與標記中出現的完全相同。

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **小技巧：** 若屬性可能不存在，`getAttribute` 會回傳 `null`。可以透過簡單的檢查避免 NullPointerException：

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## 步驟 5 – 輸出結果

最後，我們把每筆價格印到主控台。這與實務上可能將資料寫入資料庫或 API 載荷的情境相同。

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### 預期的主控台輸出

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

如果選擇器找不到符合的節點，迴圈根本不會執行——不會拋出例外。這對於 **edge cases**（例如目錄為空）是一個不錯的保護機制。

---

## 完整範例

將以下程式碼全部複製貼上至 `CssSelectorDemo.java`：

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

儲存檔案、編譯並執行，即可看到價格一筆筆輸出。 🎉

---

## 常見問題與進階技巧

| Question | Answer |
|----------|--------|
| *如果還要依標籤名稱篩選呢？* | 只要在前面加上標籤：`document.querySelectorAll("div.product-card.sale[data-price]")`。 |
| *可以串接多個屬性篩選嗎？* | 當然可以。例如 `[data-price][data-stock]` 只會保留同時具有 **兩個**屬性的元素。 |
| *`querySelectorAll` 是否區分大小寫？* | 會——在 HTML5 中，類別與屬性名稱皆為大小寫敏感。 |
| *要如何處理超大型的 HTML 檔案？* | Aspose.HTML 會以串流方式讀取文件，你也可以將選擇器限制在子樹上（`someElement.querySelectorAll(...)`）。 |
| *What

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}