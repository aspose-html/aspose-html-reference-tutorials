---
category: general
date: 2026-05-31
description: Lernen Sie, wie Sie SVG aus HTML mit Python extrahieren. Dieses Schritt‑für‑Schritt‑Tutorial
  zeigt, wie man HTML‑Dokumente liest, SVG‑Dateien speichert und Inline‑SVG effizient
  speichert.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: de
og_description: Wie man SVG aus HTML mit Python extrahiert. Folgen Sie diesem Tutorial,
  um HTML‑Dokumente zu lesen, SVG‑Dateien zu speichern und Inline‑SVG mühelos zu verarbeiten.
og_title: Wie man SVG aus HTML mit Python extrahiert – Komplettanleitung
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
title: Wie man SVG aus HTML mit Python extrahiert – Vollständige Anleitung
url: /de/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man SVG aus HTML mit Python extrahiert – Komplettanleitung

Haben Sie sich jemals gefragt, **wie man SVG** aus einer unordentlichen HTML‑Seite extrahiert, ohne sich die Haare zu raufen? Sie sind nicht allein. Egal, ob Sie einen Web‑Scraper, eine Design‑Pipeline bauen oder einfach Icons stapelweise exportieren müssen, das Wissen **wie man SVG extrahiert** ist ein praktischer Trick, der Zeit und Kopfschmerzen spart.

In diesem Tutorial zeigen wir Ihnen genau **wie man SVG extrahiert** mit der Aspose.HTML‑Bibliothek für Python. Wir lesen das HTML‑Dokument, holen sowohl das Inline‑`<svg>`‑Markup **und** externe SVG‑Verweise heraus und **speichern SVG‑Dateien** auf der Festplatte – alles in einem übersichtlichen, wiederverwendbaren Skript. Am Ende haben Sie eine sofort einsatzbereite Lösung, die Sie an Ihre eigenen Projekte anpassen können.

> **Pro‑Tipp:** Wenn Sie nur einen schnellen Blick auf die Seite werfen wollen, funktioniert `BeautifulSoup` ebenfalls, aber Aspose.HTML liefert Ihnen ein vollständiges DOM, wodurch das Extrahieren sowohl von Inline‑ als auch verlinkten SVGs zum Kinderspiel wird.

## Was Sie benötigen

* Python 3.8+ (der Code verwendet f‑Strings, daher ist 3.6+ das absolute Minimum)
* `pip install aspose-html` – die kommerzielle Bibliothek, die unser HTML‑Parsing ermöglicht
* Ein Ordner mit einer `input.html`‑Datei, die die SVGs enthält, die Sie extrahieren möchten
* Schreibberechtigung für das Ausgabeverzeichnis (wir nennen es `YOUR_DIRECTORY`)

Das war's – keine zusätzlichen Binärdateien, keine Headless‑Browser. Einfach, oder?

## Schritt 1: HTML‑Dokument mit Aspose.HTML lesen

Das Erste, was Sie tun müssen, ist **das HTML‑Dokument zu lesen**, damit Sie dessen DOM‑Baum durchlaufen können. Aspose.HTML liefert Ihnen ein `HTMLDocument`‑Objekt, das sich wie das `document` eines Browsers verhält.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Warum das wichtig ist:* Durch das Laden des HTML in ein korrektes DOM vermeiden Sie die Fallstricke der regex‑basierten Analyse und erhalten Methoden wie `get_elements_by_tag_name` und `query_selector_all` kostenlos.

## Schritt 2: Alle Inline‑`<svg>`‑Elemente sammeln

Inline‑SVGs sind die `<svg>…</svg>`‑Blöcke, die direkt im HTML stehen. Um **Inline‑SVG zu speichern**, benötigen wir lediglich ihr äußeres HTML.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Beachten Sie, dass wir das rohe Markup direkt an `svg_contents` anhängen. Später entscheiden wir, ob jeder Eintrag Markup oder ein Dateipfad ist.

## Schritt 3: Externe SVG‑Verweise finden (img‑ und object‑Tags)

Viele Seiten verlinken externe SVG‑Dateien über `<img src="icon.svg">` oder `<object data="logo.svg">`. Um **SVG aus HTML zu extrahieren**, müssen wir diese URLs ebenfalls erfassen.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Hinweis zu Sonderfällen:* Wenn die SVG‑URL relativ ist, sollten Sie sie mit dem Basis‑Pfad der HTML‑Datei verbinden. Der Einfachheit halber gehen wir davon aus, dass das HTML neben den SVG‑Dateien liegt.

