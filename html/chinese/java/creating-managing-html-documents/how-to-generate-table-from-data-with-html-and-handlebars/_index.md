---
category: general
date: 2026-10-12
description: 学习如何使用 Handlebars 从数据生成表格并从 JSON 填充表格。一步步指南，教你在动态 HTML 表格中重复表格行。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: zh
lastmod: 2026-10-12
og_description: 使用 Handlebars 从数据生成表格并从 JSON 填充表格。按照本教程创建带有重复行的动态 HTML 表格。
og_image_alt: Screenshot showing generated table from data in a web page
og_title: 使用 Handlebars 从数据生成表格 – 完整指南
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
title: 如何使用 HTML 和 Handlebars 从数据生成表格
url: /zh/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 HTML 和 Handlebars 从数据生成表格

如果您需要在网页中**从数据生成表格**，本教程将为您详细演示。通过一个简单的 Handlebars 循环，您可以**从 JSON 填充表格**，创建**重复表格行**，并最终得到一个完整的**动态 HTML 表格**，只要源数据变化，它就会自动更新。

接下来几分钟，您将看到一个完整且可运行的示例，了解每个部分为何重要，并学习如何将该模式适配到更复杂的场景，例如条件列或嵌套对象。

## 您将构建的内容

* 读取包含人员列表的 JSON 负载。
* 为每个人重复一行表格（`repeat table rows`）。
* 将每个人的名、姓和地址插入相应的单元格。
* 无需服务器端渲染——整个过程在浏览器中完成。

**先决条件**

* 基本的 HTML 与 JavaScript 知识。
* 现代浏览器（Chrome、Edge、Firefox 或 Safari）。
* Handlebars.js —— 我们将从 CDN 加载它，无需构建工具。

---

## 第一步：准备 JSON 数据源

第一步是定义一个 JavaScript 对象，模拟您从 API 获得的 JSON。Handlebars 可以直接使用普通对象，因此您可以将数据直接嵌入 `<script>` 标签中进行演示。

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

**为什么这很重要** —— 将数据保存在单独的 `<script>` 元素中，您以后可以轻松替换为真实的 AJAX 调用。结构 (`Persons.Person`) 与 Handlebars `{{#foreach Persons.Person}}` 块使用的路径相匹配，这对于**从 JSON 填充表格**至关重要。

---

## 第二步：编写重复行的 Handlebars 模板

接下来，创建一个 `<script type="text/x-handlebars-template">` 块，其中包含表格的标记。Handlebars 会用实际值替换占位符，并为每个人重复 `<tr>`。

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

**关键部分说明**

* `{{#foreach Persons.Person}}` 告诉 Handlebars 为 `Persons.Person` 数组中的每个条目**重复表格行**。
* `{{FirstName}} {{LastName}}` 和 `{{Address.*}}` 表达式从当前数组元素中提取值。
* 将整个表格包裹在 `data_merge` 属性中是可选的；它在后续处理或 CSS 选择器中可能有用。

---

## 第三步：加载 Handlebars 并编译模板

我们将从 CDN 加载 Handlebars，解析 JSON，编译模板，并将最终的 HTML 注入页面。

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

**为什么在运行时编译？** —— 只编译一次模板并重复使用可以保持页面快速，尤其是在数据频繁变化时。此模式还能轻松实现多次**从 JSON 填充表格**而无需重新加载页面。

---

## 第四步：为生成的表格预留容器

添加一个占位 `<div>`，用于显示动态生成的表格。这可以保持标记整洁，并将静态布局与生成内容的职责分离。

```html
<div id="output"></div>
```

当第 3 步的脚本运行后，`<div id="output">` 将包含一个完整的 `<table>` 元素，准备进行样式设置或进一步操作。

---

## 第五步：验证输出并为表格添加样式（可选）

在浏览器中打开页面，您应该会看到如下表格：

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

**可选样式** —— 如果想要更简洁的外观，可添加以下几条 CSS 规则：

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## 处理边缘情况和常见变体

### 1. 空数据集

如果 JSON 数组为空，Handlebars 仍会渲染表头行，但不会渲染数据行。若要显示友好提示，可将表格包裹在条件块中：

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. 嵌套循环（例如，每人多个地址）

当一个人可能有多个地址时，您可以在行内再嵌套一个 `{{#foreach}}`：

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

### 3. 使用真实 API

将静态的 `<script id="people-data">` 替换为 fetch 调用：

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

这展示了相同的**动态表格行**技术，同时获取实时数据。

### 4. 可访问性考虑

- 为 `<th>` 元素添加 `scope="col"`。
- 使用 `<caption>` 描述表格用途。
- 若使用自定义 CSS，确保颜色对比度足够。

---

## 完整、可运行的示例

将以下代码块复制到 `index.html` 文件中并在浏览器中打开。页面将**从数据生成表格**、**从 JSON 填充表格**，并自动重复行。

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

**预期结果**

一个包含两行（加表头）的表格，显示 “Alice Anderson” 与 “Bob Baker” 以及各自的地址。页面可离线运行，证明您可以在没有服务器组件的情况下**从数据生成表格**。

---

## 结论

现在您已经了解如何使用 Handlebars 模板**从数据生成表格**、**从 JSON 填充表格**，以及创建形成**动态 HTML 表格**的**重复表格行**。该模式可扩展到更大的数据集、嵌套结构和实时 API 调用，为任何客户端报表或管理界面提供坚实的基础。

**后续步骤**

- 探索 Handlebars 辅助函数，以格式化日期或数字。
- 将此方法与 CSS Grid 或 Flexbox 结合，实现响应式表格布局。
- 集成分页或排序库，以处理超大数据集。

欢迎尝试不同的 JSON 结构、添加条件列，或将 Handlebars 替换为其他模板引擎——您新掌握的技能将帮助您快速、可靠地构建灵活的数据驱动界面。

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在本教程演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}