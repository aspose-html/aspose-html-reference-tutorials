---
category: general
date: 2026-09-07
description: come collegare i dati in una tabella HTML dinamica – impara a generare
  le righe della tabella e a popolare i campi nome e cognome in modo efficiente
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: it
lastmod: 2026-09-07
og_description: come collegare i dati in una tabella HTML dinamica. Questo tutorial
  mostra come generare le righe della tabella, visualizzare nome e cognome e popolare
  le righe della tabella con JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Come associare i dati a una tabella HTML dinamica – guida passo passo
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
title: Come collegare i dati a una tabella HTML dinamica con colonne nome e cognome
url: /it/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come associare dati a una tabella HTML dinamica con colonne nome e cognome

Se hai bisogno di **come associare dati** a una tabella che cresce con ogni record, questa guida mostra una soluzione completa. Vedrai come generare una tabella HTML dinamica, popolare le righe della tabella e visualizzare il nome e il cognome di ogni persona senza scrivere markup ripetitivo.

L'esempio utilizza una sintassi di templating leggera che funziona in qualsiasi browser moderno, ma i concetti si applicano anche a Handlebars, Mustache o motori lato server. Alla fine del tutorial potrai copiare il codice nel tuo progetto e iniziare a associare i dati immediatamente.

## Cosa copre questo tutorial

* Come strutturare una fonte dati che contiene più persone  
* Come creare un modello di tabella riutilizzabile che si ripete per ogni voce  
* Come associare i dati e generare il markup HTML finale  
* Problemi comuni nella popolazione delle righe della tabella e come evitarli  

Non sono richieste librerie esterne, anche se lo stesso schema funziona con i framework di templating più popolari. L'unico prerequisito è una conoscenza di base di HTML e JavaScript.

## Prerequisiti

* Un browser moderno (Chrome, Edge, Firefox o Safari)  
* Un editor per file HTML/JavaScript  
* Facoltativo: un file JSON o un oggetto JavaScript che rappresenta la collezione di persone  

## Passo 1: Definire la fonte dati

Per prima cosa, crea un oggetto JavaScript che rispecchi la struttura usata nel modello. Ogni persona ha un nome, un cognome e un oggetto indirizzo.

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

**Perché è importante:** La gerarchia dell'oggetto (`Persons.Person`) corrisponde al ciclo `{{#foreach Persons.Person}}` nel modello, consentendo al motore di iterare automaticamente su ogni voce.

## Passo 2: Scrivere il modello della tabella con un blocco di ripetizione

Il modello qui sotto utilizza una sintassi in stile Mustache (`{{#foreach}}`) per ripetere il `<tr>` per ogni persona. Inserisci il modello all'interno di un tag `<script type="text/template">` così il browser lo ignorerà finché non lo elaborerai.

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

**Perché è importante:** La direttiva `{{#foreach Persons.Person}}` indica al motore di ripetere tutto ciò che si trova tra i tag di apertura e chiusura per ogni oggetto persona. All'interno della riga puoi fare riferimento a qualsiasi proprietà (`{{FirstName}}`, `{{LastName}}`, ecc.) per **popolare le righe della tabella** in modo dinamico.

## Passo 3: Implementare una piccola funzione di rendering

Poiché il tutorial deve essere autosufficiente, scriveremo un renderer minimale che sostituisce i segnaposto in stile Mustache con i valori reali. La funzione attraversa l'oggetto dati, espande il blocco di ripetizione e inietta l'HTML finale nella pagina.

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

**Perché è importante:** Il renderer dimostra **come generare markup di una tabella** programmaticamente senza includere una libreria completa. Inoltre chiarisce la trasformazione dal modello all'HTML finale, aiutandoti a adattare il codice ad altri motori di templating in seguito.

## Passo 4: Aggiungere un segnaposto dove apparirà la tabella generata

Crea un `<div>` vuoto che lo script riempirà dopo il rendering.

```html
<div id="output"></div>
```

Quando la pagina si carica, lo script sostituisce il contenuto di questo `<div>` con la tabella completamente popolata.

## Passo 5: Verificare il risultato

Apri il file HTML in un browser. Dovresti vedere una tabella che elenca il nome completo e l'indirizzo di ogni persona:

| Persona         | Indirizzo                       |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Se aggiungi altri oggetti all'array `data.Persons.Person`, la tabella cresce automaticamente—soddisfacendo il requisito di **popolare le righe della tabella**.

## Consiglio esperto: gestire collezioni vuote

Quando l'array dei dati è vuoto, il renderer attualmente genera solo l'intestazione della tabella. Per offrire un'esperienza utente più chiara, aggiungi una guardia:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Questa piccola modifica impedisce la visualizzazione di una tabella vuota e fornisce un feedback immediato all'utente.

## Variazioni comuni e casi limite

| Situazione                              | Adeguamento                                                                 |
|----------------------------------------|-----------------------------------------------------------------------------|
| Utilizzo di un motore lato server (es. Handlebars) | Sostituire il `renderTemplate` personalizzato con `Handlebars.compile` e passare lo stesso oggetto dati. |
| Necessità di ordinare le righe alfabeticamente | Ordinare `data.Persons.Person` prima di chiamare `renderTemplate`. |
| Aggiunta di una colonna per il numero di telefono | Estendere il `<tr>` con `<td>{{Phone}}</td>` e includere `Phone` in ogni oggetto persona. |
| Set di dati di grandi dimensioni (centinaia di righe) | Renderizzare le righe a blocchi o utilizzare lo scrolling virtuale per mantenere l'interfaccia reattiva. |

## Esempio completo funzionante

Di seguito trovi il file HTML completo che puoi copiare‑incollare in `index.html`. Contiene tutti gli elementi discussi sopra.

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

**Output previsto**

La pagina rende una tabella con due righe, ciascuna mostra il nome completo e l'indirizzo formattato di una persona. Aggiungendo altri oggetti all'array `Person` vengono aggiunte automaticamente nuove righe—dimostrando **come generare elementi di tabella** a partire dai dati.

## Conclusione

Ora sai **come associare dati** a una **tabella HTML dinamica**, generare righe per ogni record e visualizzare i valori di nome e cognome accanto all'indirizzo.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiungere CSS – CSS inline ai documenti HTML in Aspose.HTML per Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Come modificare l'albero del documento HTML in Aspose.HTML per Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Come abilitare JavaScript in Aspose HTML – Caricare HTML e ottenere testo](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}