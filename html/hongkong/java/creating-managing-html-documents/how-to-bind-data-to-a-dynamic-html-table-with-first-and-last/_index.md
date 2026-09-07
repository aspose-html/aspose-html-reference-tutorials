---
category: general
date: 2026-09-07
description: 如何在動態 HTML 表格中綁定資料——學習如何有效產生表格列並填寫名與姓欄位
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: zh-hant
lastmod: 2026-09-07
og_description: 如何在動態 HTML 表格中綁定資料。本教學示範如何產生表格列、顯示名字與姓氏，並使用 JavaScript 填充表格列。
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: 如何將資料綁定至動態 HTML 表格 – 步驟教學
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: how to bind data in a dynamic HTML table – learn how to generate table
    rows and populate first and last name fields efficiently
  headline: How to bind data to a dynamic HTML table with first and last name columns
  type: TechArticle
tags:
- data binding
- html table
- templating
title: 如何將資料綁定至具有名與姓欄位的動態HTML表格
url: /zh-hant/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何將資料繫結至具有名字與姓氏欄位的動態 HTML 表格

如果你需要 **how to bind data**（繫結資料）到會隨每筆記錄增長的表格，本指南提供完整解決方案。你將會看到如何產生動態 HTML 表格、填充表格列，並在不撰寫重複標記的情況下顯示每個人的名字與姓氏。

此範例使用輕量級的模板語法，能在任何現代瀏覽器中運作，但其概念同樣適用於 Handlebars、Mustache 或伺服器端引擎。完成本教學後，你可以直接將程式碼複製到專案中，即時開始繫結資料。

## 本教學涵蓋內容

* 如何構建包含多筆人物資料的資料來源  
* 如何建立可重複使用的表格模板，讓每筆資料都能產生對應的列  
* 如何繫結資料並產生最終的 HTML 標記  
* 在填充表格列時常見的陷阱與避免方式  

不需要外部函式庫，雖然相同模式亦可套用於常見的模板框架。唯一的前置條件是具備基本的 HTML 與 JavaScript 知識。

## 前置條件

* 現代瀏覽器（Chrome、Edge、Firefox 或 Safari）  
* 用於編輯 HTML/JavaScript 檔案的編輯器  
* 可選：一個 JSON 檔案或 JavaScript 物件，代表人物集合  

## 步驟 1：定義資料來源

首先，建立一個與模板結構相符的 JavaScript 物件。每個人物都有名字、姓氏以及地址物件。

```html
<script>
  // Data source – an array of person objects
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: {
            Street: "Maple",
            Number: "12A",
            City: "Springfield"
          }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: {
            Street: "Oak",
            Number: "34B",
            City: "Riverdale"
          }
        }
        // Add more person objects as needed
      ]
    }
  };
</script>
```

**為什麼這很重要：** 物件層級 (`Persons.Person`) 與模板中的 `{{#foreach Persons.Person}}` 迴圈相匹配，讓引擎能自動遍歷每一筆資料。

## 步驟 2：撰寫帶有重複區塊的表格模板

以下模板使用簡易的 Mustache 風格語法（`{{#foreach}}`）來為每位人物重複 `<tr>`。請將模板放在 `<script type="text/template">` 標籤內，讓瀏覽器在處理前忽略它。

