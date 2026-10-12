---
category: general
date: 2026-10-12
description: Learn how to generate table from data and populate table from JSON using
  Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: en
lastmod: 2026-10-12
og_description: Generate table from data and populate table from JSON using Handlebars.
  Follow this tutorial to create dynamic HTML tables with repeat table rows.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Generate table from data with Handlebars – complete guide
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
title: How to generate table from data with HTML and Handlebars
url: /java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to generate table from data with HTML and Handlebars

If you need to **generate table from data** in a web page, this tutorial shows you exactly how. Using a simple Handlebars loop you can **populate table from JSON**, create **repeat table rows**, and end up with a fully **dynamic HTML table** that updates whenever the source changes.

In the next few minutes you’ll see a complete, runnable example, understand why each piece matters, and learn how to adapt the pattern for more complex scenarios such as conditional columns or nested objects.

## What you’ll build

We’ll create an HTML table that:

* Reads a JSON payload containing a list of persons.
* Repeats a table row for every person (`repeat table rows`).
* Inserts each person’s first name, last name, and address into the appropriate cells.
* Works without any server‑side rendering – the entire process happens in the browser.

**Prerequisites**

* Basic knowledge of HTML and JavaScript.
* A modern browser (Chrome, Edge, Firefox, or Safari).
* Handlebars.js – we’ll load it from a CDN, so no build tools are required.

---

## Step 1: Prepare the JSON data source

The first step is to define a JavaScript object that mimics the JSON you’d receive from an API. Handlebars works with plain objects, so you can embed the data directly in a `<script>` tag for demonstration purposes.

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

**Why this matters** – By keeping the data in a separate `<script>` element you can easily swap it out with a real AJAX call later. The structure (`Persons.Person`) matches the path used in the Handlebars `{{#foreach Persons.Person}}` block, which is essential for **populate table from JSON**.

---

## Step 2: Write the Handlebars template that repeats rows

Next, create a `<script type="text/x-handlebars-template">` block that contains the table markup. Handlebars will replace the placeholders with actual values and repeat the `<tr>` for each person.

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

**Explanation of the key parts**

* `{{#foreach Persons.Person}}` tells Handlebars to **repeat table rows** for every entry in the `Persons.Person` array.
* The `{{FirstName}} {{LastName}}` and `{{Address.*}}` expressions pull values from the current array element.
* Wrapping the whole table in a `data_merge` attribute is optional; it can be useful for downstream processing or CSS selectors.

---

## Step 3: Load Handlebars and compile the template

We’ll pull Handlebars from a CDN, parse the JSON, compile the template, and inject the final HTML into the page.

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

**Why compile at runtime?** – Compiling the template once and re‑using it keeps the page fast, especially when the data changes frequently. This pattern also makes it trivial to **populate table from JSON** multiple times without reloading the page.

---

## Step 4: Reserve a container for the generated table

Add a placeholder `<div>` where the dynamic table will appear. This keeps the markup clean and separates concerns between static layout and generated content.

```html
<div id="output"></div>
```

When the script from Step 3 runs, the `<div id="output">` will contain a fully formed `<table>` element, ready for styling or further manipulation.

---

## Step 5: Verify the output and style the table (optional)

Open the page in a browser and you should see a table like the one below:

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

**Optional styling** – If you want a cleaner look, add a few CSS rules:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Handling edge cases and common variations

### 1. Empty data sets

If the JSON array is empty, Handlebars will still render the header row but no data rows. To display a friendly message, wrap the table in a conditional block:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Nested loops (e.g., multiple addresses per person)

When a person can have several addresses, you can nest another `{{#foreach}}` inside the row:

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

### 3. Using a real API

Replace the static `<script id="people-data">` with a fetch call:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

This demonstrates the same **dynamic table rows** technique while pulling live data.

### 4. Accessibility considerations

* Add `scope="col"` to `<th>` elements.
* Use `<caption>` to describe the table purpose.
* Ensure sufficient color contrast if you apply custom CSS.

---

## Full, runnable example

Copy the following block into an `index.html` file and open it in a browser. The page will **generate table from data**, **populate table from JSON**, and repeat rows automatically.

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

**Expected result**

A two‑row table (plus header) showing “Alice Anderson” and “Bob Baker” with their respective addresses. The page works offline, proving that you can **generate table from data** without any server component.

---

## Conclusion

You now know how to **generate table from data** using a Handlebars template, **populate table from JSON**, and create **repeat table rows** that form a **dynamic HTML table**. The pattern scales to larger data sets, nested structures, and live API calls, giving you a robust foundation for any client‑side reporting or admin UI.

**Next steps**

* Explore Handlebars helpers for formatting dates or numbers.
* Combine this approach with CSS Grid or Flexbox for responsive table layouts.
* Integrate pagination or sorting libraries to handle very large data sets.

Feel free to experiment with different JSON shapes, add conditional columns, or swap Handlebars for another templating engine—your new skills will let you build flexible, data‑driven interfaces quickly and reliably.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}