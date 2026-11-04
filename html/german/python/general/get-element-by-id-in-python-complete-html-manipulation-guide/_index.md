---
category: general
date: 2026-05-31
description: Lernen Sie, wie Sie ein Element per ID abrufen, die Hintergrundfarbe
  in HTML ändern, HTML‑Text auslesen und HTML‑Attribute mit Python setzen. Schritt‑für‑Schritt‑Tutorial.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: de
og_description: Element per ID abrufen, HTML‑Text auslesen, HTML‑Attribut setzen und
  Hintergrundfarbe mit Python ändern – in einer einzigen, leicht verständlichen Anleitung.
og_title: Element per ID in Python abrufen – Vollständiges HTML-Manipulations‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: Element per ID in Python abrufen – Vollständiger Leitfaden zur HTML-Manipulation
url: /de/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get element by id in Python – Complete HTML Manipulation Guide

Haben Sie schon einmal **get element by id** aus einer HTML‑Seite benötigen müssen, während Sie ein schnelles Python‑Skript geschrieben haben? Sie sind nicht allein – die meisten Entwickler stoßen genau auf dieses Problem, wenn sie beginnen, Websites zu crawlen oder lokale Berichte zu bearbeiten. Die gute Nachricht? Mit ein paar Zeilen Code können Sie den Text des Elements auslesen, seine Hintergrundfarbe ändern und sogar neue Attribute setzen, und das alles ohne Ihren Editor zu verlassen.

In diesem Tutorial gehen wir ein praxisnahes Beispiel durch: Wir laden ein lokales `sample.html`, holen das Element mit der ID `main‑content`, geben dessen inneren Text aus und tauschen schließlich die Hintergrundfarbe gegen ein helles Grau aus. Am Ende wissen Sie außerdem **how to read HTML text**, **how to set HTML attribute** und warum **manipulate HTML with Python** eine nützliche Fähigkeit in jedem Automatisierungs‑Toolbox ist.

## What You’ll Need

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- **Python 3.9+** (jede aktuelle Version funktioniert)
- Die **`lxml`**‑Bibliothek (oder **BeautifulSoup**, falls Sie das bevorzugen) – wir verwenden `lxml.html`, weil sie eine saubere `get_element_by_id`‑artige API bietet.
- Eine kleine HTML‑Datei namens `sample.html` in einem Ordner namens `YOUR_DIRECTORY`. Fühlen Sie sich frei, das Snippet unten in diese Datei zu kopieren:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

Das war’s – keine ausgefallenen Frameworks, nur reines Python und eine statische HTML‑Datei.

## Step 1: Install the Required Library

Falls Sie `lxml` noch nicht installiert haben, öffnen Sie ein Terminal und führen Sie aus:

```bash
pip install lxml
```

*Profi‑Tipp:* Die Verwendung einer virtuellen Umgebung hält Ihr globales Python sauber, besonders wenn Sie mehrere Projekte jonglieren.

## Step 2: Load the HTML Document

Jetzt lesen wir die Datei in ein `lxml.html`‑Dokumentobjekt ein. Denken Sie daran wie das Umwandeln des Rohtexts in einen navigierbaren Baum.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

Beim Ausführen wird “Document loaded successfully.” ausgegeben. Wenn die Datei nicht gefunden wird, wirft Python einen `FileNotFoundError` – gut, das frühzeitig abzufangen, bevor Sie einem Phantom‑Element nachjagen.

## Step 3: Get element by id

Hier kommt das Kernstück. `lxml` stellt uns die praktische Methode `get_element_by_id` zur Verfügung, die der DOM‑API aus JavaScript entspricht.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

Existiert das Element, sehen Sie “Element found!” in der Konsole. Das ist der **get element by id**‑Schritt, der den Großteil unserer späteren Manipulationen antreibt.

## Step 4: How to read HTML text

Sobald Sie das Element haben, ist das Extrahieren des sichtbaren Textes ein Kinderspiel. Die Methode `text_content()` liefert alles innerhalb des Elements, ohne Tags.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Erwartete Ausgabe:

```
Inner text: Hello, world! This is the original text.
```

