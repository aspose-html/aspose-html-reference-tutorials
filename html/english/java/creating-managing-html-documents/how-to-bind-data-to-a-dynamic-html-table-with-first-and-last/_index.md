---
category: general
date: 2026-09-07
description: how to bind data in a dynamic HTML table – learn how to generate table
  rows and populate first and last name fields efficiently
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: en
lastmod: 2026-09-07
og_description: how to bind data in a dynamic HTML table. This tutorial shows how
  to generate table rows, display first and last name, and populate table rows with
  JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: How to bind data to a dynamic HTML table – step‑by‑step guide
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
title: How to bind data to a dynamic HTML table with first and last name columns
url: /java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to bind data to a dynamic HTML table with first and last name columns

If you need to **how to bind data** into a table that grows with each record, this guide shows a complete solution. You’ll see how to generate a dynamic HTML table, populate table rows, and display each person’s first and last name without writing repetitive markup.

The example uses a lightweight templating syntax that works in any modern browser, but the concepts apply to Handlebars, Mustache, or server‑side engines alike. By the end of the tutorial you can copy the code into your project and start binding data instantly.

## What this tutorial covers

* How to structure a data source that contains multiple persons  
* How to create a reusable table template that repeats for each entry  
* How to bind the data and generate the final HTML markup  
* Common pitfalls when populating table rows and how to avoid them  

No external libraries are required, although the same pattern works with popular templating frameworks. The only prerequisite is basic HTML and JavaScript knowledge.

## Prerequisites

* A modern browser (Chrome, Edge, Firefox, or Safari)  
* An editor for HTML/JavaScript files  
* Optional: a JSON file or JavaScript object that represents the persons collection  

## Step 1: Define the data source

First, create a JavaScript object that mirrors the structure used in the template. Each person has a first name, last name, and an address object.

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

**Why this matters:** The object hierarchy (`Persons.Person`) matches the `{{#foreach Persons.Person}}` loop in the template, allowing the engine to iterate over every entry automatically.

## Step 2: Write the table template with a repeat block

The template below uses a simple Mustache‑style syntax (`{{#foreach}}`) to repeat the `<tr>` for each person. Place the template inside a `<script type="text/template">` tag so the browser ignores it until you process it.

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

**Why this matters:** The `{{#foreach Persons.Person}}` directive tells the engine to repeat everything between the opening and closing tags for each person object. Inside the row you can reference any property (`{{FirstName}}`, `{{LastName}}`, etc.) to **populate table rows** dynamically.

## Step 3: Implement a tiny rendering function

Because the tutorial must be self‑contained, we’ll write a minimal renderer that replaces the Mustache‑style placeholders with real values. The function walks the data object, expands the repeat block, and injects the final HTML into the page.

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

**Why this matters:** The renderer demonstrates **how to generate table** markup programmatically without pulling in a full library. It also clarifies the transformation from template to final HTML, which helps you adapt the code to other templating engines later.

## Step 4: Add a placeholder where the generated table will appear

Create an empty `<div>` that the script will fill after rendering.

```html
<div id="output"></div>
```

When the page loads, the script replaces this `<div>`’s contents with the fully populated table.

## Step 5: Verify the result

Open the HTML file in a browser. You should see a table that lists each person’s full name and address:

| Person          | Address                         |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

If you add more objects to the `data.Persons.Person` array, the table automatically grows—fulfilling the **populate table rows** requirement.

## Pro tip: handling empty collections

When the data array is empty, the renderer currently outputs an empty table header. To provide a clearer user experience, add a guard:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

This small change prevents an empty table from appearing and gives users immediate feedback.

## Common variations and edge cases

| Situation                               | Adjustment                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| Using a server‑side engine (e.g., Handlebars) | Replace the custom `renderTemplate` with `Handlebars.compile` and pass the same data object. |
| Need to sort rows alphabetically       | Sort `data.Persons.Person` before calling `renderTemplate`.               |
| Adding a column for phone number       | Extend the `<tr>` with `<td>{{Phone}}</td>` and include `Phone` in each person object. |
| Large data sets (hundreds of rows)     | Render rows in chunks or use virtual scrolling to keep the UI responsive. |

## Full working example

Below is the complete HTML file you can copy‑paste into `index.html`. It contains all the pieces discussed above.

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

**Expected output**

The page renders a table with two rows, each showing the full name and formatted address of a person. Adding more objects to the `Person` array automatically adds new rows—demonstrating **how to generate table** elements from data.

## Conclusion

You now know **how to bind data** to a **dynamic HTML table**, generate rows for each record, and display first and last name values alongside address


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Enable JavaScript in Aspose HTML – Load HTML & Get Text](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}