## Schritt 4: Jede SVG in eine separate Datei schreiben

Jetzt, da wir eine gemischte Liste aus Markup‑Strings und Dateipfaden haben, iterieren wir und **speichern SVG‑Dateien**. Das Skript unterscheidet automatisch zwischen Inline‑Markup und einem Verweis auf eine vorhandene Datei.

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

**Was Sie sehen werden:** Nachdem das Skript fertig ist, enthält `YOUR_DIRECTORY` Dateien mit den Namen `svg_0.svg`, `svg_1.svg`, …, die entweder das ursprüngliche Inline‑Markup oder eine Kopie des externen SVGs enthalten.

### Erwartete Ausgabe

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Falls eine referenzierte Datei fehlt, gibt das Skript eine Warnung aus, fährt aber fort – ein defekter Link stoppt also nicht die gesamte Extraktion.

## Häufige Probleme behandeln

| Problem | Warum es passiert | Schnelllösung |
|---------|-------------------|---------------|
| **Relative URLs brechen** | Das `src`‑Attribut kann `"../assets/icon.svg"` sein | Verwenden Sie `os.path.join(os.path.dirname(html_path), src)`, um es aufzulösen. |
| **Doppelte Dateinamen** | Zwei SVGs mit demselben Namen überschreiben sich | Fügen Sie einen Hash des Inhalts in den Dateinamen ein (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **Große Inline‑SVGs verursachen Speicherspitzen** | Speichern des gesamten Markups in einer Liste vor dem Schreiben | Streamen Sie jedes Element direkt in eine Datei, anstatt zu puffern. |
| **Nicht‑SVG‑Bilder rutschen durch** | Einige `<img>`‑Tags enden mit `.svg?version=1` | Entfernen Sie Abfragezeichenfolgen vor der Erweiterungsprüfung (`src.split('?')[0]`). |

## Vollständiges Skript zum Kopieren‑Einfügen

Unten finden Sie das komplette, sofort ausführbare Programm. Speichern Sie es als `extract_svg.py`, passen Sie `YOUR_DIRECTORY` an und führen Sie `python extract_svg.py` aus.

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

## Zusammenfassung – Wie man SVG in Kürze extrahiert

* **HTML‑Dokument lesen** mit `HTMLDocument`.
* **Inline‑`<svg>` sammeln** via `get_elements_by_tag_name`.
* **Externe SVGs finden** mit einem CSS‑Selektor, der auf `.svg` endet.
* **Jedes Stück speichern** – Markup direkt in eine Datei schreiben oder die referenzierte Datei kopieren.
* **Sonderfälle behandeln** wie relative Pfade, Duplikate und fehlende Dateien.

Das ist die komplette Antwort auf **wie man SVG** aus einer HTML‑Seite extrahiert, verpackt in einem einzigen, leicht anpassbaren Skript.

## Was kommt als Nächstes?

Jetzt, da Sie **SVG zuverlässig extrahieren** können, überlegen Sie sich diese weiterführenden Ideen:

* **Batch‑Verarbeitung:** Durchlaufen Sie ein Verzeichnis mit HTML‑Dateien, um eine Icon‑Bibliothek zu erstellen.
* **Optimierung:** Führen Sie jedes gespeicherte SVG durch SVGO (ein Node.js‑Optimizer), um die Dateigröße zu reduzieren.
* **Konvertierung:** Verwenden Sie `cairosvg` oder `svglib`, um die SVGs in PNGs für ältere Browser zu verwandeln.
* **Metadaten‑Extraktion:** Parsen Sie `<title>`‑ oder `<desc>`‑Tags in jedem SVG für durchsuchbare Beschriftungen.

Jedes dieser Themen berührt unsere sekundären Schlüsselwörter – **read HTML document**, **save svg files**, **save inline svg**, **extract svg from html** – sodass Sie reichlich Material zum Erkunden finden.

---

*Viel Spaß beim Hacken! Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar oder melden Sie sich auf GitHub. Die Welt der SVGs ist groß, aber mit den richtigen Werkzeugen ist das Extrahieren ein Kinderspiel.*

## Was sollten Sie als Nächstes lernen?

- [SVG‑Dokument in Aspose.HTML für Java speichern](/html/english/java/saving-html-documents/save-svg-document/)
- [Wie man SVG mit Aspose.HTML für Java in XPS konvertiert](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [SVG‑Dokument im .NET‑Format PNG mit Aspose.HTML rendern](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}