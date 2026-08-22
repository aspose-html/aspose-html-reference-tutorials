---
category: general
date: 2026-08-22
description: Hogyan exportáljunk linkeket HTML‑ből, és konvertáljuk őket markdown
  fájlba, bekezdésekkel együtt. Lépésről lépésre útmutató a HTML markdown konvertálásához.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export links
- convert html to markdown
- how to convert html
- how to extract paragraphs
- html to markdown file
language: hu
lastmod: 2026-08-22
og_description: Hogyan exportálhatod a linkeket egy HTML dokumentumból, és konvertálhatod
  markdown fájlba, bekezdésekkel együtt. Kövesd ezt a teljes útmutatót a megbízható
  HTML‑ról markdownra konvertáláshoz.
og_image_alt: How to export links while converting HTML to Markdown
og_title: Hogyan exportáljunk linkeket HTML‑ról Markdownra konvertálás közben – lépésről‑lépésre
  útmutató
schemas:
- author: GroupDocs
  dateModified: '2026-08-22'
  description: How to export links from HTML and convert it to a markdown file, including
    paragraphs. Step‑by‑step guide for HTML to markdown conversion.
  headline: How to export links while converting HTML to Markdown
  type: TechArticle
tags:
- HTML conversion
- Markdown
- Python
title: Hogyan exportáljunk linkeket HTML‑ról Markdownra konvertálás közben
url: /hu/python/general/how-to-export-links-while-converting-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan exportáljunk linkeket HTML‑ről Markdown‑ra konvertálás közben

Ha **hogyan exportáljunk linkeket** egy HTML‑oldalról, és az eredményt egy tiszta **html to markdown file**‑ba szeretnéd átalakítani, ez az útmutató pontos lépéseket mutat. Emellett megtudod, **hogyan vonjunk ki bekezdéseket**, hogy a Markdown‑kimenet csak a számodra fontos fő tartalmat tartalmazza. A tutorial végére már képes leszel megválaszolni a „**hogyan konvertáljunk html‑t** markdown‑ra” kérdést egy kész, futtatható szkripttel.

A linkek exportálása és a bekezdések kinyerése gyakori feladat, amikor webtartalmat migrálsz statikus oldalakra, dokumentációs portálokra vagy headless CMS‑back‑endre. Az alábbi megközelítés a GroupDocs Conversion SDK for Python‑nal működik, de a koncepciók bármely olyan könyvtárra alkalmazhatók, amely lehetővé teszi az export beállításait.

---

## Amire szükséged lesz

- Python 3.9 vagy újabb  
- `groupdocs-conversion` csomag (telepítés: `pip install groupdocs-conversion`)  
- Egy HTML‑fájl, amelyet feldolgozni szeretnél (például `input.html`)  
- Alapvető ismeretek a Python‑szkriptek írásáról  

---

## Hogyan exportáljunk linkeket HTML‑ről Markdown‑ra konvertálás közben

Az első nagy lépés a konverzió beállítása úgy, hogy csak a kívánt funkciók – a linkek és a bekezdések – kerüljenek a **html to markdown file**‑ba. Az SDK lehetővé teszi, hogy egy `MarkdownFeature` bitmaszkot állíts be; a `LINKS` és `PARAGRAPHS` kombinációjával a kimenet fókuszált marad.

```python
# Import the required classes from the GroupDocs Conversion SDK
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/input.html")

# Step 2: Create Markdown save options and select the features to export
markdown_options = MarkdownSaveOptions()
# Export only links and paragraphs from the HTML
markdown_options.features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

# Step 3: Convert the HTML to Markdown using the configured options
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)

print(f"Conversion complete. Markdown saved to {output_path}")
```

### Miért működik ez

- **`HTMLDocument`** beolvassa az eredeti fájlt, és felépíti a DOM‑ot, amelyet a konverter bejárhat.  
- **`MarkdownSaveOptions`** finomhangolt vezérlést biztosít arról, hogy az SDK mit ír ki. A `features` értékét `LINKS | PARAGRAPHS`‑ra állítva a motor figyelmen kívül hagyja a képeket, táblázatokat vagy szkripteket, ezáltal csökkentve a zajt a végső **html to markdown file**‑ban.  
- **`Converter.convert`** végzi a nehéz munkát. Figyelembe veszi a funkciómaszkot, kinyeri az `<a>` és `<p>` elemeket, és a szabványos Markdown szintaxis szerint írja ki őket.

---

## Hogyan konvertáljunk HTML‑t Markdown‑ra teljes tartalommal (opcionális)

Ha később úgy döntesz, hogy az egész oldalt – nem csak a linkeket és bekezdéseket – szeretnéd, egyszerűen módosítsd a funkciómaszkot:

```python
# Export everything the SDK supports (links, paragraphs, images, tables, etc.)
markdown_options.features = MarkdownFeature.ALL
```

Ugyanazzal a konverzióval most egy teljes **html to markdown file** jön létre, amely tükrözi az eredeti elrendezést. Ez bemutatja, **hogyan konvertáljunk html**‑t rugalmas módon: a kimenetet a funkciókapcsolók be‑ vagy kikapcsolásával szabályozod.

---

## Hogyan vonjunk ki csak bekezdéseket

Néha csak a cikk szöveges tartalmára vagy kíváncsi, a hiperhivatkozásokra nem. A bekezdéseket izolálhatod úgy, hogy a maszkot csak `PARAGRAPHS`‑ra állítod:

