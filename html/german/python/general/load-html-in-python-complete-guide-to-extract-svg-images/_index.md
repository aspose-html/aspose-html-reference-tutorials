---
category: general
date: 2026-06-10
description: Lade HTML in Python, um SVG‑Bilder von deinen Seiten zu extrahieren –
  Schritt‑für‑Schritt‑Code, Tipps und Umgang mit Sonderfällen.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: de
og_description: Lade HTML in Python und extrahiere SVG‑Bilder mit einem klaren, ausführbaren
  Beispiel. Erfahre, wie du HTML‑SVG‑Elemente suchst und Sonderfälle behandelst.
og_title: HTML in Python laden – SVG‑Bilder effizient extrahieren
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: HTML in Python laden – Vollständiger Leitfaden zum Extrahieren von SVG‑Bildern
url: /de/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML in Python laden – Vollständiger Leitfaden zum Extrahieren von SVG‑Bildern

Haben Sie jemals **HTML in Python laden** müssen, nur um jedes SVG‑Grafik aus einer Seite zu holen? Sie sind nicht allein. Egal, ob Sie einen Web‑Scraper bauen, einen Asset‑Report erstellen oder einfach nur neugierig auf die Icons einer Seite sind, zu wissen, wie man **SVG‑Bilder extrahiert**, spart Ihnen viel manuelle Suche.

In diesem Tutorial gehen wir Schritt für Schritt durch eine praktische End‑to‑End‑Lösung, die **HTML in Python lädt**, dann **HTML‑SVG**‑Elemente **sucht**, **inline SVG** findet und sogar externe SVG‑Dateien, die über `<img>`‑Tags referenziert werden, abruft. Am Ende haben Sie ein wiederverwendbares Skript, einige Tipps für knifflige Punkte und ein klares Bild davon, wie die Ausgabe aussieht.

## Was Sie am Ende haben werden

* Ein vollständig ausführbares Python‑Skript, das eine lokale HTML‑Datei (oder eine abgefragte Seite) analysiert und jedes gefundene SVG auflistet.  
* Verständnis des Unterschieds zwischen **inline SVG** (`<svg>…</svg>`) und **external SVG** (`<img src="… .svg">`).  
* Strategien zum Umgang mit fehlerhaftem Markup, fehlenden Dateien und Namespace‑Eigenheiten.  
* Ideen zur Erweiterung des Codes – SVGs speichern, in PNG konvertieren oder in eine Datenbank einspeisen.

### Voraussetzungen

* Python 3.8+ installiert.  
* Grundlegende Vertrautheit mit den Bibliotheken `requests` und `BeautifulSoup` von Python (wir importieren sie, ein tiefes Eintauchen ist nicht nötig).  
* Eine lokale HTML‑Datei oder eine URL, die Sie scannen möchten.  

Jetzt legen wir los.

## HTML in Python laden – Parser einrichten

Der allererste Schritt ist, **HTML in Python zu laden**. Sie können entweder eine Datei von der Festplatte lesen oder eine entfernte Seite abrufen. Unten finden Sie einen minimalen, aber robusten Helfer, der beides erledigt:

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **Warum das wichtig ist:** `BeautifulSoup` abstrahiert die Eigenheiten der reinen String‑Verarbeitung, und die Funktion verarbeitet sowohl lokale Dateien als auch entfernte URLs elegant. Sie wirft außerdem eine Ausnahme, wenn eine Netzwerk‑Anfrage fehlschlägt – sodass Sie sofort wissen, wenn etwas schiefgelaufen ist.

## SVG‑Bilder extrahieren – Inline‑SVG‑Elemente finden

Sobald das Dokument geladen ist, ist der nächste logische Schritt, **inline SVG**‑Tags zu **finden**. Inline SVG ist direkt im HTML‑Markup eingebettet, sodass Sie es direkt aus dem DOM holen können.

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*Pro‑Tipp:* Wenn die Seite SVG‑Namespaces verwendet (`<svg xmlns="http://www.w3.org/2000/svg">`), findet `BeautifulSoup` das Tag trotzdem, weil es standardmäßig Namespaces ignoriert. Das ist praktisch, wenn Sie einfach **HTML‑SVG** suchen.

## HTML‑SVG suchen – Externe `<img>`‑Referenzen verarbeiten

Viele Seiten betten SVG nicht direkt ein; sie referenzieren externe Dateien über `<img src="icon.svg">`. Um diese zu erfassen, müssen wir über jedes `<img>`‑Tag iterieren, dessen `src` prüfen und schauen, ob es mit `.svg` endet.

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **Edge‑Case‑Hinweis:** Einige Seiten nutzen Query‑Strings (`icon.svg?v=2`) oder Fragmente (`icon.svg#layer`). Die Prüfung `endswith(".svg")` funktioniert weiterhin, weil wir nur das kleingeschriebene Ende des Strings betrachten. Wenn Sie strengere Validierung benötigen, sollten Sie `urllib.parse` verwenden, um Parameter vorher zu entfernen.

## Inline‑SVG finden – Ergebnisse melden

Jetzt, wo wir zwei Listen haben – eine für inline SVG‑Markup und eine für externe Dateireferenzen – können wir sie zusammenführen und die Gesamtzahl melden. Das spiegelt das ursprüngliche Snippet wider, das Sie gepostet haben, fügt jedoch etwas mehr Kontext hinzu.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Alles zusammenführen – Komplettes Skript

Unten finden Sie das vollständige, sofort ausführbare Programm. Speichern Sie es als `extract_svg.py` und verweisen Sie entweder auf eine lokale HTML‑Datei oder eine URL.

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### Erwartete Ausgabe

Das Ausführen des Skripts gegen ein Beispiel‑`sample.html` könnte folgendes erzeugen:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Wenn Sie den Download‑Block auskommentieren, wird das externe SVG


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}