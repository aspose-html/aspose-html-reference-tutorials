---
category: general
date: 2026-09-07
description: 如何在动态HTML表格中绑定数据——学习如何高效生成表格行并填充名和姓字段
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: zh
lastmod: 2026-09-07
og_description: 如何在动态HTML表格中绑定数据。本教程展示了如何生成表格行、显示名和姓，并使用JavaScript填充表格行。
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: 如何将数据绑定到动态HTML表格——分步指南
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
title: 如何将数据绑定到包含名和姓列的动态HTML表格
url: /zh/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何将数据绑定到具有名字和姓氏列的动态 HTML 表格

如果您需要 **如何将数据绑定** 到一个随记录增长的表格，本指南提供完整的解决方案。您将看到如何生成动态 HTML 表格、填充表格行，并在不编写重复标记的情况下显示每个人的名字和姓氏。

示例使用一种轻量级的模板语法，可在任何现代浏览器中工作，但其概念同样适用于 Handlebars、Mustache 或服务器端模板引擎。教程结束后，您可以将代码复制到项目中并立即开始绑定数据。

## 本教程涵盖的内容

* 如何构建包含多个人员的 数据源  
* 如何创建可复用的表格模板，以便对每条记录进行重复  
* 如何绑定数据并生成最终的 HTML 标记  
* 填充表格行时的常见陷阱以及如何避免  

不需要外部库，尽管相同的模式也适用于流行的模板框架。唯一的前提是具备基本的 HTML 和 JavaScript 知识。

## 前置条件

* 现代浏览器（Chrome、Edge、Firefox 或 Safari）  
* 用于编辑 HTML/JavaScript 文件的编辑器  
* 可选：一个 JSON 文件或 JavaScript 对象，表示人员集合  

## 步骤 1：定义数据源

首先，创建一个与模板结构相匹配的 JavaScript 对象。每个人都有名字、姓氏以及一个地址对象。

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

**为什么重要：** 对象层级 (`Persons.Person`) 与模板中的 `{{#foreach Persons.Person}}` 循环相匹配，使引擎能够自动遍历每个条目。

## 步骤 2：编写带有重复块的表格模板

下面的模板使用简单的 Mustache‑style 语法（`{{#foreach}}`）来为每个人重复 `<tr>`。将模板放在 `<script type="text/template">` 标签内，以便浏览器在处理之前忽略它。

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

**为什么重要：** `{{#foreach Persons.Person}}` 指令告诉引擎对每个 person 对象重复开闭标签之间的所有内容。行内可以引用任意属性（`{{FirstName}}`、`{{LastName}}` 等）来 **动态填充表格行**。

## 步骤 3：实现一个小型渲染函数

因为本教程必须自包含，我们将编写一个最小的渲染器，用真实值替换 Mustache‑style 占位符。该函数遍历数据对象，展开重复块，并将最终的 HTML 注入页面。

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

**为什么重要：** 渲染器演示了 **如何生成表格** 标记而无需引入完整库。它还阐明了从模板到最终 HTML 的转换过程，帮助您以后将代码迁移到其他模板引擎。

## 步骤 4：添加占位符以放置生成的表格

创建一个空的 `<div>`，脚本将在渲染后填充它。

```html
<div id="output"></div>
```

页面加载时，脚本会用完整填充的表格替换该 `<div>` 的内容。

## 步骤 5：验证结果

在浏览器中打开 HTML 文件。您应该看到一个列出每个人全名和地址的表格：

| 人员            | 地址                             |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

如果向 `data.Persons.Person` 数组中添加更多对象，表格会自动增长——满足 **填充表格行** 的需求。

## 小技巧：处理空集合

当数据数组为空时，渲染器目前会输出一个空的表头。为了提供更清晰的用户体验，可加入防护代码：

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

此小改动可防止出现空表格，并向用户提供即时反馈。

## 常见变体和边缘情况

| 情形                                   | 调整说明                                                                 |
|----------------------------------------|--------------------------------------------------------------------------|
| 使用服务器端引擎（如 Handlebars）      | 将自定义的 `renderTemplate` 替换为 `Handlebars.compile` 并传入相同的数据对象。 |
| 需要按字母顺序对行进行排序               | 在调用 `renderTemplate` 前对 `data.Persons.Person` 进行排序。           |
| 添加电话号码列                         | 在 `<tr>` 中扩展为 `<td>{{Phone}}</td>`，并在每个 person 对象中加入 `Phone`。 |
| 大数据集（数百行）                     | 将行分块渲染或使用虚拟滚动，以保持 UI 响应。                             |

## 完整工作示例

下面是可以直接复制到 `index.html` 的完整 HTML 文件，包含上述所有部分。

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

**预期输出**

页面渲染出一个包含两行的表格，每行显示人员的全名和格式化地址。向 `Person` 数组中添加更多对象会自动新增行——演示了 **如何生成表格** 元素的过程。

## 结论

现在您已经掌握了 **如何将数据绑定** 到 **动态 HTML 表格**，为每条记录生成行，并在地址旁显示名字和姓氏。

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Enable JavaScript in Aspose HTML – Load HTML & Get Text](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}