---
category: general
date: 2026-05-31
description: Leer hoe je SVG uit HTML kunt extraheren met Python. Deze stapsgewijze
  tutorial laat zien hoe je een HTML‑document leest, SVG‑bestanden opslaat en inline
  SVG efficiënt opslaat.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: nl
og_description: Hoe je SVG uit HTML kunt extraheren met Python. Volg deze tutorial
  om een HTML-document te lezen, SVG‑bestanden op te slaan en inline SVG moeiteloos
  te verwerken.
og_title: Hoe SVG uit HTML te extraheren met Python – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Hoe SVG uit HTML te extraheren met Python – Complete gids
url: /nl/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe SVG uit HTML te extraheren met Python – Complete gids

Heb je je ooit afgevraagd **hoe je SVG kunt extraheren** uit een rommelige HTML-pagina zonder je haar uit te trekken? Je bent niet de enige. Of je nu een web‑scraper bouwt, een design‑pipeline, of gewoon iconen in batch wilt exporteren, weten **hoe je SVG kunt extraheren** is een handige truc die tijd en hoofdpijn bespaart.

In deze tutorial laten we je precies zien **hoe je SVG kunt extraheren** met de Aspose.HTML‑bibliotheek voor Python. We lezen het HTML‑document, halen zowel inline `<svg>`‑markup **als** externe SVG‑referenties eruit, en **slaan SVG‑bestanden** op schijf—alles in een nette, herbruikbare script. Aan het einde heb je een kant‑klaar oplossing die je kunt aanpassen aan je eigen projecten.

> **Pro tip:** Als je alleen snel een kijkje wilt nemen op de pagina, werkt `BeautifulSoup` ook, maar Aspose.HTML geeft je een volledige DOM, waardoor het extraheren van zowel inline als gekoppelde SVG's een fluitje van een cent is.

## Wat je nodig hebt

* Python 3.8+ (de code gebruikt f‑strings, dus 3.6+ is het absolute minimum)
* `pip install aspose-html` – de commerciële bibliotheek die onze HTML‑parsing aandrijft
* Een map met een `input.html`‑bestand dat de SVG's bevat die je wilt ophalen
* Schrijfrechten voor de output‑directory (we noemen deze `YOUR_DIRECTORY`)

Dat is alles—geen extra binaries, geen headless browsers. Simpel, toch?

## Stap 1: HTML‑document lezen met Aspose.HTML

Het eerste dat je moet doen is **HTML‑document lezen** zodat je door de DOM‑boom kunt lopen. Aspose.HTML geeft je een `HTMLDocument`‑object dat zich gedraagt als het `document` van een browser.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Waarom dit belangrijk is:* Door de HTML in een juiste DOM te laden, vermijd je de valkuilen van regex‑gebaseerde parsing, en krijg je gratis methoden zoals `get_elements_by_tag_name` en `query_selector_all`.

## Stap 2: Alle inline <svg>-elementen verzamelen

Inline SVG's zijn die `<svg>…</svg>`‑blokken die direct in de HTML staan. Om **inline SVG op te slaan** hebben we alleen hun outer HTML nodig.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Merk op dat we de ruwe markup direct toevoegen aan `svg_contents`. Later bepalen we of elk item markup of een bestandspad is.

## Stap 3: Externe SVG-referenties vinden (img‑ en object‑tags)

Veel pagina's linken naar externe SVG‑bestanden via `<img src="icon.svg">` of `<object data="logo.svg">`. Om **SVG uit HTML te extraheren** moeten we die URL's ook vastleggen.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Edge‑case waarschuwing:* Als de SVG‑URL relatief is, wil je deze combineren met het basispad van het HTML‑bestand. Voor de beknoptheid gaan we ervan uit dat de HTML naast de SVG‑bestanden staat.

## Stap 4: Elk SVG naar een apart bestand schrijven

Nu we een gemengde lijst hebben van markup‑strings en bestandspaden, itereren we en **slaan we SVG‑bestanden** op. Het script onderscheidt automatisch inline markup van een verwijzing naar een bestaand bestand.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**Wat je zult zien:** Nadat het script is voltooid, bevat `YOUR_DIRECTORY` bestanden genaamd `svg_0.svg`, `svg_1.svg`, … elk met ofwel de originele inline markup of een kopie van de externe SVG.

### Verwachte output

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Als een verwezen bestand ontbreekt, geeft het script een waarschuwing, maar gaat door—zodat één kapotte link de hele extractie niet stopt.

## Veelvoorkomende valkuilen behandelen

| Probleem | Waarom het gebeurt | Snelle oplossing |
|----------|-------------------|------------------|
| **Relatieve URL's breken** | Het `src`‑attribuut kan `"../assets/icon.svg"` zijn | Gebruik `os.path.join(os.path.dirname(html_path), src)` om op te lossen. |
| **Dubbele bestandsnamen** | Twee SVG's met dezelfde naam worden overschreven | Voeg een hash van de inhoud toe aan de bestandsnaam (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **Grote inline SVG's veroorzaken geheugenpieken** | Alle markup opslaan in een lijst voordat je schrijft | Stream elk element direct naar een bestand in plaats van te bufferen. |
| **Niet‑SVG afbeeldingen glippen erdoorheen** | Sommige `<img>`‑tags eindigen op `.svg?version=1` | Strip query strings before the extension check (`src.split('?')[0]`). |

## Volledig script dat je kunt kopiëren‑plakken

Hieronder staat het volledige, kant‑klaar programma. Sla het op als `extract_svg.py`, pas `YOUR_DIRECTORY` aan, en voer `python extract_svg.py` uit.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## Samenvatting – Hoe SVG te extraheren in één oogopslag

* **HTML‑document lezen** met `HTMLDocument`.
* **Inline `<svg>` verzamelen** via `get_elements_by_tag_name`.
* **Externe SVG's lokaliseren** met een CSS‑selector die eindigt op `.svg`.
* **Elk onderdeel opslaan**—schrijf markup direct naar een bestand of kopieer het verwezen bestand.
* **Edge‑cases afhandelen** zoals relatieve paden, duplicaten en ontbrekende bestanden.

Dat is het volledige antwoord op **hoe je SVG kunt extraheren** uit een HTML‑pagina, verpakt in één enkel, makkelijk‑aanpasbaar script.

## Wat is het volgende?

Nu je **SVG betrouwbaar kunt extraheren**, overweeg deze vervolgideeën:

* **Batch‑verwerking:** Loop over een map met HTML‑bestanden om een bibliotheek met iconen op te bouwen.
* **Optimalisatie:** Verwerk elke opgeslagen SVG met SVGO (een Node.js‑optimizer) om de bestandsgrootte te verkleinen.
* **Conversie:** Gebruik `cairosvg` of `svglib` om de SVG's om te zetten naar PNG's voor oudere browsers.
* **Metadata‑extractie:** Parse `<title>`‑ of `<desc>`‑tags binnen elke SVG voor doorzoekbare labels.

Elk van deze onderwerpen raakt aan onze secundaire zoekwoorden—**read HTML document**, **save svg files**, **save inline svg**, **extract svg from html**—dus je zult genoeg materiaal vinden om te verkennen.

---

*Happy hacking! Als je tegen problemen aanloopt, laat dan een reactie achter of ping me op GitHub. De wereld van SVG is enorm, maar met de juiste tools is het extraheren ervan een eitje.*

## Wat moet je hierna leren?

- [SVG-document opslaan in Aspose.HTML voor Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Hoe SVG naar XPS converteren met Aspose.HTML voor Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [SVG-document renderen als PNG in .NET met Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}