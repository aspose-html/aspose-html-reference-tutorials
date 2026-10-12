---
category: general
date: 2026-10-12
description: Lär dig hur du genererar en tabell från data och fyller i tabellen från
  JSON med Handlebars. Steg‑för‑steg‑guide för att upprepa tabellrader i dynamiska
  HTML‑tabeller.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: sv
lastmod: 2026-10-12
og_description: Generera tabell från data och fyll tabellen med JSON med hjälp av
  Handlebars. Följ den här handledningen för att skapa dynamiska HTML‑tabeller med
  upprepade rader.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Skapa tabell från data med Handlebars – komplett guide
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
title: Hur man genererar en tabell från data med HTML och Handlebars
url: /sv/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man genererar tabell från data med HTML och Handlebars

Om du behöver **generera tabell från data** på en webbsida visar den här handledningen exakt hur. Med en enkel Handlebars‑loop kan du **fylla tabell från JSON**, skapa **repeat table rows**, och få en helt **dynamic HTML table** som uppdateras när källan ändras.

Under de kommande minuterna kommer du att se ett komplett, körbart exempel, förstå varför varje del är viktig, och lära dig hur du anpassar mönstret för mer komplexa scenarier som villkorsstyrda kolumner eller nästlade objekt.

## Vad du kommer att bygga

Vi kommer att skapa en HTML‑tabell som:

* Läser ett JSON‑payload som innehåller en lista med personer.
* Upprepar en tabellrad för varje person (`repeat table rows`).
* Sätter in varje persons förnamn, efternamn och adress i respektive celler.
* Fungerar utan någon server‑sidrendering – hela processen sker i webbläsaren.

**Förutsättningar**

* Grundläggande kunskap om HTML och JavaScript.
* En modern webbläsare (Chrome, Edge, Firefox eller Safari).
* Handlebars.js – vi laddar den från en CDN, så inga byggverktyg behövs.

---

## Steg 1: Förbered JSON‑datakällan

Det första steget är att definiera ett JavaScript‑objekt som efterliknar den JSON du skulle få från ett API. Handlebars fungerar med enkla objekt, så du kan bädda in datan direkt i en `<script>`‑tagg för demonstrationsändamål.

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

**Varför detta är viktigt** – Genom att hålla datan i ett separat `<script>`‑element kan du enkelt byta ut den mot ett riktigt AJAX‑anrop senare. Strukturen (`Persons.Person`) matchar sökvägen som används i Handlebars‑blocket `{{#foreach Persons.Person}}`, vilket är avgörande för **populate table from JSON**.

---

## Steg 2: Skriv Handlebars‑mallen som upprepar rader

Nästa steg är att skapa ett `<script type="text/x-handlebars-template">`‑block som innehåller tabell‑markupen. Handlebars kommer att ersätta platshållarna med faktiska värden och upprepa `<tr>` för varje person.

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

**Förklaring av nyckeldelarna**

* `{{#foreach Persons.Person}}` instruerar Handlebars att **repeat table rows** för varje post i `Persons.Person`‑arrayen.
* `{{FirstName}} {{LastName}}`‑ och `{{Address.*}}`‑uttrycken hämtar värden från det aktuella array‑elementet.
* Att omsluta hela tabellen i ett `data_merge`‑attribut är valfritt; det kan vara användbart för efterföljande bearbetning eller CSS‑selektorer.

---

## Steg 3: Ladda Handlebars och kompilera mallen

Vi hämtar Handlebars från en CDN, parsar JSON‑datan, kompilerar mallen och injicerar den slutgiltiga HTML‑koden i sidan.

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

**Varför kompilera vid körning?** – Att kompilera mallen en gång och återanvända den håller sidan snabb, särskilt när datan förändras ofta. Detta mönster gör det också enkelt att **populate table from JSON** flera gånger utan att ladda om sidan.

---

## Steg 4: Reservera en behållare för den genererade tabellen

Lägg till en platshållare `<div>` där den dynamiska tabellen ska visas. Detta håller markupen ren och separerar ansvaret mellan statisk layout och genererat innehåll.

```html
<div id="output"></div>
```

När skriptet från Steg 3 körs kommer `<div id="output">` att innehålla ett fullständigt `<table>`‑element, redo för styling eller vidare manipulation.

---

## Steg 5: Verifiera resultatet och stilisera tabellen (valfritt)

Öppna sidan i en webbläsare så bör du se en tabell som den nedan:

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

**Valfri styling** – Om du vill ha ett renare utseende, lägg till några CSS‑regler:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Hantera kantfall och vanliga variationer

### 1. Tomma dataset

Om JSON‑arrayen är tom kommer Handlebars fortfarande rendera rubrikraden men inga datarader. För att visa ett vänligt meddelande, omslut tabellen i ett villkorsblock:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Nästlade loopar (t.ex. flera adresser per person)

När en person kan ha flera adresser kan du nästla ett annat `{{#foreach}}` inuti raden:

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

### 3. Använda ett riktigt API

Byt ut den statiska `<script id="people-data">` mot ett fetch‑anrop:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Detta demonstrerar samma **dynamic table rows**‑teknik samtidigt som den hämtar levande data.

### 4. Tillgänglighetsaspekter

* Lägg till `scope="col"` på `<th>`‑elementen.
* Använd `<caption>` för att beskriva tabellens syfte.
* Säkerställ tillräcklig färgkontrast om du använder anpassad CSS.

---

## Fullt, körbart exempel

Kopiera följande block till en `index.html`‑fil och öppna den i en webbläsare. Sidan kommer att **generate table from data**, **populate table from JSON**, och automatiskt upprepa rader.

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

**Förväntat resultat**

En två‑radig tabell (plus rubrik) som visar “Alice Anderson” och “Bob Baker” med deras respektive adresser. Sidan fungerar offline, vilket bevisar att du kan **generate table from data** utan någon serverkomponent.

---

## Slutsats

Du vet nu hur du **generate table from data** med en Handlebars‑mall, **populate table from JSON**, och skapar **repeat table rows** som bildar en **dynamic HTML table**. Mönstret skalar till större dataset, nästlade strukturer och levande API‑anrop, vilket ger dig en robust grund för all klient‑sid rapportering eller admin‑UI.

**Nästa steg**

* Utforska Handlebars‑helpers för formatering av datum eller tal.
* Kombinera detta tillvägagångssätt med CSS Grid eller Flexbox för responsiva tabelllayouter.
* Integrera paginerings‑ eller sorteringsbibliotek för att hantera mycket stora dataset.

Känn dig fri att experimentera med olika JSON‑strukturer, lägga till villkorliga kolumner eller byta Handlebars mot en annan mallmotor – dina nya färdigheter låter dig bygga flexibla, data‑drivna gränssnitt snabbt och pålitligt.

---

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa HTML-dokument med Java – Hämta JSON och generera innehåll](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Datahantering och strömhantering i Aspose.HTML för Java](/html/english/java/data-handling-stream-management/)
- [Hur man laddar HTML i Java – Steg‑för‑steg‑guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}