---
category: general
date: 2026-09-07
description: Wie man Daten in einer dynamischen HTML‑Tabelle bindet – lerne, wie man
  Tabellenzeilen generiert und die Felder für Vor‑ und Nachname effizient füllt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: de
lastmod: 2026-09-07
og_description: Wie man Daten in einer dynamischen HTML‑Tabelle bindet. Dieses Tutorial
  zeigt, wie man Tabellenzeilen erzeugt, Vor‑ und Nachnamen anzeigt und Tabellenzeilen
  mit JavaScript füllt.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Wie man Daten an eine dynamische HTML‑Tabelle bindet – Schritt‑für‑Schritt‑Anleitung
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
title: Wie man Daten an eine dynamische HTML‑Tabelle mit Vor‑ und Nachnamen‑Spalten
  bindet
url: /de/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Daten an eine dynamische HTML‑Tabelle mit Vor‑ und Nachnamen‑Spalten bindet

Wenn Sie **Daten binden** in eine Tabelle, die mit jedem Datensatz wächst, zeigt Ihnen dieser Leitfaden eine vollständige Lösung. Sie sehen, wie man eine dynamische HTML‑Tabelle erzeugt, Tabellenzeilen füllt und den Vor‑ und Nachnamen jeder Person anzeigt, ohne wiederholtes Markup zu schreiben.

Das Beispiel verwendet eine leichtgewichtige Templating‑Syntax, die in jedem modernen Browser funktioniert, aber die Konzepte gelten gleichermaßen für Handlebars, Mustache oder serverseitige Engines. Am Ende des Tutorials können Sie den Code in Ihr Projekt kopieren und sofort Daten binden.

## Was dieses Tutorial behandelt

* Wie man eine Datenquelle strukturiert, die mehrere Personen enthält  
* Wie man ein wiederverwendbares Tabellenvorlage erstellt, das für jeden Eintrag wiederholt wird  
* Wie man die Daten bindet und das endgültige HTML‑Markup generiert  
* Häufige Fallstricke beim Befüllen von Tabellenzeilen und wie man sie vermeidet  

Keine externen Bibliotheken sind erforderlich, obwohl dasselbe Muster mit beliebten Templating‑Frameworks funktioniert. Die einzige Voraussetzung ist Grundkenntnis in HTML und JavaScript.

## Voraussetzungen

* Ein moderner Browser (Chrome, Edge, Firefox oder Safari)  
* Ein Editor für HTML/JavaScript‑Dateien  
* Optional: eine JSON‑Datei oder ein JavaScript‑Objekt, das die Personensammlung repräsentiert  

## Schritt 1: Datenquelle definieren

Zuerst erstellen Sie ein JavaScript‑Objekt, das die im Template verwendete Struktur widerspiegelt. Jede Person hat einen Vornamen, Nachnamen und ein Adress‑Objekt.

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

**Warum das wichtig ist:** Die Objekt‑Hierarchie (`Persons.Person`) entspricht der `{{#foreach Persons.Person}}`‑Schleife im Template und ermöglicht es der Engine, automatisch über jeden Eintrag zu iterieren.

## Schritt 2: Tabellenvorlage mit Wiederholungsblock schreiben

Das nachstehende Template verwendet eine einfache Mustache‑ähnliche Syntax (`{{#foreach}}`), um das `<tr>` für jede Person zu wiederholen. Platzieren Sie das Template innerhalb eines `<script type="text/template">`‑Tags, damit der Browser es ignoriert, bis Sie es verarbeiten.

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

**Warum das wichtig ist:** Die Anweisung `{{#foreach Persons.Person}}` weist die Engine an, alles zwischen den öffnenden und schließenden Tags für jedes Personen‑Objekt zu wiederholen. Innerhalb der Zeile können Sie jede Eigenschaft (`{{FirstName}}`, `{{LastName}}` usw.) referenzieren, um **Tabellenzeilen** dynamisch zu füllen.

## Schritt 3: Kleine Rendering‑Funktion implementieren

