---
category: general
date: 2026-10-12
description: Erfahren Sie, wie Sie eine Tabelle aus Daten generieren und die Tabelle
  mit JSON mithilfe von Handlebars befüllen. Schritt‑für‑Schritt‑Anleitung zum Wiederholen
  von Tabellenzeilen in dynamischen HTML‑Tabellen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: de
lastmod: 2026-10-12
og_description: Erstelle eine Tabelle aus Daten und fülle die Tabelle aus JSON mit
  Handlebars. Folge diesem Tutorial, um dynamische HTML-Tabellen mit wiederholten
  Tabellenzeilen zu erstellen.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Tabelle aus Daten mit Handlebars generieren – vollständige Anleitung
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
title: Wie man mit HTML und Handlebars eine Tabelle aus Daten erzeugt
url: /de/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man eine Tabelle aus Daten mit HTML und Handlebars erzeugt

Wenn Sie **eine Tabelle aus Daten erzeugen** müssen, zeigt Ihnen dieses Tutorial genau, wie es geht. Mit einer einfachen Handlebars‑Schleife können Sie **eine Tabelle aus JSON befüllen**, **Tabellenzeilen wiederholen** und erhalten eine vollständig **dynamische HTML‑Tabelle**, die sich aktualisiert, sobald sich die Quelle ändert.

In den nächsten Minuten sehen Sie ein vollständiges, ausführbares Beispiel, verstehen, warum jedes Teil wichtig ist, und lernen, wie Sie das Muster für komplexere Szenarien wie bedingte Spalten oder verschachtelte Objekte anpassen.

## Was Sie erstellen werden

Wir erstellen eine HTML‑Tabelle, die:

* Ein JSON‑Payload liest, das eine Liste von Personen enthält.
* Eine Tabellenzeile für jede Person wiederholt (`repeat table rows`).
* Den Vornamen, Nachnamen und die Adresse jeder Person in die entsprechenden Zellen einfügt.
* Ohne serverseitiges Rendering funktioniert – der gesamte Prozess läuft im Browser.

**Voraussetzungen**

* Grundkenntnisse in HTML und JavaScript.
* Ein moderner Browser (Chrome, Edge, Firefox oder Safari).
* Handlebars.js – wir laden es von einem CDN, sodass keine Build‑Tools erforderlich sind.

---

## Schritt 1: JSON‑Datenquelle vorbereiten

Der erste Schritt besteht darin, ein JavaScript‑Objekt zu definieren, das das JSON nachahmt, das Sie von einer API erhalten würden. Handlebars arbeitet mit einfachen Objekten, sodass Sie die Daten für Demonstrationszwecke direkt in einem `<script>`‑Tag einbetten können.

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

**Warum das wichtig ist** – Durch das Halten der Daten in einem separaten `<script>`‑Element können Sie sie später leicht durch einen echten AJAX‑Aufruf ersetzen. Die Struktur (`Persons.Person`) entspricht dem Pfad, der im Handlebars‑Block `{{#foreach Persons.Person}}` verwendet wird, was für das **populate table from JSON** entscheidend ist.

---

## Schritt 2: Handlebars‑Template schreiben, das Zeilen wiederholt

Erstellen Sie als Nächstes einen `<script type="text/x-handlebars-template">`‑Block, der das Tabellen‑Markup enthält. Handlebars ersetzt die Platzhalter durch tatsächliche Werte und wiederholt das `<tr>` für jede Person.

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

**Erklärung der wichtigsten Teile**

* `{{#foreach Persons.Person}}` weist Handlebars an, **Tabellenzeilen zu wiederholen** für jeden Eintrag im Array `Persons.Person`.
* Die Ausdrücke `{{FirstName}} {{LastName}}` und `{{Address.*}}` holen Werte aus dem aktuellen Array‑Element.
* Das Einbetten der gesamten Tabelle in ein `data_merge`‑Attribut ist optional; es kann für nachgelagerte Verarbeitung oder CSS‑Selektoren nützlich sein.

---

## Schritt 3: Handlebars laden und das Template kompilieren

Wir holen Handlebars von einem CDN, parsen das JSON, kompilieren das Template und fügen das endgültige HTML in die Seite ein.

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

**Warum zur Laufzeit kompilieren?** – Das einmalige Kompilieren des Templates und dessen Wiederverwendung hält die Seite schnell, besonders wenn sich die Daten häufig ändern. Dieses Muster macht es zudem trivial, **populate table from JSON** mehrfach auszuführen, ohne die Seite neu zu laden.

