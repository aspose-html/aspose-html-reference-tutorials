---
category: general
date: 2026-05-31
description: Tanulja meg, hogyan lehet SVG‑t kinyerni HTML‑ből Python segítségével.
  Ez a lépésről‑lépésre útmutató bemutatja, hogyan olvassuk be a HTML‑dokumentumot,
  hogyan mentsük el az SVG‑fájlokat, és hogyan menthetjük hatékonyan a beágyazott
  SVG‑t.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: hu
og_description: Hogyan nyerjünk ki SVG-t HTML‑ből Python használatával. Kövesd ezt
  az útmutatót, hogy beolvass egy HTML‑dokumentumot, elmentsd az SVG‑fájlokat, és
  könnyedén kezeld a beágyazott SVG‑ket.
og_title: Hogyan lehet SVG-t kinyerni HTML-ből Python segítségével – Teljes útmutató
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
title: Hogyan lehet SVG-t kinyerni HTML-ből Python segítségével – Teljes útmutató
url: /hu/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan lehet SVG-t kinyerni HTML-ből Python‑nal – Teljes útmutató

Gondolkodtál már azon, **hogyan lehet SVG-t kinyerni** egy kusza HTML‑oldalról anélkül, hogy a hajadba ragadnál? Nem vagy egyedül. Akár web‑scrapert, akár egy design‑pipeline‑t építesz, vagy csak tömegesen kell exportálnod ikonokat, a **SVG kinyerése** egy hasznos trükk, ami időt és fejfájást spórol.

Ebben a tutorialban pontosan megmutatjuk, **hogyan lehet SVG-t kinyerni** az Aspose.HTML könyvtár segítségével Python‑ban. Beolvassuk a HTML‑dokumentumot, kinyerjük mind az inline `<svg>` markup‑ot, **mind** a külső SVG hivatkozásokat, majd **SVG fájlokként** mentjük őket a lemezre – mindezt egy rendezett, újrahasználható szkriptben. A végére egy kész, futtatható megoldásod lesz, amit saját projektjeidhez is testre szabhatsz.

> **Pro tip:** Ha csak egy gyors pillantást szeretnél a lapra, a `BeautifulSoup` is működik, de az Aspose.HTML egy teljes DOM‑ot ad, ami megkönnyíti az inline és a linked SVG‑k kinyerését.

## Amire szükséged lesz

Mielőtt belevágnánk, ellenőrizd, hogy rendelkezel-e:

* Python 3.8+ (a kód f‑stringeket használ, így a 3.6+ a minimum)
* `pip install aspose-html` – a kereskedelmi könyvtár, ami a HTML‑parszolást biztosítja
* Egy mappa, benne egy `input.html` fájllal, amely a kinyerni kívánt SVG‑ket tartalmazza
* Írási jogosultság a kimeneti könyvtárhoz (ezt `YOUR_DIRECTORY`‑nek hívjuk)

Ennyi – nincs extra bináris, nincs headless böngésző. Egyszerű, ugye?

## 1. lépés: HTML‑dokumentum beolvasása Aspose.HTML‑lel

Az első dolog, amit meg kell tenned, **a HTML‑dokumentum beolvasása**, hogy bejárhasd a DOM‑fáját. Az Aspose.HTML egy `HTMLDocument` objektumot ad, ami úgy viselkedik, mint egy böngésző `document`.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Miért fontos:* A HTML megfelelő DOM‑ba töltésével elkerülöd a regex‑alapú parsing buktatóit, és ingyen megkapod a `get_elements_by_tag_name` és `query_selector_all` metódusokat.

## 2. lépés: Az összes inline <svg> elem összegyűjtése

Az inline SVG-k azok a `<svg>…</svg>` blokkok, amelyek közvetlenül a HTML‑ben helyezkednek el. Az **inline SVG mentéséhez** csak a külső HTML‑re van szükségünk.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Vedd észre, hogy a nyers markup‑ot közvetlenül a `svg_contents` listába fűzzük. Később eldöntjük, hogy egy bejegyzés markup vagy fájlútvonal.

## 3. lépés: Külső SVG hivatkozások megtalálása (img és object tagek)

