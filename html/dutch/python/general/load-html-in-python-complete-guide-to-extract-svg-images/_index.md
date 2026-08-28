---
category: general
date: 2026-06-10
description: Laad HTML in Python om SVG‑afbeeldingen van je pagina’s te extraheren—stap‑voor‑stap
  code, tips en afhandeling van randgevallen.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: nl
og_description: Laad HTML in Python en extraheer SVG‑afbeeldingen met een duidelijk,
  uitvoerbaar voorbeeld. Leer hoe je HTML‑SVG‑elementen kunt zoeken en randgevallen
  kunt afhandelen.
og_title: HTML in Python laden – SVG‑afbeeldingen efficiënt extraheren
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
title: HTML laden in Python – Complete gids voor het extraheren van SVG‑afbeeldingen
url: /nl/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML laden in Python – Complete gids voor het extraheren van SVG-afbeeldingen

Heb je ooit **HTML in Python moeten laden** alleen maar om elke SVG-afbeelding van een pagina te halen? Je bent niet de enige. Of je nu een web‑scraper bouwt, een asset‑rapport genereert, of gewoon nieuwsgierig bent naar de iconen die een site gebruikt, weten hoe je **SVG-afbeeldingen kunt extraheren** bespaart je veel handmatig zoeken.

In deze tutorial lopen we een praktische, end‑to‑end oplossing door die **HTML laadt in Python**, vervolgens **HTML SVG**‑elementen doorzoekt, **inline SVG** vindt, en zelfs externe SVG‑bestanden oppikt die worden verwezen door `<img>`‑tags. Aan het einde heb je een herbruikbaar script, een reeks tips voor de lastige onderdelen, en een duidelijk beeld van hoe de output eruitziet.

## Wat je zult meenemen

* Een volledig uitvoerbaar Python‑script dat een lokaal HTML‑bestand (of een opgehaalde pagina) parseert en elke SVG die het kan vinden opsomt.  
* Inzicht in het verschil tussen **inline SVG** (`<svg>…</svg>`) en **external SVG** (`<img src="… .svg">`).  
* Strategieën voor het omgaan met slecht gevormde markup, ontbrekende bestanden en namespace‑eigenaardigheden.  
* Ideeën om de code uit te breiden — de SVG’s opslaan, converteren naar PNG, of invoeren in een database.

### Vereisten

* Python 3.8+ geïnstalleerd.  
* Basiskennis van Python’s `requests` en `BeautifulSoup` libraries (we importeren ze, geen diepe duik nodig).  
* Een lokaal HTML‑bestand of een URL die je wilt scannen.  

Laten we nu duiken.

## HTML laden in Python – De parser instellen

De allereerste stap is om **HTML te laden in Python**. Je kunt een bestand van de schijf lezen of een externe pagina ophalen. Hieronder staat een minimale, maar robuuste helper die beide doet:

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

> **Waarom dit belangrijk is:** Met `BeautifulSoup` worden de eigenaardigheden van ruwe string‑parsing abstract, en de functie verwerkt zowel lokale bestanden als externe URL’s op een elegante manier. Bovendien wordt er een uitzondering opgegooid als een netwerkverzoek mislukt — zodat je meteen weet wanneer er iets mis is gegaan.

## SVG-afbeeldingen extraheren – Inline SVG-elementen vinden

Zodra het document is geladen, is de volgende logische stap om **inline SVG**‑tags te **vinden**. Inline SVG is direct in de HTML‑markup ingebed, wat betekent dat je het rechtstreeks uit de DOM kunt halen.

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

*Pro tip:* Als de pagina SVG‑namespaces gebruikt (`<svg xmlns="http://www.w3.org/2000/svg">`), vindt `BeautifulSoup` de tag nog steeds omdat het standaard namespaces negeert. Dat is een handige eigenschap wanneer je gewoon **HTML SVG** aan het doorzoeken bent.

## HTML SVG zoeken – Externe `<img>`-referenties afhandelen

Veel sites embedden SVG niet direct; ze verwijzen naar externe bestanden via `<img src="icon.svg">`. Om die te vangen, moeten we over elke `<img>`‑tag itereren, de `src` controleren, en kijken of deze eindigt op `.svg`.

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

> **Edge case alert:** Sommige pagina’s gebruiken query‑strings (`icon.svg?v=2`) of fragmenten (`icon.svg#layer`). De `endswith(".svg")`‑check werkt nog steeds omdat we alleen naar het onderkastte deel van de string kijken. Als je strengere validatie nodig hebt, overweeg dan `urllib.parse` te gebruiken om parameters eerst te strippen.

## Inline SVG vinden – De resultaten rapporteren

Nu we twee lijsten hebben — één voor inline SVG‑markup en een andere voor externe bestandsreferenties — kunnen we ze combineren en het totale aantal rapporteren. Dit spiegelt de oorspronkelijke snippet die je plaatste, maar voegt een beetje meer context toe.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Alles samenvoegen – Volledig script

Hieronder staat het complete, kant‑klaar te‑runnen programma. Sla het op als `extract_svg.py` en wijs het naar een lokaal HTML‑bestand of een URL.

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

### Verwachte output

Het uitvoeren van het script tegen een voorbeeld `sample.html` kan bijvoorbeeld het volgende opleveren:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Als je het download‑blok uitcommentarieert, de externe SVG

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [svg to png java – Converteer SVG naar afbeelding met Aspose.HTML voor Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}