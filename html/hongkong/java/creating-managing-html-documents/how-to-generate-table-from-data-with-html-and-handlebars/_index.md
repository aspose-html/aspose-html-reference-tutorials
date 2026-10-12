---
category: general
date: 2026-10-12
description: 學習如何使用 Handlebars 從資料生成表格並從 JSON 填充表格。一步一步的指南，教你在動態 HTML 表格中重複表格列。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: zh-hant
lastmod: 2026-10-12
og_description: 使用 Handlebars 從資料產生表格，並以 JSON 填充表格。跟隨此教學，建立具重複表格列的動態 HTML 表格。
og_image_alt: Screenshot showing generated table from data in a web page
og_title: 使用 Handlebars 從資料生成表格 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-12'
  description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  headline: How to generate table from data with HTML and Handlebars
  type: TechArticle
- description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  name: How to generate table from data with HTML and Handlebars
  steps:
  - name: 1. Empty data sets
    text: 'If the JSON array is empty, Handlebars will still render the header row
      but no data rows. To display a friendly message, wrap the table in a conditional
      block:'
  - name: 2. Nested loops (e.g., multiple addresses per person)
    text: 'When a person can have several addresses, you can nest another `{{#foreach}}`
      inside the row:'
  - name: 3. Using a real API
    text: 'Replace the static `<script id="people-data">` with a fetch call:'
  - name: 4. Accessibility considerations
    text: '* Add `scope="col"` to `<th>` elements. * Use `<caption>` to describe the
      table purpose. * Ensure sufficient color contrast if you apply custom CSS.'
  type: HowTo
tags:
- HTML
- Handlebars
- JSON
- templating
title: 如何使用 HTML 與 Handlebars 從資料生成表格
url: /zh-hant/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 HTML 和 Handlebars 從資料產生表格

如果您需要在網頁中 **generate table from data**，本教學將會完整說明。透過簡單的 Handlebars 迴圈，您可以 **populate table from JSON**、建立 **repeat table rows**，最終得到一個會在來源變更時即時更新的 **dynamic HTML table**。

在接下來的幾分鐘內，您將看到完整且可執行的範例，了解每個部分為何重要，並學會如何將此模式套用到更複雜的情境，例如條件欄位或巢狀物件。

## 您將建立的內容

我們將建立一個 HTML 表格，該表格：

* 讀取包含人員清單的 JSON 資料。
* 為每位人員重複一個表格列 (`repeat table rows`)。
* 將每位人員的名字、姓氏與地址插入相應的儲存格。
* 無需任何伺服器端渲染——整個過程在瀏覽器中完成。

**先決條件**

* 具備 HTML 與 JavaScript 的基本知識。
* 使用現代瀏覽器（Chrome、Edge、Firefox 或 Safari）。
* Handlebars.js – 我們會從 CDN 載入，無需建置工具。

---

## 步驟 1：準備 JSON 資料來源

第一步是定義一個模擬您從 API 取得的 JSON 的 JavaScript 物件。Handlebars 能處理純物件，因此您可以直接在 `<script>` 標籤中嵌入資料以作示範。

```html
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>
```

**為何重要** – 將資料放在獨立的 `<script>` 元素中，日後可以輕鬆換成真實的 AJAX 呼叫。結構 (`Persons.Person`) 與 Handlebars `{{#foreach Persons.Person}}` 區塊使用的路徑相符，這對 **populate table from JSON** 至關重要。

## 步驟 2：撰寫會重複列的 Handlebars 範本

接著，建立一個 `<script type="text/x-handlebars-template">` 區塊，內含表格的標記。Handlebars 會將佔位符替換為實際值，並為每位人員重複 `<tr>`。