---

## Schritt 4: Einen Container für die erzeugte Tabelle reservieren

Fügen Sie ein Platzhalter‑`<div>` hinzu, an dem die dynamische Tabelle erscheinen soll. Das hält das Markup sauber und trennt die Verantwortlichkeiten zwischen statischem Layout und generiertem Inhalt.

```html
<div id="output"></div>
```

Wenn das Skript aus Schritt 3 ausgeführt wird, enthält das `<div id="output">` ein vollständig aufgebautes `<table>`‑Element, bereit für Styling oder weitere Manipulation.

---

## Schritt 5: Ausgabe überprüfen und die Tabelle stylen (optional)

Öffnen Sie die Seite in einem Browser und Sie sollten eine Tabelle wie die unten gezeigte sehen:

![Screenshot, der die aus Daten erzeugte Tabelle zeigt](image.png "Screenshot, der die aus Daten erzeugte Tabelle zeigt")

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

**Optionales Styling** – Wenn Sie ein saubereres Aussehen wünschen, fügen Sie ein paar CSS‑Regeln hinzu:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Umgang mit Randfällen und gängigen Variationen

### 1. Leere Datensätze

Wenn das JSON‑Array leer ist, rendert Handlebars weiterhin die Kopfzeile, aber keine Datenzeilen. Um eine freundliche Meldung anzuzeigen, umschließen Sie die Tabelle mit einem bedingten Block:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Verschachtelte Schleifen (z. B. mehrere Adressen pro Person)

Wenn eine Person mehrere Adressen haben kann, können Sie ein weiteres `{{#foreach}}` innerhalb der Zeile verschachteln:

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

### 3. Verwendung einer echten API

Ersetzen Sie das statische `<script id="people-data">` durch einen fetch‑Aufruf:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Dies demonstriert dieselbe **dynamic table rows**‑Technik, während Live‑Daten abgerufen werden.

### 4. Barrierefreiheits‑Überlegungen

* Fügen Sie `<th>`‑Elementen `scope="col"` hinzu.
* Verwenden Sie `<caption>`, um den Zweck der Tabelle zu beschreiben.
* Stellen Sie ausreichenden Farbkontrast sicher, wenn Sie benutzerdefiniertes CSS anwenden.

---

## Vollständiges, ausführbares Beispiel

Kopieren Sie den folgenden Block in eine `index.html`‑Datei und öffnen Sie sie in einem Browser. Die Seite wird **eine Tabelle aus Daten erzeugen**, **die Tabelle aus JSON befüllen** und Zeilen automatisch wiederholen.

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

**Erwartetes Ergebnis**

Eine zweizeilige Tabelle (plus Kopfzeile), die „Alice Anderson“ und „Bob Baker“ mit ihren jeweiligen Adressen zeigt. Die Seite funktioniert offline und beweist, dass Sie **eine Tabelle aus Daten erzeugen** können, ohne einen Server‑Komponente.

---

## Fazit

Sie wissen jetzt, wie Sie **eine Tabelle aus Daten** mit einem Handlebars‑Template **erzeugen**, **die Tabelle aus JSON befüllen** und **Tabellenzeilen wiederholen**, die eine **dynamische HTML‑Tabelle** bilden. Das Muster skaliert auf größere Datensätze, verschachtelte Strukturen und Live‑API‑Aufrufe und bietet Ihnen eine robuste Grundlage für jedes clientseitige Reporting oder Admin‑UI.

**Nächste Schritte**

* Erkunden Sie Handlebars‑Helper zum Formatieren von Daten oder Zahlen.
* Kombinieren Sie diesen Ansatz mit CSS‑Grid oder Flexbox für responsive Tabellendesigns.
* Integrieren Sie Paginierungs‑ oder Sortierbibliotheken, um sehr große Datensätze zu handhaben.

Fühlen Sie sich frei, mit verschiedenen JSON‑Strukturen zu experimentieren, bedingte Spalten hinzuzufügen oder Handlebars durch ein anderes Templating‑Engine zu ersetzen – Ihre neuen Fähigkeiten ermöglichen es Ihnen, flexible, datengetriebene Oberflächen schnell und zuverlässig zu erstellen.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [HTML-Dokument mit Java erstellen – JSON abrufen und Inhalt generieren](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Datenverarbeitung und Stream‑Management in Aspose.HTML für Java](/html/english/java/data-handling-stream-management/)
- [HTML in Java laden – Schritt‑für‑Schritt‑Anleitung](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}