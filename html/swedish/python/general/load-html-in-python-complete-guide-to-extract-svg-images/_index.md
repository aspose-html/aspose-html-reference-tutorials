---
category: general
date: 2026-06-10
description: Läs in HTML i Python för att extrahera SVG‑bilder från dina sidor—steg‑för‑steg‑kod,
  tips och hantering av kantfall.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: sv
og_description: Läs in HTML i Python och extrahera SVG‑bilder med ett tydligt, körbart
  exempel. Lär dig hur du söker efter HTML‑SVG‑element och hanterar kantfall.
og_title: Läs in HTML i Python – Extrahera SVG-bilder effektivt
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
title: Ladda HTML i Python – Komplett guide för att extrahera SVG‑bilder
url: /sv/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Läs in HTML i Python – Komplett guide för att extrahera SVG‑bilder

Har du någonsin behövt **load HTML in Python** bara för att hämta varje SVG‑grafik från en sida? Du är inte ensam. Oavsett om du bygger en web‑scraper, genererar en tillgångsrapport, eller bara är nyfiken på vilka ikoner en webbplats använder, så sparar kunskapen om hur man **extract SVG images** dig mycket manuellt letande.

I den här handledningen går vi igenom en praktisk, end‑to‑end‑lösning som **loads HTML in Python**, sedan **searches HTML SVG**‑element, **finds inline SVG**, och även hämtar externa SVG‑filer som refereras av `<img>`‑taggar. I slutet har du ett återanvändbart skript, några tips för de knepiga delarna, och en tydlig bild av hur resultatet ser ut.

## Vad du får med dig

* Ett fullt körbart Python‑skript som parsar en lokal HTML‑fil (eller en hämtad sida) och listar varje SVG den kan hitta.  
* Förståelse för skillnaden mellan **inline SVG** (`<svg>…</svg>`) och **external SVG** (`<img src="… .svg">`).  
* Strategier för att hantera felaktig markup, saknade filer och namnrymds‑egenskaper.  
* Idéer för att utöka koden—spara SVG‑filerna, konvertera dem till PNG, eller föra in dem i en databas.

### Förutsättningar

* Python 3.8+ installerat.  
* Grundläggande kunskap om Python‑biblioteken `requests` och `BeautifulSoup` (vi importerar dem, ingen djupdykning behövs).  
* En lokal HTML‑fil eller en URL du vill skanna.  

Nu, låt oss dyka ner.

## Läs in HTML i Python – Ställ in parsern

Det allra första steget är att **load HTML in Python**. Du kan antingen läsa en fil från disk eller hämta en fjärrsida. Nedan är en minimal, men robust, hjälpfunktion som gör båda:

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

> **Varför detta är viktigt:** Att använda `BeautifulSoup` abstraherar bort nyanserna i rå sträng‑parsing, och funktionen hanterar både lokala filer och fjärr‑URL:er på ett smidigt sätt. Den kastar också ett undantag om ett nätverks‑request misslyckas—så du vet omedelbart när något gick fel.

## Extrahera SVG‑bilder – Hitta inline SVG‑element

När dokumentet är laddat är nästa logiska steg att **find inline SVG**‑taggar. Inline SVG är inbäddat direkt i HTML‑markupen, vilket betyder att du kan hämta det rakt från DOM.

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

*Pro tip:* Om sidan använder SVG‑namnrymder (`<svg xmlns="http://www.w3.org/2000/svg">`), så hittar `BeautifulSoup` fortfarande taggen eftersom den ignorerar namnrymder som standard. Det är en trevlig bekvämlighet när du bara **searches HTML SVG**.

## Sök HTML SVG – Hantera externa `<img>`‑referenser

Många webbplatser bäddar inte in SVG direkt; de refererar till externa filer via `<img src="icon.svg">`. För att fånga dem måste vi iterera över varje `<img>`‑tagg, kontrollera dess `src` och se om den slutar med `.svg`.

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

> **Edge case alert:** Vissa sidor använder query‑strängar (`icon.svg?v=2`) eller fragment (`icon.svg#layer`). Kontrollen `endswith(".svg")` fungerar fortfarande eftersom vi bara tittar på den gemenerade slutdelen av strängen. Om du behöver striktare validering, överväg att använda `urllib.parse` för att ta bort parametrar först.

## Hitta inline SVG – Rapportera resultaten

Nu när vi har två listor—en för inline SVG‑markup och en för externa filreferenser—kan vi kombinera dem och rapportera det totala antalet. Detta speglar det ursprungliga kodsnutten du postade, men lägger till lite mer kontext.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Sätt ihop allt – Fullständigt skript

Nedan är det kompletta, färdiga att köra programmet. Spara det som `extract_svg.py` och peka det mot antingen en lokal HTML‑fil eller en URL.

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

### Förväntad utdata

Att köra skriptet mot ett exempel `sample.html` kan ge:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Om du avkommenterar nedladdningsblocket, den externa SVG

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}