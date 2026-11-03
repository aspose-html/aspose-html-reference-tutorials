---
category: general
date: 2026-05-31
description: Leer hoe je een element op id kunt ophalen, de achtergrondkleur in HTML
  kunt wijzigen, HTML‑tekst kunt lezen en een HTML‑attribuut kunt instellen met Python.
  Stapsgewijze tutorial.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: nl
og_description: Haal een element op basis van id, lees HTML‑tekst, stel een HTML‑attribuut
  in en wijzig de achtergrondkleur van HTML met Python in een enkele, gemakkelijk
  te volgen gids.
og_title: Element ophalen op id in Python – Volledige HTML‑manipulatie tutorial
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
title: Element ophalen op id in Python – Complete gids voor HTML-manipulatie
url: /nl/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get element by id in Python – Complete gids voor HTML-manipulatie

Heb je ooit **get element by id** nodig gehad van een HTML‑pagina terwijl je een snel Python‑script schreef? Je bent niet de enige—de meeste ontwikkelaars lopen tegen datzelfde obstakel aan wanneer ze sites gaan crawlen of lokale rapporten aanpassen. Het goede nieuws? Met een handvol code kun je de tekst van het element lezen, de achtergrondkleur wijzigen, en zelfs nieuwe attributen instellen, alles zonder je editor te verlaten.

In deze tutorial lopen we een real‑world voorbeeld door: een lokaal `sample.html` laden, het element met ID `main‑content` ophalen, de binnenste tekst afdrukken, en uiteindelijk de achtergrondkleur wijzigen naar lichtgrijs. Aan het einde weet je ook **how to read HTML text**, **how to set HTML attribute**, en waarom **manipulate HTML with Python** een handige vaardigheid is in elke automatiseringstoolbox.

## Wat je nodig hebt

- **Python 3.9+** (elke recente versie werkt)
- De **`lxml`** bibliotheek (of **BeautifulSoup** als je dat liever hebt) – we gebruiken `lxml.html` omdat het een schone `get_element_by_id`‑style API biedt.
- Een klein HTML‑bestand genaamd `sample.html` in een map genaamd `YOUR_DIRECTORY`. Voel je vrij om de onderstaande snippet naar dat bestand te kopiëren:

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

## Stap 1: Installeer de vereiste bibliotheek

Als je `lxml` nog niet geïnstalleerd hebt, open een terminal en voer uit:

```bash
pip install lxml
```

*Pro tip:* Het gebruik van een virtuele omgeving houdt je globale Python‑installatie netjes, vooral wanneer je met meerdere projecten werkt.

## Stap 2: Laad het HTML‑document

Nu lezen we het bestand in een `lxml.html` documentobject. Zie dit als het omzetten van ruwe tekst naar een doorzoekbare boom.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

Het uitvoeren hiervan print “Document loaded successfully.” Als het bestand niet gevonden kan worden, zal Python een `FileNotFoundError` raise—het is goed om dit vroeg te vangen voordat je een spookelement achterna zit.

## Stap 3: Get element by id

Hier is de kern van de zaak. `lxml` biedt ons een handige `get_element_by_id`‑methode die de DOM‑API die je in JavaScript zou gebruiken, weerspiegelt.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

Wanneer het element bestaat, zie je “Element found!” in de console geprint. Dit is de **get element by id** stap die de meeste van onze latere manipulaties aandrijft.

## Stap 4: How to read HTML text

Zodra je het element hebt, is het extraheren van de zichtbare tekst een fluitje van een cent. De `text_content()` methode retourneert alles binnenin, zonder tags.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Expected output:

```
Inner text: Hello, world! This is the original text.
```

Je vraagt je misschien af, *wat als het element geneste tags bevat?* `text_content()` werkt nog steeds—het concateneert alle afstammende tekstknooppunten, waardoor je een schone string krijgt die je kunt loggen, opslaan, of gebruiken in een ander algoritme.

## Stap 5: How to set HTML attribute

Het wijzigen of toevoegen van attributen is even eenvoudig. De `set` methode laat je elk attribuutnaam toewijzen die je wilt.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Output:

```
New attribute value: true
```

Die regel toont **how to set HTML attribute** on the fly. Je kunt `"data-modified"` vervangen door `"class"`, `"title"` of een ander attribuut dat het element ondersteunt.

## Stap 6: Change background colour HTML

Nu de visuele aanpassing. Om de achtergrondkleur te wijzigen, injecteren we een `style` attribuut dat de standaard overschrijft.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

Na het uitvoeren van het script zal de `div` in `sample.html` er zo uitzien wanneer je het in een browser opent:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

Dat is de **change background colour html** techniek die je voor elk element kunt hergebruiken—vervang gewoon de kleurcode.

## Stap 7: Manipulate HTML with Python – Alles samenvoegen

Hieronder staat het volledige, uitvoerbare script dat elke stap combineert. Sla het op als `modify_html.py` en voer het uit vanuit dezelfde map als je `YOUR_DIRECTORY` map.

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

### Wat het script doet, regel voor regel

1. **Imports** `lxml.html` voor het parsen en `pathlib` voor OS‑onafhankelijke paden.  
2. **Loads** `sample.html` en stopt met een duidelijke foutmelding als het bestand ontbreekt.  
3. **Retrieves** het element met behulp van **get element by id**.  
4. **Prints** de tekst van het element—wat **how to read HTML text** toont.  
5. **Adds** een aangepast attribuut, wat **how to set HTML attribute** illustreert.  
6. **Changes** de achtergrondkleur, waarmee aan de **change background colour html** vereiste wordt voldaan.  
7. **Writes** de bijgewerkte markup naar `sample_modified.html`, zodat je het in een browser kunt openen en de wijzigingen kunt zien.

Het uitvoeren van het script geeft console‑output die lijkt op:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Open `sample_modified.html` en je zult de grijze achtergrond achter de tekst zien—bewijs dat **manipulate HTML with python** echt werkt.

## Veelvoorkomende valkuilen & hoe ze te vermijden

- **Missing ID** – Als het doel‑element niet bestaat, retourneert `get_element_by_id` `None`. Controleer altijd op `None` voordat je eigenschappen benadert; anders krijg je een `AttributeError`.  
- **Encoding issues** – Bij het lezen van niet‑ASCII pagina's, geef `encoding='utf-8'` door aan `html.parse` of zorg dat je bestand in UTF‑8 is opgeslagen.  
- **Overwriting existing styles** – Het instellen van het `style` attribuut vervangt eerdere inline‑stijlen. Als je bestaande regels wilt behouden, lees dan eerst de huidige `style`‑waarde, voeg je nieuwe regel toe, en schrijf het terug.  
- **File permissions** – Terugschrijven naar dezelfde map kan mislukken op alleen‑lezen systemen. Kies een schrijfbare output‑pad, zoals we deden met `sample_modified.html`.

## Voorbeeld uitbreiden

Now that you’ve mastered the basics, consider these next steps:

- **Loop over multiple IDs** – Gebruik een lijst van ID's en itereren met een `for`‑lus om secties van een pagina in batches te verwerken.  
- **Replace text content** – Roep `elem.text = "New text"` aan om de zichtbare string te wijzigen.  
- **Add child elements** – Use `

## Wat moet je hierna leren?

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}