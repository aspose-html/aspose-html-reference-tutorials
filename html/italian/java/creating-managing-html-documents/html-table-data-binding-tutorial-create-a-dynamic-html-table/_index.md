---
category: general
date: 2026-08-12
description: Impara il binding dei dati di una tabella HTML in pochi minuti. Questa
  guida mostra come unire i dati, iterare attraverso la collezione e visualizzare
  il nome in una tabella HTML dinamica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- html table data binding
- how to merge data
- loop through collection
- show first name
- dynamic html table
language: it
lastmod: 2026-08-12
og_description: Il binding dei dati di una tabella HTML ti consente di unire i dati
  e di iterare attraverso la collezione per mostrare il nome e gli altri campi. Segui
  questa guida completa per creare una tabella HTML dinamica.
og_image_alt: Screenshot of a dynamic HTML table created with html table data binding
og_title: Associazione dei dati di una tabella HTML – costruisci una tabella HTML
  dinamica passo passo
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Learn html table data binding in minutes. This guide shows how to merge
    data, loop through collection, and show first name in a dynamic HTML table.
  headline: html table data binding tutorial – create a dynamic HTML table
  type: TechArticle
- description: Learn html table data binding in minutes. This guide shows how to merge
    data, loop through collection, and show first name in a dynamic HTML table.
  name: html table data binding tutorial – create a dynamic HTML table
  steps:
  - name: Sample JSON payload
    text: '```json { "Persons": { "Person": [ { "FirstName": "Alice", "LastName":
      "Smith", "Address": { "Street": "Maple Ave", "Number": "12", "City": "Springfield"
      } }, { "FirstName": "Bob", "LastName": "Johnson", "Address": { "Street": "Oak
      Street", "Number": "45B", "City": "Rivertown" } } ] } } ```'
  - name: Empty collections
    text: 'If the `Person` array is empty, the table will render only the header row.
      To display a friendly message, add a conditional block after the header:'
  - name: Escaping special characters
    text: When names or addresses contain characters like `<` or `&`, most templating
      engines escape them automatically. If your engine does not, wrap the values
      with an escape helper, e.g., `{{escape FirstName}}`.
  - name: Custom styling
    text: 'You can add CSS classes to the table for better visual presentation without
      affecting the data binding logic:'
  type: HowTo
- questions:
  - answer: Yes. Libraries like Handlebars.js or Mustache.js run in the browser and
      respect the same `{{#foreach}}` syntax. Load the library, compile the template,
      and pass the JSON object to render the table.
    question: Can I use this approach with plain JavaScript instead of a server‑side
      engine?
  - answer: Fetch the data with `fetch()` or `axios`, then call the template’s render
      function inside the promise’s `.then()` handler. The table updates once the
      data arrives.
    question: What if my data source is an API that returns data asynchronously?
  - answer: 'Pagination is a separate concern. Render only the slice of the collection
      you want to show, then re‑render the table when the user navigates to another
      page. ## Conclusion You now have a complete guide to **html table data binding**
      that shows **how to merge data**, **loop through collection**, and '
    question: Does this method support pagination?
  type: FAQPage
tags:
- HTML
- data-binding
- templating
title: Tutorial di binding dei dati in una tabella HTML – crea una tabella HTML dinamica
url: /it/java/creating-managing-html-documents/html-table-data-binding-tutorial-create-a-dynamic-html-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html table data binding – guida completa di programmazione

Se hai bisogno di **html table data binding** per trasformare un elenco JSON in una tabella HTML live, questa guida ti mostra esattamente come farlo. Imparerai a unire i dati, iterare una collezione e **show first name** insieme ad altri campi senza scrivere markup ripetitivo.

Le tabelle dinamiche sono comuni nei dashboard, nei pannelli di amministrazione e negli strumenti di reporting. Alla fine di questo tutorial potrai generare una **dynamic html table** da qualsiasi collezione di oggetti, usando solo una semplice sintassi di templating.

## Prerequisiti

- Conoscenza di base di HTML.
- Un motore di templating che supporti i loop `{{#foreach}}` (ad es., Handlebars, Mustache o un motore personalizzato lato server).
- Un payload JSON che contenga un array `Persons.Person` con i campi `FirstName`, `LastName` e un oggetto `Address`.

## Panoramica della soluzione

Ci occuperemo di:

1. **Create a table** che riceverà i dati uniti.
2. **Define the header row** una volta.
3. **Loop through the collection** e renderizza una riga per ogni persona.
4. **Show first name**, cognome e campi dell'indirizzo all'interno della stessa tabella.

Il markup finale è una **dynamic html table** completamente funzionale che si aggiorna automaticamente quando i dati sottostanti cambiano.

![html table data binding example](/images/html-table-data-binding.png "html table data binding example")

## Passo 1: Configura lo scheletro della tabella HTML (html table data binding)

L'elemento `<table>` esterno riceve i dati uniti tramite l'attributo `data_merge`. L'attributo indica al motore di templating di ripetere le righe all'interno della tabella per ogni elemento della collezione.

```html
<table border="1" data_merge="{{#foreach Persons.Person}}">
    <!-- Header row and data rows will be inserted here -->
</table>
```

*Perché è importante*: Collegando l'attributo `data_merge` all'elemento `<table>`, eviti di duplicare il markup `<tr>` per ogni persona. Il motore unisce i dati automaticamente, che è il fulcro di **html table data binding**.

## Passo 2: Aggiungi una riga di intestazione statica (dynamic html table)

Le intestazioni sono statiche—appaiono una sola volta indipendentemente dal numero di record presenti. Posizionale direttamente all'interno della tabella prima che il loop renderizzi le righe.

```html
<tr>
    <th>Person</th>
    <th>Address</th>
</tr>
```

La riga di intestazione definisce i titoli delle colonne per la **dynamic html table**. Tenerla fuori dal loop garantisce che non venga ripetuta per ogni record.

## Passo 3: Renderizza una riga per ogni persona (loop through collection)

All'interno dello stesso elemento `<table>`, aggiungi una riga che utilizza i segnaposto del templating. Il motore ripeterà questo `<tr>` per ogni voce in `Persons.Person`.

```html
<tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
</tr>
```

*Key points*:

- `{{FirstName}}` e `{{LastName}}` estraggono i valori **show first name** e cognome dall'elemento corrente.
- `{{Address.Street}}`, `{{Address.Number}}` e `{{Address.City}}` mostrano come accedere a oggetti nidificati.
- Poiché la riga è all'interno del blocco `{{#foreach}}` definito sul `<table>`, il motore di templating **how to merge data** automaticamente.

## Esempio completo funzionante

Di seguito trovi lo snippet HTML completo che puoi incollare in qualsiasi pagina che supporti la stessa sintassi di templating.

```html
<table border="1" data_merge="{{#foreach Persons.Person}}">
    <!-- Header row – appears once -->
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>

    <!-- Data row – repeated for each person -->
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
```

### Esempio di payload JSON

```json
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Smith",
        "Address": {
          "Street": "Maple Ave",
          "Number": "12",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Johnson",
        "Address": {
          "Street": "Oak Street",
          "Number": "45B",
          "City": "Rivertown"
        }
      }
    ]
  }
}
```

Quando il motore di template elabora l'HTML con il JSON sopra, l'output renderizzato appare così:

| Person          | Address                         |
|-----------------|---------------------------------|
| Alice Smith     | Maple Ave 12, Springfield       |
| Bob Johnson     | Oak Street 45B, Rivertown       |

*Perché funziona*: Il motore legge `data_merge="{{#foreach Persons.Person}}"`, itera su ogni oggetto nell'array `Person` e sostituisce i segnaposto con i valori corrispondenti. Questa è l'essenza di **html table data binding** combinata con **how to merge data**.

## Passo 4: Gestione dei casi limite (advanced html table data binding)

### Collezioni vuote

Se l'array `Person` è vuoto, la tabella renderizzerà solo la riga di intestazione. Per mostrare un messaggio amichevole, aggiungi un blocco condizionale dopo l'intestazione:

```html
{{#if Persons.Person.length}}
    <!-- rows are generated automatically -->
{{else}}
    <tr>
        <td colspan="2">No records found.</td>
    </tr>
{{/if}}
```

### Escape dei caratteri speciali

Quando nomi o indirizzi contengono caratteri come `<` o `&`, la maggior parte dei motori di templating li escape automaticamente. Se il tuo motore non lo fa, avvolgi i valori con un helper di escape, ad es., `{{escape FirstName}}`.

### Stile personalizzato

Puoi aggiungere classi CSS alla tabella per una migliore presentazione visiva senza influire sulla logica di data binding:

```html
<table class="responsive-table" border="1" data_merge="{{#foreach Persons.Person}}">
    ...
</table>
```

## Suggerimento professionale: Riutilizzare la stessa tabella per più collezioni

Se devi visualizzare sia `Employees` che `Customers` in tabelle separate nella stessa pagina, assegna a ciascuna tabella il proprio attributo `data_merge`:

```html
<table data_merge="{{#foreach Employees.Employee}}">
    <!-- employee rows -->
</table>

<table data_merge="{{#foreach Customers.Customer}}">
    <!-- customer rows -->
</table>
```

Questo dimostra la flessibilità di **html table data binding** per qualsiasi collezione.

## Domande frequenti

**Q: Posso usare questo approccio con JavaScript puro invece di un motore lato server?**  
A: Sì. Librerie come Handlebars.js o Mustache.js funzionano nel browser e rispettano la stessa sintassi `{{#foreach}}`. Carica la libreria, compila il template e passa l'oggetto JSON per renderizzare la tabella.

**Q: E se la mia fonte dati è un'API che restituisce dati in modo asincrono?**  
A: Recupera i dati con `fetch()` o `axios`, poi chiama la funzione di render del template all'interno del gestore `.then()` della promise. La tabella si aggiorna non appena i dati arrivano.

**Q: Questo metodo supporta la paginazione?**  
A: La paginazione è una questione separata. Renderizza solo la porzione della collezione che desideri mostrare, poi ri‑renderizza la tabella quando l'utente naviga a un'altra pagina.

## Conclusione

Ora hai una guida completa al **html table data binding** che mostra **how to merge data**, **loop through collection** e **show first name** insieme ad altri campi in una **dynamic html table**. Collegando un attributo `data_merge` all'elemento `<table>` e usando semplici segnaposto, elimini markup ripetitivo e mantieni la tua UI sincronizzata con i dati sottostanti.

Successivamente, considera di esplorare:

- Styling della **dynamic html table** con CSS Grid o Flexbox.
- Paginazione e ordinamento lato client usando librerie come DataTables.
- Aggiornamenti in tempo reale con WebSockets o Server‑Sent Events.

Sentiti libero di adattare il pattern ad altre strutture dati, sperimentare colonne aggiuntive o integrare la tabella in una più ampia applicazione single‑page. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Unire HTML con Json in .NET con Aspose.HTML](/html/english/net/html-document-manipulation/merge-html-with-json/)
- [Unire HTML con XML in .NET con Aspose.HTML](/html/english/net/html-document-manipulation/merge-html-with-xml/)
- [Come modificare l'albero del documento HTML in Aspose.HTML per Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}