---
category: general
date: 2026-10-12
description: Impara come generare una tabella dai dati e popolare la tabella da JSON
  usando Handlebars. Guida passo‑passo per ripetere le righe della tabella in tabelle
  HTML dinamiche.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: it
lastmod: 2026-10-12
og_description: Genera una tabella dai dati e popola la tabella da JSON usando Handlebars.
  Segui questo tutorial per creare tabelle HTML dinamiche con righe di tabella ripetute.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Genera una tabella dai dati con Handlebars – guida completa
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
title: Come generare una tabella dai dati con HTML e Handlebars
url: /it/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come generare una tabella dai dati con HTML e Handlebars

Se hai bisogno di **generare una tabella dai dati** in una pagina web, questo tutorial ti mostra esattamente come fare. Utilizzando un semplice ciclo Handlebars puoi **popolare la tabella da JSON**, creare **righe di tabella ripetute** e ottenere una **tabella HTML dinamica** che si aggiorna ogni volta che la fonte cambia.

Nei prossimi minuti vedrai un esempio completo e funzionante, comprenderai perché ogni parte è importante e imparerai a adattare il modello a scenari più complessi, come colonne condizionali o oggetti nidificati.

## What you’ll build

Creeremo una tabella HTML che:

* Legge un payload JSON contenente un elenco di persone.
* Ripete una riga di tabella per ogni persona (`repeat table rows`).
* Inserisce il nome, il cognome e l’indirizzo di ciascuna persona nelle celle appropriate.
* Funziona senza alcun rendering lato server – l’intero processo avviene nel browser.

**Prerequisites**

* Conoscenze di base di HTML e JavaScript.
* Un browser moderno (Chrome, Edge, Firefox o Safari).
* Handlebars.js – lo caricheremo da un CDN, quindi non sono necessari strumenti di build.

---

## Step 1: Prepare the JSON data source

Il primo passo è definire un oggetto JavaScript che imiti il JSON che riceveresti da un’API. Handlebars funziona con oggetti semplici, quindi puoi incorporare i dati direttamente in un tag `<script>` a scopo dimostrativo.

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

**Why this matters** – Tenendo i dati in un elemento `<script>` separato, puoi facilmente sostituirli più tardi con una vera chiamata AJAX. La struttura (`Persons.Person`) corrisponde al percorso usato nel blocco Handlebars `{{#foreach Persons.Person}}`, fondamentale per **populate table from JSON**.

---

## Step 2: Write the Handlebars template that repeats rows

Successivamente, crea un blocco `<script type="text/x-handlebars-template">` che contenga il markup della tabella. Handlebars sostituirà i segnaposto con i valori reali e ripeterà il `<tr>` per ogni persona.

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

* `{{#foreach Persons.Person}}` indica a Handlebars di **repeat table rows** per ogni elemento dell’array `Persons.Person`.
* Le espressioni `{{FirstName}} {{LastName}}` e `{{Address.*}}` estraggono i valori dall’elemento corrente dell’array.
* Avvolgere l’intera tabella in un attributo `data_merge` è opzionale; può essere utile per elaborazioni successive o per selettori CSS.

---

## Step 3: Load Handlebars and compile the template

Caricheremo Handlebars da un CDN, analizzeremo il JSON, compileremo il template e inietteremo l’HTML finale nella pagina.

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

**Why compile at runtime?** – Compilare il template una sola volta e riutilizzarlo mantiene la pagina veloce, soprattutto quando i dati cambiano frequentemente. Questo modello rende anche banale **populate table from JSON** più volte senza ricaricare la pagina.

---

## Step 4: Reserve a container for the generated table

Aggiungi un placeholder `<div>` dove apparirà la tabella dinamica. Questo mantiene il markup pulito e separa le preoccupazioni tra layout statico e contenuto generato.

```html
<div id="output"></div>
```

Quando lo script del Passo 3 verrà eseguito, il `<div id="output">` conterrà un elemento `<table>` completamente formato, pronto per lo styling o ulteriori manipolazioni.

---

## Step 5: Verify the output and style the table (optional)

Apri la pagina in un browser e dovresti vedere una tabella simile a quella mostrata qui sotto:

![Screenshot che mostra la tabella generata dai dati](image.png "Screenshot che mostra la tabella generata dai dati")

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

**Optional styling** – Se desideri un aspetto più pulito, aggiungi qualche regola CSS:

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

Se l’array JSON è vuoto, Handlebars renderizzerà comunque la riga di intestazione ma nessuna riga di dati. Per mostrare un messaggio amichevole, avvolgi la tabella in un blocco condizionale:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Nested loops (e.g., multiple addresses per person)

Quando una persona può avere più indirizzi, puoi annidare un altro `{{#foreach}}` all’interno della riga:

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

Sostituisci il `<script id="people-data">` statico con una chiamata fetch:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Questo dimostra la stessa tecnica di **dynamic table rows** estraendo dati in tempo reale.

### 4. Accessibility considerations

* Aggiungi `scope="col"` agli elementi `<th>`.
* Usa `<caption>` per descrivere lo scopo della tabella.
* Assicurati di avere un contrasto di colore sufficiente se applichi CSS personalizzato.

---

## Full, runnable example

Copia il blocco seguente in un file `index.html` e aprilo in un browser. La pagina **genererà una tabella dai dati**, **popolerà la tabella da JSON** e ripeterà le righe automaticamente.

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

Una tabella a due righe (più l’intestazione) che mostra “Alice Anderson” e “Bob Baker” con i rispettivi indirizzi. La pagina funziona offline, dimostrando che puoi **generate table from data** senza alcun componente server.

---

## Conclusion

Ora sai come **generate table from data** usando un template Handlebars, **populate table from JSON** e creare **repeat table rows** che formano una **dynamic HTML table**. Il modello scala a set di dati più grandi, strutture nidificate e chiamate API live, fornendoti una base solida per qualsiasi reporting client‑side o interfaccia admin.

**Next steps**

* Esplora gli helper di Handlebars per formattare date o numeri.
* Combina questo approccio con CSS Grid o Flexbox per layout di tabelle responsive.
* Integra librerie di paginazione o ordinamento per gestire set di dati molto grandi.

Sentiti libero di sperimentare con forme JSON diverse, aggiungere colonne condizionali o sostituire Handlebars con un altro motore di templating – le tue nuove competenze ti permetteranno di costruire interfacce flessibili, guidate dai dati, rapidamente e in modo affidabile.

## What Should You Learn Next?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea documento HTML con Java – Recupera JSON e genera contenuto](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Gestione dei dati e dei flussi in Aspose.HTML per Java](/html/english/java/data-handling-stream-management/)
- [Come caricare HTML in Java – Guida passo‑passo](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}