```html
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Table header -->
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <!-- Row populated with each person's data -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**為什麼這很重要：** `{{#foreach Persons.Person}}` 指令告訴引擎對每個人物物件重複開閉標籤之間的內容。於列內你可以引用任何屬性（`{{FirstName}}`、`{{LastName}}` 等）以 **populate table rows** 動態填充。

## 步驟 3：實作一個小型渲染函式

因為教學必須自給自足，我們將撰寫一個最小化的渲染器，將 Mustache 風格的佔位符替換為真實值。此函式會遍歷資料物件、展開重複區塊，並將最終的 HTML 注入頁面。

```html
<script>
  /**
   * Renders a template that contains a single {{#foreach}} block.
   * This implementation is intentionally simple and works for the
   * specific structure used in this tutorial.
   *
   * @param {string} tmpl   The raw template string.
   * @param {object} ctx    The data context (e.g., the `data` object).
   * @returns {string}      The rendered HTML.
   */
  function renderTemplate(tmpl, ctx) {
    // Extract the foreach expression and the block to repeat
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl; // No foreach found

    const path = match[1].trim(); // e.g., "Persons.Person"
    const block = match[2];       // HTML that repeats

    // Resolve the array from the context (supports dot notation)
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items)) return tmpl;

    // Render each item
    const renderedBlocks = items.map(item => {
      // Replace each {{property}} with the corresponding value
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });

    // Replace the whole foreach section with the concatenated rows
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  // When the DOM is ready, render the table
  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>
```

**為什麼這很重要：** 此渲染器示範了 **how to generate table** 標記的程式化方式，無需引入完整函式庫。它同時說明了從模板到最終 HTML 的轉換過程，方便你日後改寫為其他模板引擎。

## 步驟 4：加入佔位元素以放置產生的表格

建立一個空的 `<div>`，腳本會在渲染完成後填入內容。

```html
<div id="output"></div>
```

頁面載入時，腳本會將此 `<div>` 的內容取代為完整的表格。

## 步驟 5：驗證結果

在瀏覽器開啟 HTML 檔案。你應該會看到一個列出每位人物全名與地址的表格：

| 人物            | 地址                             |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

若你在 `data.Persons.Person` 陣列中加入更多物件，表格會自動增長，滿足 **populate table rows** 的需求。

## 小技巧：處理空集合

當資料陣列為空時，渲染器目前會輸出一個空的表頭。為提供更清晰的使用者體驗，可加入防護機制：

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

此小變更可防止空表格出現，並即時給予使用者回饋。

## 常見變化與邊緣案例

| 情境                                   | 調整方式                                                                 |
|----------------------------------------|--------------------------------------------------------------------------|
| 使用伺服器端引擎（如 Handlebars）      | 將自訂的 `renderTemplate` 換成 `Handlebars.compile`，並傳入相同的資料物件。 |
| 需要依字母順序排序列                   | 在呼叫 `renderTemplate` 前先對 `data.Persons.Person` 進行排序。          |
| 新增電話號碼欄位                       | 在 `<tr>` 中加入 `<td>{{Phone}}</td>`，並在每個人物物件內加入 `Phone`。 |
| 大量資料（數百列）                     | 分批渲染列或使用虛擬捲動，以維持 UI 響應速度。                           |

## 完整範例

以下是可直接貼到 `index.html` 的完整 HTML 檔案，包含上述所有部份。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to bind data to a dynamic HTML table</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<h1>Dynamic HTML table bound to JavaScript data</h1>

<!-- Step 2: Table template -->
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>

<!-- Step 1: Data source -->
<script>
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: { Street: "Maple", Number: "12A", City: "Springfield" }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: { Street: "Oak", Number: "34B", City: "Riverdale" }
        }
        // Add more entries as needed
      ]
    }
  };
</script>

<!-- Step 4: Output container -->
<div id="output"></div>

<!-- Step 3: Rendering logic -->
<script>
  function renderTemplate(tmpl, ctx) {
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl;
    const path = match[1].trim();
    const block = match[2];
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items) || items.length === 0) {
      return '<p>No records found.</p>';
    }
    const renderedBlocks = items.map(item => {
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>

</body>
</html>
```

**預期輸出**

頁面會呈現一個兩列的表格，每列顯示人物的全名與格式化地址。將更多物件加入 `Person` 陣列即會自動新增列，示範 **how to generate table** 元素的資料驅動方式。

## 結論

現在你已掌握 **how to bind data** 到 **dynamic HTML table**，能為每筆記錄產生列，並在表格中同時顯示名字與姓氏。

## 接下來該學什麼？

以下教學與本指南的技巧密切相關，提供完整的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Enable JavaScript in Aspose HTML – Load HTML & Get Text](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}