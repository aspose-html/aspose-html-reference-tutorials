---
category: general
date: 2026-08-25
description: Lernen Sie, wie man ein HTML‑Dokument erstellt, ein CSS‑Element auswählt,
  HTML‑Text ändert und eine HTML‑Datei mit einem einfachen Python‑Skript speichert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: de
lastmod: 2026-08-25
og_description: Erstelle ein HTML‑Dokument, wähle ein CSS‑Element aus, modifiziere
  den HTML‑Text und speichere die HTML‑Datei in wenigen Zeilen Python. Folge diesem
  vollständigen Tutorial.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Erstelle ein HTML‑Dokument und bearbeite dessen Inhalt mit Python – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: Wie man ein HTML-Dokument erstellt und dessen Inhalt in Python bearbeitet
url: /de/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein HTML-Dokument erstellt und dessen Inhalt in Python bearbeitet

Wenn Sie ein **create html document** von Grund auf neu erstellen und seine Elemente programmgesteuert ändern müssen, zeigt Ihnen diese Anleitung genau, wie das geht. Sie sehen ein kurzes, ausführbares Skript, das eine Datei erstellt, einen Absatz mit einem CSS-Selektor auswählt, den Text aktualisiert und das Ergebnis wieder auf die Festplatte schreibt.

Die Arbeit mit HTML in Python ist üblich beim Erstellen von Berichten, E‑Mail‑Vorlagen oder statischen Webseiteninhalten. Am Ende dieses Tutorials können Sie **select element css**, **modify html text** und **save html file** ausführen, ohne Ihre IDE zu verlassen.

## Voraussetzungen

* Python 3.9 oder neuer installiert.
* Die Pakete `beautifulsoup4` und `lxml` (Installation mit `pip install beautifulsoup4 lxml`).
* Schreibberechtigung für das Verzeichnis, in dem Sie die Ausgabedatei speichern möchten.

Keine zusätzlichen Werkzeuge sind erforderlich; die Standardbibliothek übernimmt die Datei‑Ein‑/Ausgabe.

## Schritt 1: Installieren der benötigten Bibliotheken

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` bietet eine praktische API zum Parsen und Manipulieren von HTML, während `lxml` einen schnellen Parser liefert, der CSS‑Selektoren versteht.

## Schritt 2: Erstellen des initialen HTML-Dokuments

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

Der `BeautifulSoup`‑Konstruktor erstellt ein **create html document**‑Objekt im Speicher. Die Verwendung des `"lxml"`‑Parsers stellt vollständige CSS‑Selektor‑Unterstützung sicher.

## Schritt 3: Auswählen des Absatz‑Elements mit einem CSS-Selektor

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

Die Methode `select_one` implementiert die **select element css**‑Logik und gibt das erste passende Tag zurück. Wenn der Selektor nichts findet, ist `para` `None`, daher ist in Produktionscode eine defensive Prüfung ratsam.

## Schritt 4: Ändern des Textinhalts des Absatzes

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

Das Zuweisen zu `para.string` führt eine **modify html text**‑Operation aus. BeautifulSoup aktualisiert den zugrunde liegenden DOM‑Baum, sodass die Änderung beim Serialisieren des Dokuments sichtbar wird.

## Schritt 5: Speichern des aktualisierten HTML in einer Datei

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

Der Aufruf von `open` zusammen mit `write` implementiert die **save html file**‑Funktionalität. Durch die Verwendung von `prettify()` entsteht eine schön eingerückte Ausgabe, die beim Debuggen hilfreich ist.

### Vollständiges Skript für schnelles Kopieren‑Einfügen

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

Das Ausführen von `python edit_html.py` erzeugt `updated.html` mit folgendem Inhalt:

```html
<p>
 New
</p>
```

## Häufige Variationen und Sonderfälle

### Auswählen mehrerer Elemente

Wenn Sie **select element css**‑Selektoren benötigen, die mehrere Tags treffen (z. B. `"div.note"`), verwenden Sie `doc.select("div.note")`, das eine Liste zurückgibt. Iterieren Sie über die Liste, um Änderungen auf jedes Element anzuwenden.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### Vorhandene Attribute beibehalten

Wenn Sie den Text ersetzen, behält BeautifulSoup alle Attribute des Tags bei. Zum Beispiel:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### Fehlende Elemente elegant behandeln

In Produktionsskripten stoßen Sie häufig auf fehlerhaftes HTML. Wickeln Sie die Auswahl in eine Bedingung oder einen try‑except‑Block, wie in Schritt 4 gezeigt, um Abstürze zu vermeiden.

### Schreiben in ein bestimmtes Verzeichnis

Ersetzen Sie `output_path` durch einen absoluten oder relativen Pfad:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

Stellen Sie sicher, dass das Verzeichnis existiert; andernfalls wirft Python `FileNotFoundError`.

## Pro‑Tipps

* **Performance** – Bei großen HTML‑Dateien bevorzugen Sie `lxml.etree` direkt; BeautifulSoup fügt eine dünne Abstraktionsschicht hinzu, die praktisch, aber etwas langsamer ist.
* **Encoding** – Öffnen Sie Dateien immer mit `encoding="utf-8"`, um Nicht‑ASCII‑Zeichen zu erhalten.
* **Testing** – Nach der Modifikation können Sie die Ausgabe mit `assert "New" in open(output_path).read()` in einem Unit‑Test überprüfen.

## Fazit

Sie wissen jetzt, wie man **create html document** erstellt, eine **select element css**‑Abfrage verwendet, um einen Knoten zu finden, **modify html text** durchführt und schließlich **save html file** mit Python speichert. Dieses Muster lässt sich auf komplexere Transformationen wie Massen‑Updates, Attributänderungen oder die Generierung von Vorlagen ausweiten.

Als Nächstes erkunden Sie verwandte Themen wie **how to edit html** mit XPath‑Ausdrücken, das Erzeugen vollständiger HTML‑Seiten mit Jinja2 oder die Automatisierung der Stapelverarbeitung mehrerer Dateien. Jeder dieser Punkte baut auf den hier gezeigten Kernschritten auf und erweitert Ihr Werkzeugset für die programmgesteuerte HTML‑Manipulation.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [HTML-Dokument mit Aspose.HTML erstellen – Schritt‑für‑Schritt‑Anleitung](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [Wie man den HTML‑Dokumentbaum in Aspose.HTML für Java bearbeitet](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [HTML‑Dokument in Aspose.HTML für Java speichern](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}