Vielleicht fragen Sie sich, *was, wenn das Element verschachtelte Tags enthält?* `text_content()` funktioniert weiterhin – es verkettet alle Nachkommen‑Textknoten und gibt Ihnen einen sauberen String, den Sie protokollieren, speichern oder in einen anderen Algorithmus einspeisen können.

## Step 5: How to set HTML attribute

Attribute zu ändern oder hinzuzufügen ist genauso unkompliziert. Die Methode `set` lässt Sie jeden gewünschten Attributnamen zuweisen.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Ausgabe:

```
New attribute value: true
```

Diese Zeile demonstriert **how to set HTML attribute** on the fly. Sie können `"data-modified"` durch `"class"`, `"title"` oder ein anderes vom Element unterstütztes Attribut ersetzen.

## Step 6: Change background colour HTML

Jetzt zum visuellen Feinschliff. Um die Hintergrundfarbe zu ändern, fügen wir ein `style`‑Attribut ein, das die Vorgabe überschreibt.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

Nach dem Ausführen des Skripts sieht das `div` in `sample.html` beim Öffnen im Browser folgendermaßen aus:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

Das ist die **change background colour html**‑Technik, die Sie für jedes Element wiederverwenden können – einfach den Farbcode austauschen.

## Step 7: Manipulate HTML with Python – Putting It All Together

Unten finden Sie das vollständige, ausführbare Skript, das alle Schritte kombiniert. Speichern Sie es als `modify_html.py` und führen Sie es im selben Verzeichnis wie Ihren `YOUR_DIRECTORY`‑Ordner aus.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### What the script does, line by line

1. **Imports** `lxml.html` zum Parsen und `pathlib` für OS‑unabhängige Pfade.  
2. **Loads** `sample.html` und bricht mit einer klaren Fehlermeldung ab, falls die Datei fehlt.  
3. **Retrieves** das Element mittels **get element by id**.  
4. **Prints** den Text des Elements – zeigt **how to read HTML text**.  
5. **Adds** ein benutzerdefiniertes Attribut, veranschaulicht **how to set HTML attribute**.  
6. **Changes** die Hintergrundfarbe und erfüllt damit die Anforderung **change background colour html**.  
7. **Writes** das aktualisierte Markup nach `sample_modified.html`, sodass Sie es im Browser öffnen und die Änderungen sehen können.

Beim Ausführen des Skripts erhalten Sie eine Konsolenausgabe ähnlich dieser:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Öffnen Sie `sample_modified.html` und Sie werden den grauen Hintergrund hinter dem Text bemerken – ein Beweis dafür, dass **manipulate HTML with python** wirklich funktioniert.

## Common Pitfalls & How to Avoid

- **Missing ID** – Existiert das Ziel‑Element nicht, gibt `get_element_by_id` `None` zurück. Prüfen Sie immer auf `None`, bevor Sie Eigenschaften zugreifen; sonst erhalten Sie einen `AttributeError`.  
- **Encoding issues** – Beim Lesen von Nicht‑ASCII‑Seiten übergeben Sie `encoding='utf-8'` an `html.parse` oder stellen Sie sicher, dass Ihre Datei in UTF‑8 gespeichert ist.  
- **Overwriting existing styles** – Das Setzen des `style`‑Attributs überschreibt vorhandene Inline‑Styles. Wenn Sie bestehende Regeln erhalten wollen, lesen Sie zuerst den aktuellen `style`‑Wert, hängen Ihre neue Regel an und schreiben ihn zurück.  
- **File permissions** – Das Schreiben zurück in denselben Ordner kann auf schreibgeschützten Systemen fehlschlagen. Wählen Sie einen beschreibbaren Ausgabepfad, wie wir es mit `sample_modified.html` getan haben.

## Extending the Example

Jetzt, wo Sie die Grundlagen beherrschen, denken Sie an folgende nächste Schritte:

- **Loop over multiple IDs** – Verwenden Sie eine Liste von IDs und iterieren Sie mit einer `for`‑Schleife, um mehrere Abschnitte einer Seite zu verarbeiten.  
- **Replace text content** – Rufen Sie `elem.text = "New text"` auf, um den sichtbaren String zu ändern.  
- **Add child elements** – Verwenden Sie `

## What Should You Learn Next?

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}