Da das Tutorial eigenständig sein muss, schreiben wir einen minimalen Renderer, der die Mustache‑ähnlichen Platzhalter durch echte Werte ersetzt. Die Funktion durchläuft das Datenobjekt, erweitert den Wiederholungsblock und fügt das endgültige HTML in die Seite ein.

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

**Warum das wichtig ist:** Der Renderer zeigt **wie man Tabellen‑Markup** programmgesteuert erzeugt, ohne eine komplette Bibliothek einzubinden. Er verdeutlicht zudem die Transformation vom Template zum finalen HTML, was Ihnen später hilft, den Code an andere Templating‑Engines anzupassen.

## Schritt 4: Platzhalter hinzufügen, an dem die generierte Tabelle erscheint

Erstellen Sie ein leeres `<div>`, das das Skript nach dem Rendern füllt.

```html
<div id="output"></div>
```

Wenn die Seite geladen wird, ersetzt das Skript den Inhalt dieses `<div>` durch die vollständig gefüllte Tabelle.

## Schritt 5: Ergebnis überprüfen

Öffnen Sie die HTML‑Datei in einem Browser. Sie sollten eine Tabelle sehen, die den vollständigen Namen und die Adresse jeder Person auflistet:

| Person          | Adresse                         |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Wenn Sie weitere Objekte zum Array `data.Persons.Person` hinzufügen, wächst die Tabelle automatisch – was die Anforderung **Tabellenzeilen füllen** erfüllt.

## Profi‑Tipp: Umgang mit leeren Sammlungen

Wenn das Daten‑Array leer ist, gibt der Renderer derzeit einen leeren Tabellenkopf aus. Um ein klareres Benutzererlebnis zu bieten, fügen Sie eine Prüfung hinzu:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Diese kleine Änderung verhindert, dass eine leere Tabelle angezeigt wird, und gibt den Benutzern sofortiges Feedback.

## Häufige Variationen und Sonderfälle

| Situation                               | Anpassung                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| Verwendung einer server‑seitigen Engine (z. B. Handlebars) | Ersetzen Sie das benutzerdefinierte `renderTemplate` durch `Handlebars.compile` und übergeben Sie dasselbe Datenobjekt. |
| Notwendigkeit, Zeilen alphabetisch zu sortieren       | Sortieren Sie `data.Persons.Person` bevor Sie `renderTemplate` aufrufen.               |
| Hinzufügen einer Spalte für Telefonnummer       | Erweitern Sie das `<tr>` um `<td>{{Phone}}</td>` und fügen Sie `Phone` in jedes Personen‑Objekt ein. |
| Große Datensätze (Hunderte von Zeilen)     | Rendern Sie Zeilen in Portionen oder verwenden Sie virtuelles Scrollen, um die UI reaktionsfähig zu halten. |

## Vollständiges funktionierendes Beispiel

Unten finden Sie die vollständige HTML‑Datei, die Sie in `index.html` kopieren‑und‑einfügen können. Sie enthält alle oben besprochenen Bestandteile.

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

**Erwartete Ausgabe**

Die Seite rendert eine Tabelle mit zwei Zeilen, die jeweils den vollständigen Namen und die formatierte Adresse einer Person anzeigen. Das Hinzufügen weiterer Objekte zum `Person`‑Array fügt automatisch neue Zeilen hinzu – was **wie man Tabellen‑Elemente** aus Daten generiert, demonstriert.

## Fazit

Sie wissen jetzt **wie man Daten** an eine **dynamische HTML‑Tabelle** bindet, Zeilen für jeden Datensatz erzeugt und Vor‑ und Nachnamenwerte zusammen mit der Adresse anzeigt.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man CSS hinzufügt – Inline‑CSS zu HTML‑Dokumenten in Aspose.HTML für Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Wie man den HTML‑Dokumentbaum in Aspose.HTML für Java bearbeitet](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Wie man JavaScript in Aspose HTML aktiviert – HTML laden & Text extrahieren](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}