Sok oldal külső SVG fájlokra hivatkozik `<img src="icon.svg">` vagy `<object data="logo.svg">` segítségével. Az **SVG kinyeréséhez HTML‑ből** ezeket az URL‑eket is el kell kapnunk.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Edge case alert:* Ha az SVG URL relatív, akkor a HTML fájl alapútvonalával kell összefűzni. A rövidség kedvéért feltételezzük, hogy a HTML a SVG fájlok mellett helyezkedik el.

## 4. lépés: Minden SVG mentése külön fájlba

Most, hogy kevert listánk van markup‑stringekkel és fájlútvonalakkal, végigiterálunk, és **SVG fájlokat mentünk**. A szkript automatikusan megkülönbözteti az inline markup‑ot a meglévő fájlra mutató hivatkozástól.

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

**Mit fogsz látni:** A szkript befejezése után a `YOUR_DIRECTORY` tartalmazni fog `svg_0.svg`, `svg_1.svg`, … fájlokat, amelyek vagy az eredeti inline markup‑ot, vagy a külső SVG másolatát tárolják.

### Várható kimenet

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Ha egy hivatkozott fájl hiányzik, a szkript figyelmeztetést ír ki, de folytatja – így egy törött link sem állítja meg a teljes kinyerést.

## Gyakori buktatók kezelése

| Probléma | Miért fordul elő | Gyors megoldás |
|----------|------------------|----------------|
| **Relatív URL‑k hibát okoznak** | A `src` attribútum lehet `"../assets/icon.svg"` | Használd az `os.path.join(os.path.dirname(html_path), src)`‑t a feloldáshoz. |
| **Duplikált fájlnevek** | Két SVG ugyanazzal a névvel felülírja egymást | Tedd a hash‑t a fájlnévbe (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **Nagy inline SVG‑k memóriacsúcsot okoznak** | Az összes markup egy listában tárolódik írás előtt | Streameld közvetlenül a fájlba, ne buffereld. |
| **Nem‑SVG képek is átcsúsznak** | Egyes `<img>` tagek `.svg?version=1`‑vel végződnek | Távolítsd el a query stringet a kiterjesztés ellenőrzése előtt (`src.split('?')[0]`). |

## Teljes szkript, amit másolhatsz‑beilleszthetsz

Az alábbiakban a kész, futtatható program teljes kódja található. Mentsd `extract_svg.py`‑ként, állítsd be a `YOUR_DIRECTORY`‑t, és futtasd `python extract_svg.py`‑val.

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

## Összefoglalás – Hogyan lehet SVG-t kinyerni egy pillantásra

* **HTML‑dokumentum beolvasása** `HTMLDocument`‑dal.
* **Inline `<svg>` gyűjtése** `get_elements_by_tag_name`‑el.
* **Külső SVG‑k megtalálása** egy `.svg`‑re végződő CSS‑selectorral.
* **Minden darab mentése** – markup közvetlenül fájlba, vagy a hivatkozott fájl másolása.
* **Edge case‑ek kezelése**: relatív útvonalak, duplikátumok, hiányzó fájlok.

Ez a teljes válasz arra, **hogyan lehet SVG-t kinyerni** egy HTML‑oldalról, egyetlen, könnyen módosítható szkriptben összefoglalva.

## Mi a következő lépés?

Most, hogy megbízhatóan **kivonod az SVG‑ket**, gondolkodhatsz ezeken a további ötleteken:

* **Batch feldolgozás:** Egy könyvtár HTML‑fájljaiban iterálva építs ikonkönyvtárat.
* **Optimalizálás:** Futtasd a mentett SVG‑ket az SVGO‑val (Node.js optimalizáló) a méret csökkentéséhez.
* **Konvertálás:** Használd a `cairosvg` vagy `svglib` könyvtárakat, hogy az SVG‑ket PNG‑vé alakítsd régi böngészőknek.
* **Metaadat kinyerés:** Parseld a `<title>` vagy `<desc>` tageket minden SVG‑ben kereshető címkékhez.

Ezek a témák mind a másodlagos kulcsszavainkat érintik – **read HTML document**, **save svg files**, **save inline svg**, **extract svg from html** – így bőven találsz anyagot a további felfedezéshez.

---

*Boldog hackelést! Ha elakadsz, írj egy megjegyzést lent, vagy pingeld fel a GitHub‑on. Az SVG világa hatalmas, de a megfelelő eszközökkel a kinyerés egy szelet torta.*


## Mit érdemes legközelebb megtanulni?

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendre un document SVG au format PNG dans .NET avec Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}