---
category: general
date: 2026-09-07
description: hoe data te binden in een dynamische HTML‑tabel – leer hoe je tabelrijen
  genereert en de velden voor voor‑ en achternaam efficiënt vult
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: nl
lastmod: 2026-09-07
og_description: hoe data te binden in een dynamische HTML‑tabel. Deze tutorial laat
  zien hoe je tabelrijen genereert, voor‑ en achternaam weergeeft en tabelrijen vult
  met JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Hoe je data bindt aan een dynamische HTML‑tabel – stapsgewijze handleiding
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
title: Hoe gegevens binden aan een dynamische HTML‑tabel met kolommen voor voor‑ en
  achternaam
url: /nl/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe data te binden aan een dynamische HTML-tabel met kolommen voor voor- en achternaam

Als je **hoe data te binden** in een tabel die groeit met elk record, laat deze gids een volledige oplossing zien. Je zult zien hoe je een dynamische HTML-tabel genereert, tabelrijen vult en de voor‑ en achternaam van elke persoon weergeeft zonder repetitieve markup te schrijven.

Het voorbeeld gebruikt een lichtgewicht templating‑syntaxis die werkt in elke moderne browser, maar de concepten zijn toepasbaar op Handlebars, Mustache of server‑side engines. Aan het einde van de tutorial kun je de code naar je project kopiëren en direct data binden.

## Wat deze tutorial behandelt

* Hoe een gegevensbron te structureren die meerdere personen bevat  
* Hoe een herbruikbare tabeltemplate te maken die voor elke invoer wordt herhaald  
* Hoe de data te binden en de uiteindelijke HTML‑markup te genereren  
* Veelvoorkomende valkuilen bij het vullen van tabelrijen en hoe deze te vermijden  

Er zijn geen externe bibliotheken nodig, hoewel hetzelfde patroon werkt met populaire templating‑frameworks. De enige voorwaarde is basiskennis van HTML en JavaScript.

## Voorvereisten

* Een moderne browser (Chrome, Edge, Firefox of Safari)  
* Een editor voor HTML/JavaScript‑bestanden  
* Optioneel: een JSON‑bestand of JavaScript‑object dat de personen‑collectie vertegenwoordigt  

## Stap 1: Definieer de gegevensbron

Eerst maak je een JavaScript‑object dat de structuur van de template weerspiegelt. Elke persoon heeft een voornaam, achternaam en een adresobject.

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

**Waarom dit belangrijk is:** De objecthiërarchie (`Persons.Person`) komt overeen met de `{{#foreach Persons.Person}}`‑lus in de template, waardoor de engine automatisch over elk item kan itereren.

## Stap 2: Schrijf de tabeltemplate met een herhaalblok

De onderstaande template gebruikt een eenvoudige Mustache‑style syntaxis (`{{#foreach}}`) om de `<tr>` voor elke persoon te herhalen. Plaats de template binnen een `<script type="text/template">`‑tag zodat de browser deze negeert totdat je hem verwerkt.

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

**Waarom dit belangrijk is:** De `{{#foreach Persons.Person}}`‑directive vertelt de engine om alles tussen de opening‑ en sluit‑tags te herhalen voor elk persoon‑object. Binnen de rij kun je elke eigenschap refereren (`{{FirstName}}`, `{{LastName}}`, enz.) om **tabelrijen dynamisch te vullen**.

## Stap 3: Implementeer een kleine renderfunctie

Omdat de tutorial zelf‑voorzienend moet zijn, schrijven we een minimale renderer die de Mustache‑style placeholders vervangt door echte waarden. De functie doorloopt het data‑object, breidt het herhaalblok uit en injecteert de uiteindelijke HTML in de pagina.

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

**Waarom dit belangrijk is:** De renderer toont **hoe een tabel**‑markup programmatisch te genereren zonder een volledige bibliotheek te gebruiken. Het verduidelijkt ook de transformatie van template naar uiteindelijke HTML, wat je later helpt de code aan te passen voor andere templating‑engines.

## Stap 4: Voeg een placeholder toe waar de gegenereerde tabel zal verschijnen

Maak een lege `<div>` die het script na het renderen zal vullen.

```html
<div id="output"></div>
```

Wanneer de pagina laadt, vervangt het script de inhoud van dit `<div>`‑element door de volledig ingevulde tabel.

## Stap 5: Verifieer het resultaat

Open het HTML‑bestand in een browser. Je zou een tabel moeten zien die de volledige naam en het adres van elke persoon opsomt:

| Person          | Address                         |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Als je meer objecten toevoegt aan de `data.Persons.Person`‑array, groeit de tabel automatisch — wat voldoet aan de **populate table rows**‑vereiste.

## Pro tip: omgaan met lege collecties

Wanneer de data‑array leeg is, geeft de renderer momenteel een lege tabelkop weer. Voeg een guard toe om een duidelijkere gebruikerservaring te bieden:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Deze kleine wijziging voorkomt dat een lege tabel verschijnt en geeft gebruikers directe feedback.

## Veelvoorkomende variaties en randgevallen

| Situatie                               | Aanpassing                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| Een server‑side engine gebruiken (bijv. Handlebars) | Vervang de aangepaste `renderTemplate` door `Handlebars.compile` en geef hetzelfde data‑object door. |
| Rijen alfabetisch sorteren             | Sorteer `data.Persons.Person` vóór het aanroepen van `renderTemplate`.               |
| Een kolom voor telefoonnummer toevoegen | Breid de `<tr>` uit met `<td>{{Phone}}</td>` en voeg `Phone` toe aan elk persoon‑object. |
| Grote datasets (honderden rijen)      | Render rijen in delen of gebruik virtueel scrollen om de UI responsief te houden. |

## Volledig werkend voorbeeld

Hieronder vind je het complete HTML‑bestand dat je kunt kopiëren‑plakken in `index.html`. Het bevat alle besproken onderdelen.

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

**Verwachte output**

De pagina rendert een tabel met twee rijen, waarbij elke rij de volledige naam en het geformatteerde adres van een persoon toont. Het toevoegen van meer objecten aan de `Person`‑array voegt automatisch nieuwe rijen toe — wat **hoe een tabel**‑elementen uit data te genereren demonstreert.

## Conclusie

Je weet nu **hoe data te binden** aan een **dynamische HTML‑tabel**, rijen voor elk record te genereren en voor‑ en achternaamwaarden naast het adres weer te geven.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe CSS toe te voegen – Inline CSS aan HTML‑documenten in Aspose.HTML voor Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Hoe de HTML‑documentboom te bewerken in Aspose.HTML voor Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Hoe JavaScript in te schakelen in Aspose HTML – HTML laden & tekst ophalen](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}