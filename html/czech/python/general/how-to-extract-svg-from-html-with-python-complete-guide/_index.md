---
category: general
date: 2026-05-31
description: Naučte se, jak extrahovat SVG z HTML pomocí Pythonu. Tento krok‑za‑krokem
  návod ukazuje, jak načíst HTML dokument, uložit SVG soubory a efektivně uložit vložené
  SVG.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: cs
og_description: Jak extrahovat SVG z HTML pomocí Pythonu. Sledujte tento tutoriál,
  abyste načetli HTML dokument, uložili SVG soubory a snadno pracovali s vloženým
  SVG.
og_title: Jak extrahovat SVG z HTML pomocí Pythonu – Kompletní průvodce
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
title: Jak extrahovat SVG z HTML pomocí Pythonu – Kompletní průvodce
url: /cs/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak extrahovat SVG z HTML pomocí Pythonu – Kompletní průvodce

Už jste se někdy zamysleli nad tím, **jak extrahovat SVG** z nepořádné HTML stránky, aniž byste si trhali vlasy? Nejste v tom sami. Ať už vytváříte web‑scraper, design‑pipeline, nebo jen potřebujete hromadně exportovat ikony, znalost **jak extrahovat SVG** je užitečný trik, který šetří čas i starosti.

V tomto tutoriálu vám ukážeme přesně **jak extrahovat SVG** pomocí knihovny Aspose.HTML pro Python. Načteme HTML dokument, vytáhneme jak inline `<svg>` značky **tak** externí odkazy na SVG, a poté **uložíme SVG soubory** na disk – vše v přehledném, znovupoužitelném skriptu. Na konci budete mít připravené řešení, které můžete přizpůsobit svým projektům.

> **Tip:** Pokud potřebujete jen rychlý náhled na stránku, `BeautifulSoup` také funguje, ale Aspose.HTML vám poskytne kompletní DOM, což usnadňuje extrakci jak inline, tak propojených SVG.

## Co budete potřebovat

* Python 3.8+ (kód používá f‑stringy, takže 3.6+ je absolutní minimum)
* `pip install aspose-html` – komerční knihovna, která pohání naše parsování HTML
* Složka s souborem `input.html`, který obsahuje SVG, jež chcete vytáhnout
* Oprávnění k zápisu do výstupního adresáře (nazveme ho `YOUR_DIRECTORY`)

To je vše – žádné extra binární soubory, žádné headless prohlížeče. Jednoduché, že?

## Krok 1: Načtení HTML dokumentu pomocí Aspose.HTML

První věc, kterou musíte udělat, je **načíst HTML dokument**, abyste mohli procházet jeho DOM strom. Aspose.HTML vám poskytne objekt `HTMLDocument`, který se chová jako `document` v prohlížeči.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Proč je to důležité:* Načtením HTML do správného DOM se vyhnete úskalím regex‑založeného parsování a získáte metody jako `get_elements_by_tag_name` a `query_selector_all` zdarma.

## Krok 2: Shromáždění všech inline <svg> elementů

Inline SVG jsou ty `<svg>…</svg>` bloky, které jsou přímo uvnitř HTML. Pro **uložení inline SVG** potřebujeme jen jejich vnější HTML.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Všimněte si, že přidáváme surový markup přímo do `svg_contents`. Později rozhodneme, zda je každý záznam markup nebo cesta k souboru.

## Krok 3: Najděte externí odkazy na SVG (tagy img a object)

Mnoho stránek odkazuje na externí SVG soubory pomocí `<img src="icon.svg">` nebo `<object data="logo.svg">`. Pro **extrahování SVG z HTML** musíme zachytit i tyto URL.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Upozornění na okrajový případ:* Pokud je SVG URL relativní, budete ji chtít spojit se základní cestou HTML souboru. Pro stručnost předpokládáme, že HTML soubor leží vedle SVG souborů.

## Krok 4: Zapište každý SVG do samostatného souboru

Nyní, když máme smíšený seznam řetězců s markupem a cestami k souborům, projdeme jej a **uložíme SVG soubory**. Skript automaticky rozliší mezi inline markupem a odkazem na existující soubor.

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

**Co uvidíte:** Po dokončení skriptu bude `YOUR_DIRECTORY` obsahovat soubory pojmenované `svg_0.svg`, `svg_1.svg`, …, z nichž každý bude obsahovat buď původní inline markup, nebo kopii externího SVG.

### Očekávaný výstup

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Pokud chybí odkazovaný soubor, skript vypíše varování, ale bude pokračovat – takže jeden nefunkční odkaz nezastaví celou extrakci.

## Řešení běžných problémů

| Problém | Proč se to děje | Rychlé řešení |
|---------|----------------|---------------|
| **Relativní URL selhávají** | Atribut `src` může být `"../assets/icon.svg"` | Použijte `os.path.join(os.path.dirname(html_path), src)` k vyřešení. |
| **Duplicitní názvy souborů** | Dvě SVG se stejným názvem se přepíšou | Zahrňte hash obsahu do názvu souboru (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **Velké inline SVG způsobují špičky v paměti** | Ukládání celého markupu do seznamu před zápisem | Streamujte každý prvek přímo do souboru místo bufferování. |
| **Ne‑SVG obrázky proklouznou** | Některé `<img>` tagy končí na `.svg?version=1` | Odstraňte dotazové řetězce před kontrolou přípony (`src.split('?')[0]`). |

## Kompletní skript, který můžete zkopírovat a vložit

Níže je kompletní, připravený ke spuštění program. Uložte jej jako `extract_svg.py`, upravte `YOUR_DIRECTORY` a spusťte `python extract_svg.py`.

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

## Shrnutí – Jak extrahovat SVG v kostce

* **Načtěte HTML dokument** pomocí `HTMLDocument`.
* **Shromážděte inline `<svg>`** pomocí `get_elements_by_tag_name`.
* **Najděte externí SVG** pomocí CSS selektoru, který končí na `.svg`.
* **Uložte každý kus** – zapište markup přímo do souboru nebo zkopírujte odkazovaný soubor.
* **Řešte okrajové případy** jako relativní cesty, duplikáty a chybějící soubory.

To je kompletní odpověď na **jak extrahovat SVG** z HTML stránky, zabalená do jediného, snadno upravitelného skriptu.

## Co dál?

Nyní, když můžete **extrahovat SVG** spolehlivě, zvažte následující nápady:

* **Dávkové zpracování:** Procházet adresář HTML souborů a vytvořit knihovnu ikon.
* **Optimalizace:** Proveďte každé uložené SVG skrz SVGO (Node.js optimalizátor) pro zmenšení velikosti souboru.
* **Konverze:** Použijte `cairosvg` nebo `svglib` k převodu SVG na PNG pro starší prohlížeče.
* **Extrahování metadat:** Parsujte tagy `<title>` nebo `<desc>` uvnitř každého SVG pro vyhledávatelné štítky.

Každé z těchto témat se dotýká našich sekundárních klíčových slov – **read HTML document**, **save svg files**, **save inline svg**, **extract svg from html** – takže najdete spoustu materiálu k prozkoumání.

---

*Šťastné hackování! Pokud narazíte na problémy, zanechte komentář níže nebo mě kontaktujte na GitHubu. Svět SVG je obrovský, ale s těmi správnými nástroji je jejich extrakce hračka.*

## Co byste se měli naučit dál?

- [Uložit SVG dokument v Aspose.HTML pro Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Jak převést SVG na XPS pomocí Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Renderovat SVG dokument do formátu PNG v .NET s Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}