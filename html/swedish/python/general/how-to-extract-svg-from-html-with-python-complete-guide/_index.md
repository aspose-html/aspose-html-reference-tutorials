---
category: general
date: 2026-05-31
description: Lär dig hur du extraherar SVG från HTML med Python. Denna steg‑för‑steg‑handledning
  visar hur du läser HTML‑dokument, sparar SVG‑filer och sparar inline‑SVG effektivt.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: sv
og_description: Hur man extraherar SVG från HTML med Python. Följ den här handledningen
  för att läsa HTML-dokument, spara SVG-filer och hantera inbäddad SVG utan ansträngning.
og_title: Hur man extraherar SVG från HTML med Python – Komplett guide
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
title: Hur man extraherar SVG från HTML med Python – Komplett guide
url: /sv/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man extraherar SVG från HTML med Python – Komplett guide

Har du någonsin undrat **how to extract SVG** från en rörig HTML‑sida utan att rycka ur håret? Du är inte ensam. Oavsett om du bygger en web‑scraper, en design‑pipeline, eller bara behöver batch‑exportera ikoner, så är kunskapen **how to extract SVG** ett praktiskt knep som sparar tid och huvudvärk.

I den här handledningen visar vi dig exakt **how to extract SVG** med Aspose.HTML‑biblioteket för Python. Vi läser HTML‑dokumentet, hämtar både inline `<svg>`‑markup **och** externa SVG‑referenser, och sedan **save SVG files** till disk — allt i ett snyggt, återanvändbart skript. När du är klar har du en färdig lösning som du kan anpassa till dina egna projekt.

> **Pro tip:** Om du bara vill ha en snabb sniff av sidan fungerar `BeautifulSoup` också, men Aspose.HTML ger dig ett komplett DOM, vilket gör extraheringen av både inline‑ och länkade SVG‑filer till en barnlek.

## Vad du behöver

* Python 3.8+ (koden använder f‑strings, så 3.6+ är det absoluta minimumet)
* `pip install aspose-html` – det kommersiella biblioteket som driver vår HTML‑parsing
* En mapp med en `input.html`‑fil som innehåller de SVG‑filer du vill hämta
* Skrivbehörighet till utmatningskatalogen (vi kallar den `YOUR_DIRECTORY`)

Det är allt—inga extra binärer, inga headless‑webbläsare. Enkelt, eller?

## Steg 1: Läs HTML‑dokument med Aspose.HTML

Det första du måste göra är att **read HTML document** så att du kan gå igenom dess DOM‑träd. Aspose.HTML ger dig ett `HTMLDocument`‑objekt som beter sig som en webbläsares `document`.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Varför detta är viktigt:* Genom att ladda HTML i ett korrekt DOM undviker du fallgroparna med regex‑baserad parsning, och du får metoder som `get_elements_by_tag_name` och `query_selector_all` gratis.

## Steg 2: Samla alla inline <svg>-element

Inline‑SVG är de `<svg>…</svg>`‑block som sitter direkt i HTML‑koden. För att **save inline SVG** behöver vi bara deras yttre HTML.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Observera att vi lägger till den råa markupen direkt i `svg_contents`. Senare kommer vi att avgöra om varje post är markup eller en filsökväg.

## Steg 3: Hitta externa SVG‑referenser (img‑ och object‑taggar)

Många sidor länkar till externa SVG‑filer via `<img src="icon.svg">` eller `<object data="logo.svg">`. För att **extract SVG from HTML** måste vi också fånga dessa URL:er.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Edge case alert:* Om SVG‑URL:en är relativ vill du slå ihop den med basvägen för HTML‑filen. För korthetens skull antar vi att HTML‑filen ligger bredvid SVG‑filerna.

## Steg 4: Skriv varje SVG till en separat fil

Nu när vi har en blandad lista av markup‑strängar och filsökvägar, itererar vi och **save SVG files**. Skriptet skiljer automatiskt mellan inline‑markup och en referens till en befintlig fil.

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

**Vad du kommer att se:** När skriptet är klart kommer `YOUR_DIRECTORY` att innehålla filer med namn `svg_0.svg`, `svg_1.svg`, … där varje fil innehåller antingen den ursprungliga inline‑markupen eller en kopia av den externa SVG‑filen.

### Förväntad output

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Om en refererad fil saknas skriver skriptet ut en varning men fortsätter—så en trasig länk stoppar inte hela extraktionen.

## Hantera vanliga fallgropar

| Problem | Why it Happens | Quick Fix |
|---------|----------------|-----------|
| **Relativa URL:er går sönder** | `src`‑attributet kan vara `"../assets/icon.svg"` | Använd `os.path.join(os.path.dirname(html_path), src)` för att lösa. |
| **Duplicerade filnamn** | Två SVG‑filer med samma namn skrivs över | Inkludera en hash av innehållet i filnamnet (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **Stora inline‑SVG:er orsakar minnesökningar** | Att lagra all markup i en lista innan skrivning | Strömma varje element direkt till en fil istället för att buffra. |
| **Icke‑SVG‑bilder smiter igenom** | Vissa `<img>`‑taggar slutar med `.svg?version=1` | Ta bort frågesträngar innan filändelsekontrollen (`src.split('?')[0]`). |

## Fullt skript du kan kopiera‑och‑klistra

Nedan är det kompletta, färdiga programmet. Spara det som `extract_svg.py`, justera `YOUR_DIRECTORY`, och kör `python extract_svg.py`.

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

## Sammanfattning – Hur man extraherar SVG i ett nötskal

* **Read HTML document** med `HTMLDocument`.
* **Gather inline `<svg>`** via `get_elements_by_tag_name`.
* **Locate external SVGs** med en CSS‑selector som slutar på `.svg`.
* **Save each piece**—skriv markup direkt till en fil eller kopiera den refererade filen.
* **Handle edge cases** som relativa sökvägar, dubbletter och saknade filer.

Det är hela svaret på **how to extract SVG** från en HTML‑sida, inbäddat i ett enda, lätt‑att‑modifiera skript.

## Vad blir nästa?

Nu när du kan **extract SVG** på ett pålitligt sätt, överväg dessa uppföljningsidéer:

* **Batch processing:** Loopa igenom en katalog med HTML‑filer för att bygga ett ikonbibliotek.
* **Optimization:** Kör varje sparad SVG genom SVGO (en Node.js‑optimerare) för att minska filstorleken.
* **Conversion:** Använd `cairosvg` eller `svglib` för att omvandla SVG‑filerna till PNG för äldre webbläsare.
* **Metadata extraction:** Pars `<title>`‑ eller `<desc>`‑taggar i varje SVG för sökbara etiketter.

Var och en av dessa ämnen berör våra sekundära nyckelord—**read HTML document**, **save svg files**, **save inline svg**, **extract svg from html**—så du hittar massor av material att utforska.

---

*Happy hacking! Om du stöter på problem, lämna en kommentar nedan eller ping mig på GitHub. SVG‑världen är enorm, men med rätt verktyg är extraheringen ett enkelt stycke tårta.*

## Vad bör du lära dig härnäst?

- [Spara SVG-dokument i Aspose.HTML för Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Hur man konverterar SVG till XPS med Aspose.HTML för Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendera ett SVG-dokument i PNG-format i .NET med Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}