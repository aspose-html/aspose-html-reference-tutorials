---
category: general
date: 2026-10-12
description: Leer hoe je een tabel genereert uit gegevens en een tabel vult vanuit
  JSON met Handlebars. Stapsgewijze handleiding voor het herhalen van tabelrijen in
  dynamische HTML‑tabellen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: nl
lastmod: 2026-10-12
og_description: Genereer een tabel uit gegevens en vul de tabel met JSON via Handlebars.
  Volg deze tutorial om dynamische HTML‑tabellen te maken met herhaalde tabelrijen.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Genereer tabel uit gegevens met Handlebars – volledige gids
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
title: Hoe een tabel te genereren uit data met HTML en Handlebars
url: /nl/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een tabel te genereren uit gegevens met HTML en Handlebars

Als je een **tabel uit gegevens moet genereren** op een webpagina, laat deze tutorial je precies zien hoe. Met een eenvoudige Handlebars‑lus kun je **tabel vullen vanuit JSON**, **tabelrijen herhalen**, en eindigen met een volledig **dynamische HTML‑tabel** die wordt bijgewerkt zodra de bron verandert.

In de komende paar minuten zie je een compleet, uitvoerbaar voorbeeld, begrijp je waarom elk onderdeel belangrijk is, en leer je hoe je het patroon kunt aanpassen voor complexere scenario's zoals voorwaardelijke kolommen of geneste objecten.

## Wat je gaat bouwen

We zullen een HTML‑tabel maken die:

* Leest een JSON‑payload die een lijst van personen bevat.
* Herhaalt een tabelrij voor elke persoon (`repeat table rows`).
* Plaatst de voornaam, achternaam en adres van elke persoon in de juiste cellen.
* Werkt zonder server‑side rendering – het volledige proces gebeurt in de browser.

**Voorvereisten**

* Basiskennis van HTML en JavaScript.
* Een moderne browser (Chrome, Edge, Firefox of Safari).
* Handlebars.js – we laden het van een CDN, dus er zijn geen build‑tools nodig.

---

## Stap 1: Bereid de JSON‑gegevensbron voor

De eerste stap is het definiëren van een JavaScript‑object dat de JSON nabootst die je van een API zou ontvangen. Handlebars werkt met gewone objecten, dus je kunt de gegevens direct in een `<script>`‑tag opnemen voor demonstratiedoeleinden.

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

**Waarom dit belangrijk is** – Door de gegevens in een apart `<script>`‑element te plaatsen, kun je ze later eenvoudig vervangen door een echte AJAX‑aanroep. De structuur (`Persons.Person`) komt overeen met het pad dat wordt gebruikt in de Handlebars `{{#foreach Persons.Person}}`‑block, wat essentieel is voor **populate table from JSON**.

## Stap 2: Schrijf de Handlebars‑template die rijen herhaalt

Vervolgens maak je een `<script type="text/x-handlebars-template">`‑block dat de tabel‑markup bevat. Handlebars zal de placeholders vervangen door de werkelijke waarden en de `<tr>` voor elke persoon herhalen.

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

**Uitleg van de belangrijkste onderdelen**

* `{{#foreach Persons.Person}}` vertelt Handlebars om **repeat table rows** uit te voeren voor elk item in de `Persons.Person`‑array.
* De `{{FirstName}} {{LastName}}`‑ en `{{Address.*}}`‑expressies halen waarden op uit het huidige array‑element.
* Het omhullen van de hele tabel in een `data_merge`‑attribuut is optioneel; het kan nuttig zijn voor downstream‑verwerking of CSS‑selectors.

## Stap 3: Laad Handlebars en compileer de template

We halen Handlebars van een CDN, parseren de JSON, compileren de template en injecteren de uiteindelijke HTML in de pagina.

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

**Waarom compileren tijdens runtime?** – Het één keer compileren van de template en hergebruiken ervan houdt de pagina snel, vooral wanneer de gegevens vaak veranderen. Dit patroon maakt het bovendien triviaal om **populate table from JSON** meerdere keren uit te voeren zonder de pagina te herladen.

## Stap 4: Reserveer een container voor de gegenereerde tabel

Voeg een placeholder `<div>` toe waar de dynamische tabel zal verschijnen. Dit houdt de markup schoon en scheidt de zorgen tussen statische layout en gegenereerde inhoud.

```html
<div id="output"></div>
```

Wanneer het script uit Stap 3 wordt uitgevoerd, zal de `<div id="output">` een volledig gevormd `<table>`‑element bevatten, klaar voor styling of verdere manipulatie.

## Stap 5: Controleer de output en style de tabel (optioneel)

Open de pagina in een browser en je zou een tabel moeten zien zoals hieronder:

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

**Optionele styling** – Als je een nettere uitstraling wilt, voeg dan een paar CSS‑regels toe:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

## Omgaan met randgevallen en veelvoorkomende variaties

### 1. Lege datasets

Als de JSON‑array leeg is, zal Handlebars nog steeds de header‑rij renderen maar geen gegevensrijen. Om een vriendelijke boodschap weer te geven, wikkel je de tabel in een conditionele block:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Geneste lussen (bijv. meerdere adressen per persoon)

Wanneer een persoon meerdere adressen kan hebben, kun je een andere `{{#foreach}}` binnen de rij nesten:

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

### 3. Een echte API gebruiken

Vervang de statische `<script id="people-data">` door een fetch‑aanroep:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Dit demonstreert dezelfde **dynamic table rows**‑techniek terwijl er live data wordt opgehaald.

### 4. Toegankelijkheidsaspecten

* Voeg `scope="col"` toe aan `<th>`‑elementen.
* Gebruik `<caption>` om het doel van de tabel te beschrijven.
* Zorg voor voldoende kleurcontrast als je aangepaste CSS toepast.

## Volledig, uitvoerbaar voorbeeld

Kopieer het volgende blok naar een `index.html`‑bestand en open het in een browser. De pagina zal **generate table from data**, **populate table from JSON** en rijen automatisch herhalen.

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

**Verwacht resultaat**

Een tabel met twee rijen (plus header) die “Alice Anderson” en “Bob Baker” toont met hun respectieve adressen. De pagina werkt offline, wat bewijst dat je **generate table from data** kunt uitvoeren zonder enige servercomponent.

## Conclusie

Je weet nu hoe je **generate table from data** kunt gebruiken met een Handlebars‑template, **populate table from JSON**, en **repeat table rows** kunt maken die een **dynamic HTML table** vormen. Het patroon schaalt naar grotere datasets, geneste structuren en live API‑calls, waardoor je een robuuste basis krijgt voor elke client‑side rapportage of admin‑UI.

**Volgende stappen**

* Verken Handlebars‑helpers voor het formatteren van datums of getallen.
* Combineer deze aanpak met CSS Grid of Flexbox voor responsieve tabel‑lay-outs.
* Integreer paginering‑ of sorteer‑bibliotheken om zeer grote datasets te verwerken.

Voel je vrij om te experimenteren met verschillende JSON‑structuren, voorwaardelijke kolommen toe te voegen, of Handlebars te vervangen door een andere templating‑engine—je nieuwe vaardigheden stellen je in staat om snel en betrouwbaar flexibele, data‑gedreven interfaces te bouwen.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [HTML‑document maken met Java – JSON ophalen en inhoud genereren](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Gegevensverwerking en stream‑beheer in Aspose.HTML voor Java](/html/english/java/data-handling-stream-management/)
- [HTML laden in Java – Stapsgewijze handleiding](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}