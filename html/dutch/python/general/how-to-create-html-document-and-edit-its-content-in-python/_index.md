---
category: general
date: 2026-08-25
description: Leer hoe je een HTML-document maakt, een CSS-element selecteert, HTML-tekst
  wijzigt en een HTML-bestand opslaat met een eenvoudig Python‑script.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: nl
lastmod: 2026-08-25
og_description: Maak een HTML-document, selecteer een CSS‑element, wijzig de HTML‑tekst
  en sla het HTML‑bestand op in een paar regels Python. Volg deze volledige tutorial.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Maak een HTML-document en bewerk de inhoud met Python – stapsgewijze handleiding
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
title: Hoe maak je een HTML-document en bewerk je de inhoud ervan in Python
url: /nl/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een html-document te maken en de inhoud ervan te bewerken in Python

Als je een **create html document** vanaf nul moet maken en de elementen programmatisch wilt wijzigen, laat deze gids je precies zien hoe. Je ziet een kort, uitvoerbaar script dat een bestand maakt, een alinea selecteert met een CSS‑selector, de tekst bijwerkt en het resultaat terug naar de schijf schrijft.

Werken met HTML in Python is gebruikelijk bij het genereren van rapporten, e‑mailtemplates of statische site‑inhoud. Aan het einde van deze tutorial kun je **select element css**, **modify html text** en **save html file** uitvoeren zonder je IDE te verlaten.

## Vereisten

* Python 3.9 of nieuwer geïnstalleerd.
* De `beautifulsoup4`- en `lxml`-pakketten (installeren met `pip install beautifulsoup4 lxml`).
* Schrijfrechten voor de map waarin je het uitvoerbestand wilt opslaan.

Er zijn geen extra tools nodig; de standaardbibliotheek behandelt bestands‑I/O.

## Stap 1: Installeer de vereiste bibliotheken

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` biedt een handige API voor het parseren en manipuleren van HTML, terwijl `lxml` een snelle parser levert die CSS‑selectors begrijpt.

## Stap 2: Maak het initiële HTML‑document

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

De `BeautifulSoup`‑constructor bouwt een **create html document**‑object in het geheugen. Het gebruik van de `"lxml"`‑parser zorgt voor volledige CSS‑selectorondersteuning.

## Stap 3: Selecteer het alinea‑element met een CSS‑selector

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

De `select_one`‑methode implementeert **select element css**‑logica en retourneert de eerste overeenkomende tag. Als de selector niets vindt, is `para` `None`, dus een defensieve controle is aan te raden in productiecodel.

## Stap 4: Wijzig de tekstinhoud van de alinea

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

Toewijzen aan `para.string` voert een **modify html text**‑bewerking uit. BeautifulSoup werkt de onderliggende DOM‑boom bij, zodat de wijziging zichtbaar is wanneer het document wordt geserialiseerd.

## Stap 5: Sla de bijgewerkte HTML op in een bestand

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

De `open`‑aanroep in combinatie met `write` implementeert **save html file**‑functionaliteit. Het gebruik van `prettify()` levert mooi ingesprongen output op, wat handig is bij het debuggen.

### Volledig script voor snel kopiëren‑plakken

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

Het uitvoeren van `python edit_html.py` maakt `updated.html` aan met:

```html
<p>
 New
</p>
```

## Veelvoorkomende variaties en randgevallen

### Meerdere elementen selecteren

Als je **select element css**‑selectors nodig hebt die meerdere tags matchen (bijv. `"div.note"`), gebruik dan `doc.select("div.note")` dat een lijst retourneert. Iterate over de lijst om wijzigingen op elk element toe te passen.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### Bestaande attributen behouden

Wanneer je de tekst vervangt, behoudt BeautifulSoup alle attributen op de tag. Bijvoorbeeld:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### Ontbrekende elementen elegant afhandelen

In productiescripts kom je vaak mal gevormde HTML tegen. Plaats de selectie in een voorwaarde of try‑except‑blok, zoals getoond in Stap 4, om crashes te voorkomen.

### Schrijven naar een specifieke map

Vervang `output_path` door een absoluut of relatief pad:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

Zorg ervoor dat de map bestaat; anders zal Python `FileNotFoundError` raise.

## Pro‑tips

* **Performance** – Voor grote HTML‑bestanden, geef de voorkeur aan `lxml.etree` direct; BeautifulSoup voegt een dunne abstractielaag toe die handig is maar iets trager.
* **Encoding** – Open altijd bestanden met `encoding="utf-8"` om niet‑ASCII‑tekens te behouden.
* **Testing** – Na wijziging kun je de output verifiëren met `assert "New" in open(output_path).read()` in een unit‑test.

## Conclusie

Je weet nu hoe je een **create html document** maakt, een **select element css**‑query gebruikt om een knoop te vinden, **modify html text** uitvoert, en uiteindelijk **save html file** met Python. Dit patroon schaalt naar complexere transformaties zoals bulk‑updates, attribuutwijzigingen of sjabloongeneratie.

Verken vervolgens gerelateerde onderwerpen zoals **how to edit html** met XPath‑expressies, volledige HTML‑pagina's genereren met Jinja2, of batchverwerking van meerdere bestanden automatiseren. Elk van deze bouwt voort op de kernstappen die hier worden getoond en breidt je gereedschapskist uit voor programmatische HTML‑manipulatie.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}