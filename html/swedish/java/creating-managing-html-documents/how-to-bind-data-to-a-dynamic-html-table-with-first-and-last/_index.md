---
category: general
date: 2026-09-07
description: hur man binder data i en dynamisk HTML‑tabell – lär dig hur du genererar
  tabellrader och fyller i fält för för- och efternamn effektivt
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: sv
lastmod: 2026-09-07
og_description: hur man binder data i en dynamisk HTML‑tabell. Denna handledning visar
  hur man genererar tabellrader, visar för‑ och efternamn samt fyller tabellrader
  med JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Hur man binder data till en dynamisk HTML‑tabell – steg‑för‑steg‑guide
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
title: Hur man binder data till en dynamisk HTML‑tabell med kolumner för förnamn och
  efternamn
url: /sv/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så binder du data till en dynamisk HTML‑tabell med kolumner för för- och efternamn

Om du behöver **binda data** till en tabell som växer med varje post, visar den här guiden en komplett lösning. Du får se hur du genererar en dynamisk HTML‑tabell, fyller på tabellrader och visar varje persons för‑ och efternamn utan att skriva repetitiv markup.

Exemplet använder en lättviktig mallsyntaks som fungerar i alla moderna webbläsare, men koncepten gäller även för Handlebars, Mustache eller server‑side‑motorer. När du är klar med tutorialen kan du kopiera koden till ditt projekt och börja binda data omedelbart.

## Vad den här tutorialen täcker

* Hur du strukturerar en datakälla som innehåller flera personer  
* Hur du skapar en återanvändbar tabellmall som upprepas för varje post  
* Hur du binder data och genererar den slutgiltiga HTML‑markuppen  
* Vanliga fallgropar när du fyller på tabellrader och hur du undviker dem  

Inga externa bibliotek krävs, även om samma mönster fungerar med populära mallramverk. Det enda förutsättningen är grundläggande kunskaper i HTML och JavaScript.

## Förutsättningar

* En modern webbläsare (Chrome, Edge, Firefox eller Safari)  
* En editor för HTML/JavaScript‑filer  
* Valfritt: en JSON‑fil eller ett JavaScript‑objekt som representerar personsamlingen  

## Steg 1: Definiera datakällan

Börja med att skapa ett JavaScript‑objekt som speglar strukturen som används i mallen. Varje person har ett förnamn, efternamn och ett adress‑objekt.

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

**Varför detta är viktigt:** Objekt‑hierarkin (`Persons.Person`) matchar `{{#foreach Persons.Person}}`‑loopen i mallen, vilket låter motorn iterera över varje post automatiskt.

## Steg 2: Skriv tabellmallen med ett upprepningsblock

Mallen nedan använder en enkel Mustache‑liknande syntax (`{{#foreach}}`) för att upprepa `<tr>` för varje person. Placera mallen inuti ett `<script type="text/template">`‑tagg så att webbläsaren ignorerar den tills du bearbetar den.

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

**Varför detta är viktigt:** Direktivet `{{#foreach Persons.Person}}` talar om för motorn att upprepa allt mellan öppnings‑ och stängningstaggarna för varje person‑objekt. Inuti raden kan du referera till vilken egenskap som helst (`{{FirstName}}`, `{{LastName}}` osv.) för att **fylla på tabellrader** dynamiskt.

## Steg 3: Implementera en liten renderingsfunktion

Eftersom tutorialen måste vara självständig skriver vi en minimal renderare som ersätter de Mustache‑liknande platshållarna med riktiga värden. Funktionen går igenom data‑objektet, expanderar upprepningsblocket och injicerar den färdiga HTML‑koden i sidan.

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

**Varför detta är viktigt:** Renderaren visar **hur man genererar tabell**‑markup programatiskt utan att behöva ett fullständigt bibliotek. Den klargör också transformationen från mall till slutlig HTML, vilket underlättar anpassning till andra mallmotorer senare.

## Steg 4: Lägg till en platshållare där den genererade tabellen ska visas

Skapa en tom `<div>` som skriptet fyller i efter rendering.

```html
<div id="output"></div>
```

När sidan laddas ersätter skriptet innehållet i denna `<div>` med den fullständigt ifyllda tabellen.

## Steg 5: Verifiera resultatet

Öppna HTML‑filen i en webbläsare. Du bör se en tabell som listar varje persons fullständiga namn och adress:

| Person          | Adress                         |
|-----------------|--------------------------------|
| Alice Johnson   | Maple 12A, Springfield         |
| Bob Smith       | Oak 34B, Riverdale             |

Om du lägger till fler objekt i `data.Persons.Person`‑arrayen växer tabellen automatiskt – vilket uppfyller kravet på **fylla på tabellrader**.

## Proffstips: hantera tomma samlingar

När data‑arrayen är tom skriver renderaren för närvarande ut ett tomt tabellhuvud. För att ge en tydligare användarupplevelse, lägg till ett skydd:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Denna lilla förändring förhindrar att en tom tabell visas och ger användaren omedelbar återkoppling.

## Vanliga variationer och specialfall

| Situation                               | Justering                                                                 |
|----------------------------------------|---------------------------------------------------------------------------|
| Använda en server‑side‑motor (t.ex. Handlebars) | Ersätt den anpassade `renderTemplate` med `Handlebars.compile` och skicka in samma dataobjekt. |
| Behöva sortera rader alfabetiskt       | Sortera `data.Persons.Person` innan du anropar `renderTemplate`.        |
| Lägga till en kolumn för telefonnummer | Utöka `<tr>` med `<td>{{Phone}}</td>` och inkludera `Phone` i varje person‑objekt. |
| Stora datamängder (hundratals rader)   | Rendera rader i portioner eller använd virtuell scrollning för att hålla UI‑responsivt. |

## Fullt fungerande exempel

Nedan är den kompletta HTML‑filen som du kan kopiera‑klistra in i `index.html`. Den innehåller alla delar som diskuterats ovan.

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

**Förväntat resultat**

Sidan renderar en tabell med två rader, där varje rad visar personens fullständiga namn och formaterade adress. Att lägga till fler objekt i `Person`‑arrayen lägger automatiskt till nya rader – vilket demonstrerar **hur man genererar tabell**‑element från data.

## Slutsats

Du vet nu **hur man binder data** till en **dynamisk HTML‑tabell**, genererar rader för varje post och visar för‑ och efternamn tillsammans med adress.

## Vad bör du lära dig härnäst?

De följande tutorialerna behandlar närliggande ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Enable JavaScript in Aspose HTML – Load HTML & Get Text](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}