```python
markdown_options.features = MarkdownFeature.PARAGRAPHS
output_path = "YOUR_DIRECTORY/only_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)
```

Az eredményül kapott Markdown tiszta, sortöréssel ellátott szöveget tartalmaz, linkjelölés nélkül. Ez a kódrészlet megválaszolja a **hogyan vonjunk ki bekezdéseket** kérdést egy HTML‑forrásból.

---

## Gyakori buktatók és megoldások

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| Üres kimeneti fájl | A forrás HTML nem tartalmaz `<a>` vagy `<p>` elemeket, amelyek megfelelnek a kiválasztott funkcióknak. | Ellenőrizd a HTML‑szerkezetet, vagy bővítsd a funkciómaszkot (például `HEADINGS`‑t is vegyél fel). |
| Kódolási problémák | A HTML nem‑UTF‑8 karakterkészletet használ, és az SDK helytelenül olvassa be. | Adj meg explicit kódolást a `HTMLDocument`‑nek, pl. `HTMLDocument(path, encoding="iso-8859-1")`. |
| Meglévő Markdown felülírása | A szkript többször futtatva felülírja az előző fájlt. | Adj időbélyeget a kimeneti fájlnévhez, vagy ellenőrizd az `os.path.exists`‑t írás előtt. |

**Pro tipp:** Sok fájl feldolgozásakor csomagold a konverziólogikát egy ciklusba, és naplózd minden egyes eredményt. Így átlátható audit nyomot kapsz, és könnyen folytathatod a munkát hiba után.

---

## Teljes szkript, amelyet egyszerűen másolhatsz‑beilleszthetsz

Az alábbi önálló Python‑fájl (`convert_links_paragraphs.py`) közvetlenül futtatható. Argumentum‑parszolást tartalmaz, így a bemeneti és kimeneti útvonalakat a parancssorból adhatod meg anélkül, hogy a kódot módosítanád.

```python
#!/usr/bin/env python3
"""
convert_links_paragraphs.py

A complete example that shows how to export links and extract paragraphs
when converting HTML to a markdown file using GroupDocs Conversion SDK.
"""

import argparse
import os
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

def convert_html_to_md(input_html: str, output_md: str, features: int) -> None:
    """Perform the conversion with the given feature mask."""
    if not os.path.isfile(input_html):
        raise FileNotFoundError(f"Input file not found: {input_html}")

    # Load the HTML document
    html_doc = HTMLDocument(input_html)

    # Configure markdown options
    md_options = MarkdownSaveOptions()
    md_options.features = features

    # Run the conversion
    Converter.convert(html_doc, md_options, output_md)
    print(f"✅ Conversion finished – markdown saved to: {output_md}")

def main() -> None:
    parser = argparse.ArgumentParser(
        description="How to export links while converting HTML to Markdown."
    )
    parser.add_argument("input", help="Path to the source HTML file.")
    parser.add_argument(
        "output",
        help="Path for the resulting markdown file (e.g., links_and_paragraphs.md).",
    )
    parser.add_argument(
        "--links",
        action="store_true",
        help="Include links in the markdown output.",
    )
    parser.add_argument(
        "--paragraphs",
        action="store_true",
        help="Include paragraphs in the markdown output.",
    )
    args = parser.parse_args()

    # Build the feature mask based on user flags
    selected_features = 0
    if args.links:
        selected_features |= MarkdownFeature.LINKS
    if args.paragraphs:
        selected_features |= MarkdownFeature.PARAGRAPHS

    # Default to both links and paragraphs if no flag is provided
    if selected_features == 0:
        selected_features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

    try:
        convert_html_to_md(args.input, args.output, selected_features)
    except Exception as exc:
        print(f"❌ Conversion failed: {exc}")

if __name__ == "__main__":
    main()
```

**Hogyan futtassuk**

```bash
python convert_links_paragraphs.py YOUR_DIRECTORY/input.html YOUR_DIRECTORY/links_and_paragraphs.md --links --paragraphs
```

A fenti parancs bemutatja, **hogyan exportáljunk linkeket** és **hogyan vonjunk ki bekezdéseket** egyetlen hívásban. A `--links` vagy `--paragraphs` kapcsolók elhagyásával a kimenetet a saját igényeidhez igazíthatod.

---

## Ellenőrzés – hogyan néz ki a kimenet

A következő egyszerű HTML (`input.html`) alapján:

```html
<!DOCTYPE html>
<html>
<head><title>Sample page</title></head>
<body>
  <p>Welcome to the tutorial.</p>
  <p>Visit <a href="https://example.com">our site</a> for more info.</p>
</body>
</html>
```

A szkript mindkét kapcsolóval futtatva `links_and_paragraphs.md`‑t hoz létre:

```markdown
Welcome to the tutorial.

Visit [our site](https://example.com) for more info.
```

Láthatod, hogy csak a két bekezdés és a hiperhivatkozás maradt meg – pontosan az, amit a **hogyan exportáljunk linkeket** keresésekor vártál a **convert html to markdown** folyamat során.

---

## Következő lépések és kapcsolódó témák

- **How to convert html to markdown** with images: add `MarkdownFeature.IMAGES` to the mask.  
- **How to extract paragraphs** and then post‑process


## Mit érdemes még megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy elsajátíthasd a további API‑funkciókat, és alternatív megvalósítási megközelítéseket fedezhess fel saját projektjeidben.

- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [Convert HTML to Markdown – Complete C# Guide](/html/english/java/conversion-html-to-other-formats/convert-html-to-markdown-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}