```html
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Header row describing the columns -->
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <!-- Data row – this block is repeated for each Person -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**關鍵部分說明**

* `{{#foreach Persons.Person}}` 告訴 Handlebars 為 `Persons.Person` 陣列中的每個項目 **repeat table rows**。
* `{{FirstName}} {{LastName}}` 與 `{{Address.*}}` 表達式會從目前的陣列元素取得值。
* 將整個表格包在 `data_merge` 屬性中是可選的；它可用於後續處理或 CSS 選擇器。

## 步驟 3：載入 Handlebars 並編譯範本

我們會從 CDN 載入 Handlebars，解析 JSON，編譯範本，並將最終的 HTML 注入頁面。

```html
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  // Parse the JSON stored in the <script id="people-data">
  const rawData = document.getElementById('people-data').textContent;
  const context = JSON.parse(rawData);

  // Grab the template markup and compile it
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);

  // Generate the final HTML by applying the context
  const html = template(context);

  // Insert the generated table into the DOM
  document.getElementById('output').innerHTML = html;
</script>
```

**為何在執行時編譯？** – 只編譯一次範本並重複使用，可保持頁面效能，特別是資料頻繁變動時。此模式也讓 **populate table from JSON** 多次執行變得簡單，無需重新載入頁面。

## 步驟 4：為產生的表格保留容器

加入一個佔位的 `<div>`，讓動態表格顯示於此。這樣可保持標記整潔，並將靜態版面與產生的內容分離。

```html
<div id="output"></div>
```

當步驟 3 的腳本執行後，`<div id="output">` 內將會出現完整的 `<table>` 元素，供樣式或後續操作使用。

## 步驟 5：驗證輸出並為表格加上樣式（可選）

在瀏覽器開啟此頁面，您應該會看到如下的表格：

![Screenshot showing generated table from data](image.png "Screenshot showing generated table from data")

```html
<table border="1" data_merge="true">
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <tr>
    <td>Alice Anderson</td>
    <td>Maple 123, Springfield</td>
  </tr>
  <tr>
    <td>Bob Baker</td>
    <td>Oak 456, Rivertown</td>
  </tr>
</table>
```

**可選樣式** – 若想要更簡潔的外觀，可加入以下 CSS 規則：

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

## 處理邊緣案例與常見變化

### 1. 空資料集

若 JSON 陣列為空，Handlebars 仍會渲染表頭列，但不會產生資料列。若要顯示友善訊息，可將表格包在條件區塊中：

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. 巢狀迴圈（例如，每人多個地址）

當一個人可能有多個地址時，您可以在列內再巢狀一個 `{{#foreach}}`：

```handlebars
{{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>
      {{#foreach Address}}
        {{Street}} {{Number}}, {{City}}<br>
      {{/foreach}}
    </td>
  </tr>
{{/foreach}}
```

### 3. 使用真實 API

將靜態的 `<script id="people-data">` 替換為 fetch 呼叫：

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

這示範了相同的 **dynamic table rows** 技術，同時取得即時資料。

### 4. 可及性考量

* 為 `<th>` 元素加入 `scope="col"`。
* 使用 `<caption>` 來說明表格目的。
* 若套用自訂 CSS，請確保有足夠的色彩對比度。

## 完整、可執行的範例

將以下區塊複製到 `index.html` 檔案中，然後在瀏覽器開啟。此頁面將 **generate table from data**、**populate table from JSON**，並自動重複列。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic table from JSON</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; border: 1px solid #ddd; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<!-- Step 1: JSON data source -->
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>

<!-- Step 2: Handlebars template -->
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th scope="col">Person</th>
    <th scope="col">Address</th>
  </tr>
  {{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
  {{/foreach}}
</table>
</script>

<!-- Step 4: Container for the generated table -->
<div id="output"></div>

<!-- Step 3: Load Handlebars, compile, and render -->
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  const raw = document.getElementById('people-data').textContent;
  const context = JSON.parse(raw);
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);
  document.getElementById('output').innerHTML = template(context);
</script>

</body>
</html>
```

**預期結果**

一個兩列（加上表頭）的表格，顯示 “Alice Anderson” 與 “Bob Baker” 以及各自的地址。此頁面可離線運作，證明您可以在不需要伺服器元件的情況下 **generate table from data**。

## 結論

您現在已了解如何使用 Handlebars 範本 **generate table from data**、**populate table from JSON**，以及建立 **repeat table rows** 形成 **dynamic HTML table**。此模式可擴展至更大的資料集、巢狀結構與即時 API 呼叫，為任何客戶端報表或管理介面提供堅實基礎。

**下一步**

* 探索 Handlebars helper，以格式化日期或數字。
* 將此方法與 CSS Grid 或 Flexbox 結合，以實作響應式表格版面。
* 整合分頁或排序函式庫，以處理極大量的資料集。

歡迎嘗試不同的 JSON 結構、加入條件欄位，或將 Handlebars 換成其他模板引擎——您新學的技能將讓您快速且可靠地構建彈性、資料驅動的介面。

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此技術為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}